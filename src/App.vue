<script setup>
import HeaderSection from "./components/HeaderSection.vue";
import ButtonEl from "./components/ButtonEl.vue";
</script>

<template>
	<div class="container">
		<HeaderSection title="Task Tracker">
			<ButtonEl title="Add" className="btn-success" />
		</HeaderSection>
	</div>
</template>

<script>
export default {
	data() {
		return {
			tasks: [],
		};
	},

	created() {
		this.tasks = [
			{
				id: 1,
				text: "Doctor Appointment",
				day: "March 1st at 2:30pm",
				reminder: true,
			},
			{
				id: 2,
				text: "Meeting at School",
				day: "March 3st at 4:00pm",
				reminder: true,
			},
			{
				id: 3,
				text: "Food Shopping",
				day: "March 13st at 4:00pm",
				reminder: false,
			},
		];
	},
};
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Poppins:ital,wght@0,400;0,500;0,600;0,700;1,300&display=swap");

* {
	box-sizing: border-box;
	margin: 0;
	padding: 0;
}

body {
	font-family: "Poppins", sans-serif;
}

.container {
	max-width: 500px;
	width: 100%;
	margin: 30px auto;
	overflow: auto;
	min-height: 300px;
	border: 1px solid steelblue;
	border-radius: 6px;
	padding: 30px;
}
</style>
