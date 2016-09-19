<template>
	<div></div>
</template>

<style scoped>
	div {
		position: absolute;
		height: 4px;
		border-radius: 2px;
	}
</style>

<script>
	export default {
		props: {

			// 百分比 0-1
			percent: Number

		},
		watch: {
			'percent': function(val) {
				this.$el.style.width = val * 100 + '%';
			}
		},
		ready() {
			this.$el.style.width = this.percent * 100 + 'px';
		}
	}
</script>