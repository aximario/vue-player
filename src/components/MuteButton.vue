<template>
  <button v-muted @click="handleClick">
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
		components: {
			Icon
		},
		props: {
			audio: null
		},
		data() {
			return {
				muted: undefined
			}
		},
		computed: {
			icon: function() {
				return this.muted ? '&#xe605;' : '&#xe604;'
			}
		},
		methods: {
			handleClick() {
				let audio = this.audio;
				if (this.muted) {
					audio.muted = false;
				} else {
					audio.muted = true;
				}
			}
		},
		directives: {

			// 同步audio的muted状态
			muted: {
				bind: function() {
					let audio = this.vm.audio;

					// 初始化muted状态
					this.vm.muted = audio.muted;
					audio.addEventListener('volumechange', e => {
						this.vm.muted = audio.muted;
					}, false);
				}
			}
		}
	}
</script>