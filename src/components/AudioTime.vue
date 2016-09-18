<template>
	<div>
		{{time}}
	</div>
</template>

<script>
	export default {
		data() {
			return {
				time: '00:00 / 00:00'
			}
		},
		methods: {
			timeFormat(seconds) {
				if(typeof seconds !== 'number') {
					return '00:00'
				}else {
					let raw = Math.round(seconds);
					let sec = raw % 60;
					let min = (raw - sec) / 60;
					return (min < 10 ? '0' + min : min) + ':' + (sec < 10 ? '0' + sec : sec);
				}
			}
		},
		events: {
			'audio-time-update': function(obj) {
				this.time = this.timeFormat(obj.currentTime) + ' / ' + this.timeFormat(obj.duration);
			},
			'audio-loaded-metadata': function(duration) {
				this.time = '00:00 / ' + this.timeFormat(duration);
			}
		}
	}
</script>

<style>
	div {
		color: #eee;
	}
</style>