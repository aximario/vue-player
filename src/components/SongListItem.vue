<template>
	<div @click="handleClick">
		{{song.name}}
	</div>
</template>

<style scoped>
	div {
		padding: 14px;
		color: #eee;

		border-top: 1px solid #efefef;
		border-bottom: 1px solid #efefef;
	}
</style>

<script>
	export default {
		props: {
			audio: null,
			song: Object
		},
		methods: {

			// 播放这首歌
			handleClick: function() {
				let audio = this.audio;
				audio.src = this.song.src;
				audio.play();
			}
		}
	}
</script>