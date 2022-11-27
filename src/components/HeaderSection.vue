<script setup>
defineProps({
	title: {
		type: String,
		required: true,
	},
});
</script>
<template>
	<header>
		<h1>{{ title }}</h1>
		<slot></slot>
	</header>
</template>

<style scoped>
header {
	display: flex;
	align-items: center;
	justify-content: space-between;
	gap: 48px;
	margin-bottom: 20px;
}
</style>
