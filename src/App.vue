<template>
  <div id="app">
	  <audio v-el:audio src="http://o94al90ev.bkt.clouddn.com/songs/BAAD%20-%20%E5%90%9B%E3%81%8B%E3%82%99%E5%A5%BD%E3%81%8D%E3%81%9F%E3%82%99%E3%81%A8%E5%8F%AB%E3%81%B2%E3%82%99%E3%81%9F%E3%81%84.mp3"></audio>
	  <player :audio.once="$els.audio"></player>
	  <song-list :audio.once="$els.audio"></song-list>
  </div>
</template>

<script>
	import Player from './components/Player'
	import SongList from './components/SongList'
	export default {
		components: {
			Player,
			SongList
		}
	}
</script>

<style>
	body {
		background-color: #272C30;
	}
</style>