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
		async addTask(task) {
			const res = await fetch("http://localhost:8989/tasks", {
				method: "POST",
				headers: {
					"Content-type": "application/json",
				},
				body: JSON.stringify(task),
			});

			const data = await res.json();

			// this.tasks = [...this.tasks, task];
			this.tasks = [...this.tasks, data];
		},
		async deleteTask(id) {
			if (confirm("Are you sure?")) {
				const res = await fetch(`http://localhost:8989/tasks/${id}`, {
					method: "DELETE",
				});

				res.status === 200
					? (this.tasks = this.tasks.filter((task) => task.id !== id))
					: alert("Error deleting task");
			}
		},
		async toggleReminder(id) {
			const taskToToggle = await this.fetchTask(id);

			const updateTask = { ...taskToToggle, reminder: !taskToToggle.reminder };

			const res = await fetch(`http://localhost:8989/tasks/${id}`, {
				method: "PUT",
				headers: {
					"Content-type": "application/json",
				},
				body: JSON.stringify(updateTask),
			});

			const data = await res.json();

			// const markTask = this.tasks.map((task) => (task.id === id ? { ...task, reminder: !task.reminder } : task));
			const markTask = this.tasks.map((task) => (task.id === id ? { ...task, reminder: data.reminder } : task));
			this.tasks = markTask;
		},
		toggleForm() {
			this.showAddTask = !this.showAddTask;
		},
		async fetchTasks() {
			const res = await fetch("http://localhost:8989/tasks");
			// const res = await fetch("api/tasks");
			const data = await res.json();
			return data;
		},
		async fetchTask(id) {
			// const res = await fetch(`api/task/${id}`);
			const res = await fetch(`http://localhost:8989/tasks/${id}`);
			const data = await res.json();
			return data;
		},
	},

	async created() {
		this.tasks = await this.fetchTasks();
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
