<template>
    <div class="bar">
        <div v-el:dot class="dot" @mousedown="handleDown"></div>
    </div>
</template>

<style scoped>
	.bar {
		position: relative;
		width: 100px;
		height: 4px;
		background-color: rgba(255, 255, 255, .1);
	}
	
	.dot {
		position: absolute;
		left: 95px;
		top: -3px;
		width: 10px;
		height: 10px;
		border-radius: 50%;
		background-color: #ffffe6;
		cursor: pointer;
	}
</style>

<script>
	export default {
		props: {
			audio: null
		},
		methods: {
			handleDown: function(e) {
				let ele = this.$els.dot,
					startX = e.clientX + window.pageXOffset,
					origX = ele.offsetLeft,
					deltaX = startX - origX;

				let handleMove = e => {
					let newLeft = e.clientX + window.pageXOffset - deltaX;
					if (newLeft < -5) {
						this.audio.volume = 0
					} else if (newLeft > 95) {
						this.audio.volume = 1
					} else {
						this.audio.volume = (newLeft + 5) / 100
						ele.style.left = newLeft + 'px';
					}
					e.stopPropagation()
				}

				let handleUp = e => {
					document.removeEventListener('mousemove', handleMove, true)
					document.removeEventListener('mouseup', handleUp, true)
					e.stopPropagation()
				}

				document.addEventListener('mousemove', handleMove, true)
				document.addEventListener('mouseup', handleUp, true)
				e.stopPropagation()
				e.preventDefault()
			}
		}
	}
</script>