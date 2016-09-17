<template>
    <div class="bar">
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
</style>

<script>
	import DragDot from './DragDot';
	export default {
		components: {
			DragDot
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
				let volume = offset/100
				this.audio.volume = volume;
				this.volume = volume;
			}
		}
	}
</script>