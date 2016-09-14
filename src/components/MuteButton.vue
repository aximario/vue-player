<template>
  <button @click="handleClick">
    <icon class="icon" :icon="icon"></icon>
  </button>
</template>

<style scoped>
	.icon {
		font-size: 24px;
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
				muted: this.audio.muted
			}
		},
		components: {
			Icon
		},
		computed: {
			icon: function() {
				return this.muted ? '&#xe605;' : '&#xe604;'
			}
		},
		methods: {
			handleClick() {
				this.muted = !this.muted
				this.audio.muted = this.muted;
			}
		}
	}
</script>