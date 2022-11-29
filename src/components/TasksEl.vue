<script setup>
import Task from "./Task.vue";

defineProps({
	tasks: {
		type: Array,
		required: true,
	},
});
</script>
<template>
	<div class="flex flex-col gap-3 pt-5">
		<div v-for="task in tasks" :key="task.id">
			<Task
				@toggle-reminder="$emit('toggle-reminder', task.id)"
				@delete-task="$emit('delete-task', task.id)"
				:task="task"
			/>
		</div>
	</div>
</template>
