<template>
	<div class="progress-bar">
		<progressed class="progress" :length.once="percent * 200"></progressed>
		<drag-dot class="drag-dot" :length.once="200" :offset.once="percent * 200" v-on:drag="drag"></drag-dot>
	</div>
</template>

<style scoped>
	.progress-bar {
		position: relative;
		width: 200px;
		height: 4px;
		background-color: rgba(255, 255, 255, .1);
		;
	}
	
	.progress {
		left: 0;
		top: 0;
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
		props: {
			audio: null
		},
		components: {
			Progressed,
			DragDot
		},
		data() {
			return {
				percent: 0
			}
		},
		methods: {
			drag(offset) {
				let percent = offset / 200,
					audio = this.audio;
				this.percent = percent;
				audio.currentTime = audio.duration * percent;
				this.$broadcast('progress', offset);
			}
		},
		ready() {
			let audio = this.audio;
			audio.addEventListener('timeupdate', e => {
				this.percent = audio.currentTime / audio.duration;
				this.$broadcast('progress', this.percent * 200);
				this.$broadcast('update-offset', this.percent * 200);
			}, false);
		}
	}
</script>