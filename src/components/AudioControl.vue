<template>
    <div>
		<prev-button></prev-button>
		<play-button :audio.once="audio"></play-button>
		<next-button></next-button>
		<progress-bar :audio.once="audio"></progress-bar>
		<div class="volume-control">
			<mute-button class="mute" :audio.once="audio"></mute-button>
			<volume-bar class="volume" :audio.once="audio"></volume-bar>
		</div>
    </div>
</template>

<script>
	import PrevButton from './PrevButton';
	import PlayButton from './PlayButton';
	import NextButton from './NextButton';
	import VolumeBar from './VolumeBar';
	import MuteButton from './MuteButton';
	import ProgressBar from './ProgressBar';
	export default {
		props: {
			audio: null
		},
		components: {
			PrevButton,
			PlayButton,
			NextButton,
			VolumeBar,
			MuteButton,
			ProgressBar
		}
	}
</script>

<style scoped>
	.volume-control:after {
		content: '';
		display: block;
		height: 0;
		clear: both;
	}
	
	.mute,
	.volume {
		float: left;
	}
	
	.mute {
		margin: 8px 6px 8px 0;
	}
	
	.volume {
		margin: 17px 0;
	}
</style>