<template>
	<ol>
		<li v-for="album in albums">{{ album.name }}</li>
	</ol>
</template>

<script>
	import request from 'superagent';
	export default {
		data() {
			albums: []
		},
		ready() {
			request
				.get('http://localhost:3000/albums')
				.end((err, res) => {
					console.log(res.body);
				});
		}
	}
</script>