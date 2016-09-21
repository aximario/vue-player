// 可拖动点 // 在被拖动的时候会 dispatch 'drag' 事件 // 向父链通知当前的偏移量 // 可以在父链捕获到相应的偏移量改变并做处理

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

			// 百分比 0-1
			percent: Number

		},
		watch: {
			percent(val) {
				this.$el.style.left = `calc(${val*100}% - 5px)`;
			}
		},

		// 初始化，绑定事件
		ready() {
			let dragEle = this.$el,
				that = this;

			// 初始化偏移量
			dragEle.style.left = `calc(${this.percent*100}% - 5px)`;

			// 拖动事件
			let handleDown = function(e) {
				let startX = e.clientX + window.pageXOffset,
					origX = dragEle.offsetLeft,
					deltaX = startX - origX;
				let handleMove = e => {
					let ofs = e.clientX + window.pageXOffset - deltaX;

					// 触发dispatch事件，向父链通知偏移量（offset）的改变
					that.$dispatch('drag', ofs + 5);

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