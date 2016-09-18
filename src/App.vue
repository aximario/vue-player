<template>
  <div id="app">
	  <audio v-el:audio></audio>
	  <audio-control 
	  	v-on:pause="pause" 
		v-on:play="play" 
		v-on:next-song="nextSong" 
		v-on:prev-song="prevSong" 
		v-on:mute="mute" 
		v-on:unmute="unmute" 
		v-on:update-volume="updateVolume" 
		v-on:update-time="updateTime"></audio-control>
	  <audio-list v-on:change-song="changeSong"></audio-list>
	  <audio-time></audio-time>
  </div>
</template>

<script>
	import AudioControl from './components/AudioControl';
	import AudioList from './components/AudioList';
	import AudioTime from './components/AudioTime';
	export default {
		components: {
			AudioControl,
			AudioList,
			AudioTime
		},
		methods: {
			pause() {
				this.$els.audio.pause();
			},
			play() {
				this.$els.audio.play();
			},
			nextSong(){
				this.$broadcast('list-next');
			},
			prevSong(){
				this.$broadcast('list-prev');
			},
			mute() {
				this.$els.audio.muted = true;
			},
			unmute() {
				this.$els.audio.muted = false;
			},
			updateVolume(volume) {
				this.$els.audio.volume = volume;
			},
			updateTime(percent) {
				let audio = this.$els.audio;
				audio.currentTime = audio.duration * percent;
			},
			changeSong(song) {
				let audio = this.$els.audio;
				audio.src = song.src;
				audio.play();
			}
		},
		ready() {
			let audio = this.$els.audio;
			audio.addEventListener('ended', e => {
				this.$broadcast('audio-ended');
			}, false);
			audio.addEventListener('play', e => {
				this.$broadcast('audio-play');
			}, false);
			audio.addEventListener('pause', e => {
				this.$broadcast('audio-pause');
			}, false);
			audio.addEventListener('volumechange', e => {
				this.$broadcast('audio-volume-change', audio.volume);
			}, false);
			audio.addEventListener('timeupdate', e => {
				this.$broadcast('audio-time-update', {
					currentTime: audio.currentTime,
					duration: audio.duration
				});
			}, false);
			audio.addEventListener('loadedmetadata', e => {
				this.$broadcast('audio-loaded-metadata', audio.duration);
			}, false);
			audio.addEventListener('progress', e => {
				this.$broadcast('audio-progress', {
					buffered: audio.buffered,
					duration: audio.duration
				});
			}, false);
		}
	}
</script>

<style>
	body {
		background-color: #272C30;
	}
</style>