<template>
	<div class="progress-bar" v-el:bgb>
		<progressed class="cache" :percent="cache"></progressed>
		<progressed class="progress" :percent="percent"></progressed>
		<drag-dot class="drag-dot" :percent="percent" v-on:drag="drag"></drag-dot>
	</div>
</template>

<style scoped>
	.progress-bar {
		position: relative;
		width: 100%;
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
		background-color: rgba(255, 255, 255, .3);
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
			drag(offset) {
				let computedWidth = Number(window.getComputedStyle(this.$els.bgb).width.split('px')[0]);
				this.$dispatch('update-time', offset/computedWidth);
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