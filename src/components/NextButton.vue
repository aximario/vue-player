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
		font-size: 36px;
		color: #cdcdcd;
	}
	
	button {
		border: none;
		background-color: transparent;
		outline: none;
	}
</style>