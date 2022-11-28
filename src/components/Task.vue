<script setup>
defineProps({
	task: {
		type: Object,
		required: true,
	},
});
</script>

<template>
	<div
		@dblclick="$emit('toggle-reminder', task.id)"
		:class="[
			task.reminder ? 'border-l-4 border-solid border-[#2a9d8f]' : '',
			'p-3 bg-[#f4f4f4] rounded-md flex items-center justify-between',
		]"
	>
		<div class="flex flex-col gap-2">
			<h3 class="text-lg text-slate-800 font-medium">{{ task.text }}</h3>
			<p class="text-base text-slate-600">{{ task.day }}</p>
		</div>
		<span class="p-3 cursor-pointer" @click="onDelete(task.id)">
			<i class="fas fa-times text-slate-500"></i>
		</span>
	</div>
</template>

<script>
export default {
	methods: {
		onDelete(id) {
			this.$emit("delete-task", id);
		},
	},
};
</script>
