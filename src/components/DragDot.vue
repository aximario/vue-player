<template>
	<div></div>
</template>

<style scoped>
	div {
		width: 10px;
		height: 10px;
		border-radius: 50%;
		background-color: #eee;
		cursor: pointer;
		position: absolute;
	}
</style>

<script>
	export default {
		props: {

			// 偏移量 单位：px
			offset: Number,

			// 总长度（最大偏移量） 单位：px
			length: Number
		},
		ready() {
			let dragEle = this.$el,
				that = this;

			// 初始化偏移量
			dragEle.style.left = this.offset - 5 + 'px';

			// 拖动事件
			let handleDown = function(e) {
				let startX = e.clientX + window.pageXOffset,
					origX = dragEle.offsetLeft,
					deltaX = startX - origX,
					len = that.length - 5;
				let handleMove = e => {
					let ofs = e.clientX + window.pageXOffset - deltaX;
					if (ofs <= len && ofs >= -5) {
						that.offset = ofs + 5;

						// 触发派发事件，向父链通知偏移量（offset）的改变
						that.$dispatch('drag', that.offset);
						
						dragEle.style.left = ofs + 'px';
					}
					e.stopPropagation()
				};
				let handleUp = e => {
					document.removeEventListener('mousemove', handleMove, true);
					document.removeEventListener('mouseup', handleUp, true);
					e.stopPropagation();
				};
				document.addEventListener('mousemove', handleMove, true);
				document.addEventListener('mouseup', handleUp, true);
				e.stopPropagation();
				e.preventDefault();
			};
			dragEle.addEventListener('mousedown', handleDown, false);
		}
	}
</script>