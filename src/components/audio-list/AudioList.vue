<template>
	<div>
		<audio-list-item v-for="item in list" :current="current" :song="item" v-on:select-song="selectSong"></audio-list-item>
	</div>
</template>

<script>
	import AudioListItem from './AudioListItem';
	import request from 'superagent';
	export default {
		components: {
			AudioListItem
		},
		data() {
			return {
				current: null,
				list: null
			}
		},
		methods: {
			selectSong(current) {
				this.current = current;
				this.$dispatch('change-song', this.current);
			}
		},
		events: {
			'list-next': function() {
				let currentIndex = this.list.indexOf(this.current);
				let nextIndex = (currentIndex + 1) % this.list.length;
				this.current = this.list[nextIndex];
				this.$dispatch('change-song', this.current);
			},
			'list-prev': function() {
				let currentIndex = this.list.indexOf(this.current);
				let prevIndex = (currentIndex + this.list.length - 1) % this.list.length;
				this.current = this.list[prevIndex];
				this.$dispatch('change-song', this.current);
			}
		},
		ready() {
			let that = this;
			request
				.get('http://localhost:3000/list/461712793')
				// .get('/list')
				.end((err, res) => {
					that.list = res.body.result.tracks;
					this.current = this.list[0];
					this.$dispatch('init-song', this.current);
				});
		}
	}
</script>

<style scoped>
	div {
		max-height: 600px;
		overflow: auto;
	}
</style>