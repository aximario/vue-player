<template>
	<button>
		<icon class="icon" icon="&#xe601;" @click="handleClick"></icon>
	</button>
</template>

<script>
	import Icon from './Icon';
	export default {
		components: {
			Icon
		},
		methods: {
			handleClick(e) {
				e.stopPropagation();
				this.$dispatch('next-song');
			}
		}
	}
</script>

<style scoped>
	.icon {
		font-size: 26px;
		color: rgba(255, 255, 255, .85);
	}
	
	button {
		border: none;
		margin: 6px 0;
		vertical-align: top;
		background-color: transparent;
		outline: none;
		cursor: pointer;
	}
</style>