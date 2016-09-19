<template>
  <button @click="handleClick">
    <icon class="icon" :icon="icon"></icon>
  </button>
</template>

<style scoped>
	.icon {
		font-size: 36px;
		color: rgba(255, 255, 255, .85);
	}
	
	button {
		border: none;
		background-color: transparent;
		outline: none;
		cursor: pointer;
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
				paused: true
			}
		},
		computed: {
			icon() {
				return this.paused ? '&#xe602;' : '&#xe603;';
			}
		},
		methods: {
			handleClick: function(e) {
				e.stopPropagation();
				this.paused ? this.$dispatch('play') : this.$dispatch('pause');
			}
		},
		events: {
			'audio-play': function() {
				this.paused = false;
			},
			'audio-pause': function() {
				this.paused = true;
			},
			'audio-ended': function() {
				this.paused = true;
			}
		}
	}
</script>