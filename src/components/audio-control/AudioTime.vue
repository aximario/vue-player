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

				// 当没有取到歌曲duration，或者不是number类型时返回00：00
				if (!seconds || typeof seconds !== 'number') {
					return '00:00'
				} else {
					let raw = Math.round(seconds);
					let sec = raw % 60;
					let min = (raw - sec) / 60;
					
					// 默认歌曲最大时长不会超过 59:59
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

<style scoped>
	div {
		width: 76px;
		font-size: 13px;
		color: rgba(255, 255, 255, .5);
	}
</style>