<template>
	<div @click="handleClick">
		{{song.name}}
	</div>
</template>

<style scoped>
	div {
		font-size: 14px;
		padding: 14px;
		color: rgba(255, 255, 255, .5);
		border-top: 1px solid rgba(255, 255, 255, .5);
		cursor: pointer;
	}
</style>

<script>
	export default {
		props: {
			song: Object
		},
		methods: {
			handleClick: function() {
				let audio = this.audio;

				// dispatch 选择歌曲 事件，通知音频列表更新当前音频
				this.$dispatch('select-song', this.song);
			}
		}
	}
</script>