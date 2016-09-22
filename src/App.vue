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
			<audio-list v-on:change-song="changeSong" v-on:init-song="initSong"></audio-list>
			<audio-lyric :song-id='song.id'></audio-lyric>
	    </div>
    </div>
</template>

<script>
	import AudioControl from './components/audio-control/AudioControl';
	import AudioList from './components/audio-list/AudioList';
	import AudioLyric from './components/audio-lyric/AudioLyric'
	import Logo from './components/common/Logo';
	import './assets/styles/normalize.css';
	export default {
		components: {
			AudioControl,
			AudioList,
			AudioLyric,
			Logo
		},
		data() {
			return {
				song: null
			}
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
			initSong(song) {
				this.song = song;
				this.$els.audio.src = song.mp3Url;
			},
			changeSong(song) {
				this.song = song;
				let audio = this.$els.audio;
				audio.src = song.src;
				audio.play();
			}
		},
		ready() {
			let audio = this.$els.audio;
			audio.addEventListener('loadstart', e => {
				this.$broadcast('audio-loadstart');
			}, false);
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
				if (audio.readyState === 4) {
					this.$broadcast('audio-progress', {
						buffered: audio.buffered,
						duration: audio.duration
					});
				}
			}, false);
			audio.addEventListener('error', e => {
				try {
					throw e;
				} catch (e) {
					switch (audio.error.code) {
						case 2:
							console.error('网络错误，请检查网络状态');
							break;
						case 3:
							console.error('解码错误');
							this.$broadcast('list-next');
							break;
						case 4:
							console.error('不支持的媒体类型');
							this.$broadcast('list-next');
							break;
					}
				}
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