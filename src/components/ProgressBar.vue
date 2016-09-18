<template>
	<div class="progress-bar">
		<progressed class="cache" :length.once="200" :percent="cache"></progressed>
		<progressed class="progress" :length.once="200" :percent="percent"></progressed>
		<drag-dot class="drag-dot" :length.once="200" :percent="percent" v-on:drag="drag"></drag-dot>
	</div>
</template>

<style scoped>
	.progress-bar {
		position: relative;
		width: 200px;
		height: 4px;
		background-color: rgba(255, 255, 255, .1);
		border-radius: 2px;
	}
	
	.progress,
	.cache {
		left: 0;
		top: 0;
	}
	
	.progress {
		background-color: lightblue;
	}
	
	.cache {
		background-color: lightgreen;
	}
	
	.drag-dot {
		left: -5px;
		top: -3px;
	}
</style>

<script>
	import Progressed from './Progressed';
	import DragDot from './DragDot';
	export default {
		components: {
			Progressed,
			DragDot
		},
		data() {
			return {
				percent: 0,
				cache: 0
			}
		},
		methods: {
			drag(percent) {
				this.$dispatch('update-time', percent);
			}
		},
		events: {
			'audio-time-update': function(obj) {
				this.percent = obj.currentTime / obj.duration;
			},
			'audio-progress': function(obj) {
				this.cache = obj.buffered.end(0) / obj.duration;
			}
		}
	}
</script>