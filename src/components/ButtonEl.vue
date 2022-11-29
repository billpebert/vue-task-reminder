<script setup>
defineProps({
	title: {
		type: String,
		required: true,
		default: "black",
	},
	className: {
		type: String,
		required: false,
		default: "btn-black",
	},
});
</script>

<template>
	<button :class="`btn ${className}`">{{ title }}</button>
</template>

<style scoped>
.btn {
	display: inline-block;
	border: none;
	padding: 10px 20px;
	margin: 5px;
	border-radius: 6px;
	cursor: pointer;
	text-decoration: none;
	font-size: 16px;
	font-family: inherit;
	font-weight: 600;
}

.btn-black {
	background-color: #252525;
	color: #f8f9fa;
}
.btn-success {
	background-color: #2a9d8f;
	color: #f8f9fa;
}

.btn-secondary {
	background-color: #f2e8cf;
	color: #212529;
}

.btn:focus {
	outline: none;
}

.btn:active {
	transform: scale(0.98);
}

.btn-block {
	display: block;
	width: 100%;
}
</style>
