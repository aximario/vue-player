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
	import Icon from '../common/Icon'
	export default {
		components: {
			Icon
		},
		data() {
			return {
				paused: true,
				ended: false
			}
		},
		computed: {
			icon() {
				return (this.paused || this.ended) ? '&#xe602;' : '&#xe603;';
			}
		},
		methods: {
			handleClick: function(e) {
				e.stopPropagation();
				this.paused ? this.$dispatch('play') : this.$dispatch('pause');
			}
		},
		events: {

			// 调用了play()方法或者设置autoplay触发
			// !!!! 但是音频**不一定**立马播放
			// 如果没有足够的数据，会触发waiting事件，进入缓冲状态
			// 如果有足够的数据，音频播放，触发playing事件
			'audio-play': function() {
				this.paused = false;
			},

			'audio-pause': function() {
				this.paused = true;
			},
			'audio-loadstart': function() {
				this.ended = false;
			},
			'audio-ended': function() {
				this.ended = true;
			}
		}
	}
</script>