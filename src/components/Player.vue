<template>
  <div>
    <play-button :audio.once="audio"></play-button>
    <mute-button :audio.once="audio"></mute-button>
    <volume-bar :audio.once="audio"></volume-bar>
  </div>
</template>

<script>
	import PlayButton from './PlayButton'
	import VolumeBar from './VolumeBar'
	import MuteButton from './MuteButton'
	export default {
		props: {
			audio: null
		},
		components: {
			PlayButton,
			VolumeBar,
			MuteButton
		}
	}
</script>

<style>
	body {
		background-color: #272C30;
	}
</style>