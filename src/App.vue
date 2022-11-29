<script setup>
import HeaderSection from "./components/HeaderSection.vue";
import ButtonEl from "./components/ButtonEl.vue";
import TasksElVue from "./components/TasksEl.vue";
import AddTaskVue from "./components/AddTask.vue";
</script>

<template>
	<div class="container-wrapper">
		<HeaderSection title="Task Tracker">
			<ButtonEl
				:title="showAddTask ? 'Close Form' : 'Add Task'"
				:className="showAddTask ? 'btn-black' : 'btn-success'"
				@click="toggleForm"
			/>
		</HeaderSection>
		<div v-show="showAddTask">
			<AddTaskVue @add-task="addTask" />
		</div>
		<TasksElVue @toggle-reminder="toggleReminder" @delete-task="deleteTask" :tasks="tasks" />
	</div>
</template>

<script>
export default {
	data() {
		return {
			tasks: [],
			showAddTask: false,
		};
	},

	methods: {
		addTask(task) {
			this.tasks = [...this.tasks, task];
		},
		deleteTask(id) {
			this.tasks = this.tasks.filter((task) => task.id !== id);
		},
		toggleReminder(id) {
			const markTask = this.tasks.map((task) => (task.id === id ? { ...task, reminder: !task.reminder } : task));
			this.tasks = markTask;
		},
		toggleForm() {
			this.showAddTask = !this.showAddTask;
		},
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
	border: 1px solid steelblue;
	border-radius: 6px;
	padding: 30px;
}
</style>
