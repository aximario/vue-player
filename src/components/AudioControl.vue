<template>
    <div class="audio-control">
		<div class="control-buttons">
			<prev-button></prev-button>
			<play-button></play-button>
			<next-button></next-button>
		</div>
		<div class="control-volume">
			<audio-time class="audio-time"></audio-time>
			<mute-button class="mute"></mute-button>
			<volume-bar class="volume"></volume-bar>
		</div>
		<div class="control-progress">
			<progress-bar class="progress-bar"></progress-bar>
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
	import AudioTime from './AudioTime';
	export default {
		components: {
			PrevButton,
			PlayButton,
			NextButton,
			VolumeBar,
			MuteButton,
			ProgressBar,
			AudioTime
		}
	}
</script>

<style scoped>
	.progress-bar,
	.control-buttons,
	.audio-time,
	.mute,
	.volume {
		float: left;
	}

	.audio-control {
		box-sizing: border-box;
	}

	.control-progress {
		box-sizing: border-box;
		padding: 0 246px 0 145px;
	}

	.control-volume {
		float: right;
	}
	
	.control-progress:after,
	.control-volume:after {
		content: '';
		display: block;
		height: 0;
		clear: both;
	}
	
	.control-buttons {
		width: 133px;
		margin: 0 6px;
	}
	.progress-bar {
		margin: 21px 6px;
	}
	
	.audio-time {
		margin: 16px 6px;
	}
	
	.mute {
		margin: 10px 6px;
	}
	
	.volume {
		margin: 21px 6px 21px 0;
	}
</style>