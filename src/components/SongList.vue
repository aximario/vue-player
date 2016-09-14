<template>
	<div>
		<song-list-item v-for="item in list" :audio.once="audio" :song="item"></song-list-item>
	</div>
</template>

<script>
	import SongListItem from './SongListItem';
	export default {
		props: {
			audio: null
		},
		data() {
			return {
				list: [{
					id: 0,
					name: 'Alan Walker - Fade',
					src: 'http://o94al90ev.bkt.clouddn.com/songs/Alan%20Walker%20-%20Fade.mp3'
				}, {
					id: 1,
					name: 'BAAD - 君が好きだと叫びたい.',
					src: 'http://o94al90ev.bkt.clouddn.com/songs/BAAD%20-%20%E5%90%9B%E3%81%8B%E3%82%99%E5%A5%BD%E3%81%8D%E3%81%9F%E3%82%99%E3%81%A8%E5%8F%AB%E3%81%B2%E3%82%99%E3%81%9F%E3%81%84.mp3'
				}, {
					id: 2,
					name: '好妹妹乐队 - 不说再见',
					src: 'http://o94al90ev.bkt.clouddn.com/songs/%E5%A5%BD%E5%A6%B9%E5%A6%B9%E4%B9%90%E9%98%9F%20-%20%E4%B8%8D%E8%AF%B4%E5%86%8D%E8%A7%81.mp3'
				}]
			}
		},
		components: {
			SongListItem
		}
	}
</script>

<style scoped>

</style>