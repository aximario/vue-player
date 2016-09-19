<template>
	<div>
		<audio-list-item v-for="item in list" :song="item" v-on:select-song="selectSong"></audio-list-item>
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
				list: [{
					id: 0,
					name: 'Fade',
					src: 'http://o94al90ev.bkt.clouddn.com/songs/Alan%20Walker%20-%20Fade.mp3'
				}, {
					id: 1,
					name: '君が好きだと叫びたい.',
					src: 'http://o94al90ev.bkt.clouddn.com/songs/BAAD%20-%20%E5%90%9B%E3%81%8B%E3%82%99%E5%A5%BD%E3%81%8D%E3%81%9F%E3%82%99%E3%81%A8%E5%8F%AB%E3%81%B2%E3%82%99%E3%81%9F%E3%81%84.mp3'
				}, {
					id: 2,
					name: '不说再见',
					src: 'http://o94al90ev.bkt.clouddn.com/songs/%E5%A5%BD%E5%A6%B9%E5%A6%B9%E4%B9%90%E9%98%9F%20-%20%E4%B8%8D%E8%AF%B4%E5%86%8D%E8%A7%81.mp3'
				}, {
					id: 3,
					name: 'Butterfly',
					src: 'http://o94al90ev.bkt.clouddn.com/songs/One%20Direction%20-%20What%20Makes%20You%20Beautiful.mp3'
				}, {
					id: 4,
					name: 'What Makes You Beautiful',
					src: 'http://o94al90ev.bkt.clouddn.com/songs/One%20Direction%20-%20What%20Makes%20You%20Beautiful.mp3'
				}, {
					id: 5,
					name: '给未来的自己',
					src: 'http://o94al90ev.bkt.clouddn.com/songs/%E6%9D%A8%E5%AE%97%E7%BA%AC%20-%20%E7%BB%99%E6%9C%AA%E6%9D%A5%E7%9A%84%E8%87%AA%E5%B7%B1%28Live%29%20-%20live.mp3'
				}, {
					id: 6,
					name: 'U Make Me Wanna',
					src: 'http://o94al90ev.bkt.clouddn.com/songs/Blue%20-%20U%20Make%20Me%20Wanna.mp3'
				}]
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
		}
	}
</script>

<style scoped>

</style>