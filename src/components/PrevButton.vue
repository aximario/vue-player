<template>
	<button>
		<icon class="icon" icon="&#xe600;" @click="handleClick"></icon>
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
				this.$dispatch('prev-song');
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