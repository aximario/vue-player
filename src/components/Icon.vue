<template>
<i>{{{icon}}}</i>
</template>

<script>
export default {
	props: {
		icon: String
	}
}
</script>

<style scoped>
@font-face {
	font-family: 'iconfont';
	src: url('//at.alicdn.com/t/font_1473589104_234917.eot');
	/* IE9*/
	src: url('//at.alicdn.com/t/font_1473589104_234917.eot?#iefix') format('embedded-opentype'), /* IE6-IE8 */
	url('//at.alicdn.com/t/font_1473589104_234917.woff') format('woff'), /* chrome、firefox */
	url('//at.alicdn.com/t/font_1473589104_234917.ttf') format('truetype'), /* chrome、firefox、opera、Safari, Android, iOS 4.2+*/
	url('//at.alicdn.com/t/font_1473589104_234917.svg#iconfont') format('svg');
	/* iOS 4.1- */
}

i {
	font-family: "iconfont";
	font-size: 16px;
	font-style: normal;
}
</style>
