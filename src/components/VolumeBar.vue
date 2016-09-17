<template>
    <div class="bar">
		<progressed class="progress" :length.once="volume * 100"></progressed>
        <drag-dot class="drag-dot" v-on:drag="updateVolume" :offset.once="60" :length.once="100"></drag-dot>
    </div>
</template>

<style scoped>
	.bar {
		position: relative;
		width: 100px;
		height: 4px;
		background-color: rgba(255, 255, 255, .1);
	}
	.drag-dot {
		left: -5px;
		top: -3px;
	}
	.progress {
		left: 0;
		top: 0;
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
		props: {
			audio: null
		},
		data() {
			return {
				volume: 0.6
			}
		},
		methods: {
			updateVolume(offset) {
				let volume = offset/100;
				this.volume = volume;
				this.audio.volume = volume;
				this.$broadcast('progress', offset);
			}
		}
	}
</script>