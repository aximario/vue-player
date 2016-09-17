<template>
	<div></div>
</template>

<style scoped>
	div {
		position: absolute;

		height: 4px;
		background-color: lightblue;
	}
</style>

<script>
	export default {
		props: {

			// 进度的长度 单位：px
			length: Number
		},
		events: {
			progress(length){
				this.length = length;
				this.$el.style.width = length + 'px';
			}
		},
		ready() {
			this.$el.style.width = this.length + 'px';
		}
	}
</script>