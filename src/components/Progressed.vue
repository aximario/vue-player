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
			percent: Number,

			// 总长度 单位：px
			length: Number
		},
		computed: {
			width() {
				return this.percent * this.length;
			}
		},
		watch: {
			'width': function(val) {
				this.$el.style.width = val + 'px';
			}
		},
		ready() {
			this.$el.style.width = this.width + 'px';
		}
	}
</script>