<template>
    <div class="bar">
        <div v-volume class="dot"></div>
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
		data() {
			return {
				volume: undefined
			}
		},
		directives: {

			volume: {
				bind: function() {
					let audio = this.vm.audio,
						ele = this.el;
					this.vm.volume = 0.6;
					ele.style.left = (this.vm.volume * 100 - 5) + 'px';
					audio.addEventListener('volumechange', e => {
						this.vm.volume = audio.volume;
					}, false);
					let handleDown = function(e) {
						let startX = e.clientX + window.pageXOffset,
							origX = ele.offsetLeft,
							deltaX = startX - origX;
						let handleMove = e => {
							let newLeft = e.clientX + window.pageXOffset - deltaX;
							if (newLeft < -5) {
								audio.volume = 0
							} else if (newLeft > 95) {
								audio.volume = 1
							} else {
								audio.volume = (newLeft + 5) / 100
							}
							ele.style.left = (audio.volume * 100 - 5) + 'px';
							e.stopPropagation()
						}
						let handleUp = e => {
							document.removeEventListener('mousemove', handleMove, true)
							document.removeEventListener('mouseup', handleUp, true);
							document.removeEventListener('mouseup', handleDown, true);
							e.stopPropagation()
						}
						document.addEventListener('mousemove', handleMove, true)
						document.addEventListener('mouseup', handleUp, true)
						e.stopPropagation()
						e.preventDefault()
					};
					ele.addEventListener('mousedown', handleDown, false);
				}
			}
		}
	}
</script>