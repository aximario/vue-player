<template>
	<ol>
		<li v-for="line in lyric">{{line.value}}</li>
	</ol>
</template>

<script>
	import request from 'superagent'
	export default {
		props: {
			songId: Number
		},
		data() {
			return {
				lyric: []
			}
		},
		methods: {
			parseLyric(lrcString) {
				const PATTERN = /^\[(.*)\](.*)/
				let parsed = []
				let raw = lrcString.split('\n')
				for (let i = 0; i < raw.length - 1; i++) {
					let kv = PATTERN.exec(raw[i])
					if (kv[2]) {
						parsed.push({
							key: kv[1],
							value: kv[2]
						})
					} else {
						let tag = kv[1].split(':')
						if (tag.length > 2) {
							parsed.push({
								key: kv[1],
								value: ' '
							})
						} else {
							parsed.push({
								key: tag[0],
								value: tag[1]
							})
						}
					}
				}
				return parsed
			}
		},
		watch: {
			// computed 好像不支持异步
			songId(val) {
				request
					.get(`http://localhost:3000/lyric/${val}`)
					.end((err, res) => {
						this.lyric = this.parseLyric(res.body.lrc.lyric)
					})
			}
		}
	}
</script>