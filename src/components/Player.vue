<template>
  <div>
    <play-button :audio.once="audio"></play-button>
	<progress-bar :audio.once="audio"></progress-bar>
	<div>
    	<mute-button class="mute" :audio.once="audio"></mute-button>
    	<volume-bar class="volume" :audio.once="audio"></volume-bar>
	</div>
  </div>
</template>

<script>
	import PlayButton from './PlayButton'
	import VolumeBar from './VolumeBar'
	import MuteButton from './MuteButton';
	import ProgressBar from './ProgressBar';
	export default {
		props: {
			audio: null
		},
		components: {
			PlayButton,
			VolumeBar,
			MuteButton,
			ProgressBar
		}
	}
</script>

<style scoped>
	.mute, .volume {
		display: inline-block;
	}
</style>