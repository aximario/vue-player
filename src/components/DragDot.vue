// 可拖动点
// 在被拖动的时候会 dispatch 'drag' 事件
// 向父链通知当前的偏移量
// 可以在父链捕获到相应的偏移量改变并做处理

<template>
	<div></div>
</template>

<style scoped>
	div {
		position: absolute;

		width: 10px;
		height: 10px;

		border-radius: 50%;
		background-color: #eee;

		cursor: pointer;
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
		events: {

			// 监听update-offset事件，更新偏移量
			'update-offset': function(offset){
				this.offset = offset;
				this.$el.style.left = offset - 5 + 'px';
			}
		},

		// 初始化，绑定事件
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

						// 触发dispatch事件，向父链通知偏移量（offset）的改变
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