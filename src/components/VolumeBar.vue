<template>
    <div class="bar">
		<progressed class="progress" :percent="volume"></progressed>
        <drag-dot class="drag-dot" v-on:drag="drag" :percent="volume"></drag-dot>
    </div>
</template>

<style scoped>
	.bar {
		position: relative;
		width: 100px;
		height: 4px;
		background-color: rgba(255, 255, 255, .1);

		border-radius: 2px;
	}
	.drag-dot {
		left: -5px;
		top: -3px;
	}
	.progress {
		left: 0;
		top: 0;
		background-color: lightblue;
	}
</style>

<script>
	import DragDot from './DragDot';
	import Progressed from './Progressed';
	export default {
		components: {
			DragDot,
			Progressed
		},
		data() {
			return {
				volume: 0.6
			}
		},
		methods: {
			drag(offset) {
				this.$dispatch('update-volume', offset/100);
			}
		},
		events: {
			'audio-volume-change': function(volume) {
				this.volume = volume;
			}
		}
	}
</script>