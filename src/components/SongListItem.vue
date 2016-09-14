<template>
	<div @click="handleClick">
		{{song.name}}
	</div>
</template>

<style>

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