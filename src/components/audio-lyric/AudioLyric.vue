<template>
	<div>{{lyric}}</div>
</template>

<script>
	import request from 'superagent'
	export default {
		props: {
			songId: Number
		},
		data() {
			return {
				lyric: ''
			}
		},
		watch: {
			// computed 好像不支持异步
			songId(val) {
				request
				.get(`http://localhost:3000/lyric/${val}`)
				.end((err, res) => {
					this.lyric = res.body.lrc.lyric
				})
			}
		}
	}
</script>