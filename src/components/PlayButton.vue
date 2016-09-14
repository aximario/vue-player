<template>
  <button @click="handleClick">
    <icon class="icon" :icon="icon"></icon>
  </button>
</template>

<style scoped>
	.icon {
		font-size: 36px;
		color: #cdcdcd;
	}
	
	button {
		border: none;
		background-color: transparent;
		outline: none;
	}
</style>

<script>
	import Icon from './Icon'
	export default {
		props: {
			audio: null
		},
		data() {
			return {
				paused: this.audio.paused
			}
		},
		components: {
			Icon
		},
		computed: {
			icon: function() {
				return this.paused ? '&#xe602;' : '&#xe603;'
			}
		},
		methods: {
			handleClick: function() {
				this.paused ? this.audio.play() : this.audio.pause();
				this.paused = !this.paused;
			}
		}
	}
</script>