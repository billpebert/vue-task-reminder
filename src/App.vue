<script setup>
import FooterElVue from "./components/FooterEl.vue";
</script>

<template>
	<div class="container-wrapper">
		<router-view></router-view>
		<FooterElVue />
	</div>
</template>

<style>
* {
	box-sizing: border-box;
	margin: 0;
	padding: 0;
}

.container-wrapper {
	max-width: 500px;
	width: 100%;
	margin: 30px auto;
	overflow: auto;
	min-height: 300px;
	border: 4px solid #2a9d8f;
	border-radius: 24px;
	padding: 30px;
}
</style>
