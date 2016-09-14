<template>
  <button v-pause @click="handleClick">
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
		components: {
			Icon
		},
		props: {
			audio: null
		},
		data() {
			return {

				// 代理audio的paused属性
				paused: undefined
			}
		},
		computed: {
			icon() {
				return this.paused ? '&#xe602;' : '&#xe603;';
			}
		},
		methods: {
			handleClick: function() {
				this.paused ? this.audio.play() : this.audio.pause();
			}
		},
		directives: {

			// 同步audio的paused状态
			pause: {
				bind: function() {

					// 初始化paused状态
					this.vm.paused = this.vm.audio.paused;
					this.vm.audio.addEventListener('pause', e => {
						this.vm.paused = true;
					}, false);
					this.vm.audio.addEventListener('play', e => {
						this.vm.paused = false;
					}, false);
				}
			}
		}
	}
</script>