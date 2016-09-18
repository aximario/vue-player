<template>
  <button @click="handleClick">
    <icon class="icon" :icon="icon"></icon>
  </button>
</template>

<style scoped>
	.icon {
		font-size: 23px;
		color: #cdcdcd;
	}
	
	button {
		padding: 0;
		border: none;
		background-color: transparent;
		outline: none;
	}
</style>

<script>
	import Icon from './Icon'
	export default {
		components: {
			Icon
		},
		data() {
			return {
				muted: false
			}
		},
		computed: {
			icon: function() {
				return this.muted ? '&#xe605;' : '&#xe604;'
			}
		},
		methods: {
			handleClick(e) {
				e.stopPropagation();
				this.muted ? this.$dispatch('unmute') : this.$dispatch('mute');
				this.muted = !this.muted;
			}
		}
	}
</script>