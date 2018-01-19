<template>
	<div v-show="preloader">
		<img src="../../assets/preloader.gif" class="preloader">
	</div>
</template>

<script>
export default {
	props: {
		preloader: {
			required: true,
			type: Boolean,
			default: false,
		}
	}
}
</script>

<style scoped>
	img.preloader{max-width: 60px;}
</style>
