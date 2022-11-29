<template>
	<form @submit="onSubmit" class="flex flex-col gap-5 pb-5 border-b-2 border-b-slate-200">
		<div class="flex flex-col gap-2">
			<label for="" class="text-base text-slate-600 font-medium">Task</label>
			<input
				type="text"
				name="text"
				class="text-base text-slate-600 font-medium border border-slate-400 p-3 rounded-lg"
				placeholder="Add Task"
				v-model="text"
			/>
		</div>
		<div class="flex flex-col gap-2">
			<label for="" class="text-base text-slate-600 font-medium">Date Time</label>
			<input
				type="text"
				name="day"
				class="text-base text-slate-600 font-medium border border-slate-400 p-3 rounded-lg"
				placeholder="Add Date Time"
				v-model="day"
			/>
		</div>
		<div class="flex gap-2 items-center">
			<label for="" class="text-base text-slate-600 font-medium">Set Reminder</label>
			<input type="checkbox" name="reminder" v-model="reminder" />
		</div>

		<input
			type="submit"
			value="Save Task"
			class="bg-[#2a9d8f] py-3 px-6 font-semibold text-white rounded-lg hover:bg-[#24887d] transition-all cursor-pointer"
		/>
	</form>
</template>

<script>
export default {
	data() {
		return {
			text: "",
			day: "",
			reminder: false,
		};
	},

	methods: {
		onSubmit(e) {
			e.preventDefault();

			if (!this.text) {
				alert("Please add a task");
				return;
			}

			const newTask = {
				// id: Math.floor(Math.random() * 10000),
				text: this.text,
				day: this.day,
				reminder: this.reminder,
			};

			this.text = "";
			this.day = "";
			this.reminder = false;

			this.$emit("add-task", newTask);
		},
	},
};
</script>
