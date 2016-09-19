<template>
    <div id="app">
		<audio v-el:audio></audio>
	    <div>
			<logo></logo>
			<audio-control 
				class="audio-control"
				v-on:pause="pause" 
				v-on:play="play" 
				v-on:next-song="nextSong" 
				v-on:prev-song="prevSong" 
				v-on:mute="mute" 
				v-on:unmute="unmute" 
				v-on:update-volume="updateVolume" 
				v-on:update-time="updateTime"></audio-control>
			<audio-list v-on:change-song="changeSong"></audio-list>
	    </div>
    </div>
</template>

<script>
	import AudioControl from './components/AudioControl';
	import AudioList from './components/AudioList';
	import Logo from './components/Logo';
	import './assets/styles/normalize.css';
	export default {
		components: {
			AudioControl,
			AudioList,
			Logo
		},
		methods: {
			pause() {
				this.$els.audio.pause();
			},
			play() {
				this.$els.audio.play();
			},
			nextSong() {
				this.$broadcast('list-next');
			},
			prevSong() {
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
				this.$broadcast('list-next');
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
	html,
	body,
	#app {
		height: 100%
	}
	
	body {
		background-color: #272C30;
		font-family: Arial, Helvetica, sans-serif;
	}

	#app {
		width: 100%;
	}
	
	#app>div {
		position: relative;
		height: 100%;
		max-width: 1000px;
		margin: 0 auto;
	}
	
	#app>div:after {
		content: '';
		height: 0;
		display: block;
		clear: both;
	}
	
	.audio-control {
		width: 100%;
		max-width: 1280px;
		margin: 0 auto;
		position: absolute;
		bottom: 10px;
	}
</style>