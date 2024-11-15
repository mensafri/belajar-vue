<script setup>
import { ref, onMounted } from "vue";

const name = ref("Sapri");
const status = ref("active");
const tasks = ref(["Task 1", "Task 2", "Task 3"]);
const newTask = ref("");

const toggleStatus = () => {
	status.value = status.value === "active" ? "pending" : "active";
};

const addTask = () => {
	if (newTask.value !== "") {
		tasks.value.push(newTask.value);
		newTask.value = "";
	}
};

const deleteTask = (index) => {
	tasks.value.splice(index, 1);
};

onMounted(async () => {
	try {
		const response = await fetch("https://jsonplaceholder.typicode.com/todos");
		const data = await response.json();

		tasks.value = data.map((task) => task.title);
	} catch (error) {
		console.log(error);
	}
});
</script>

<template>
	<h1>{{ name }}</h1>
	<h1 v-if="status == 'active'">User is Active</h1>
	<h1 v-else-if="status == 'pending'">User is Pending</h1>
	<h1 v-else>User is Not Active</h1>

	<form @submit.prevent="addTask">
		<label for="newTask">Add Task</label>
		<input
			type="text"
			id="newTask"
			name="newTask"
			v-model="newTask"
			placeholder="Add Task" />
		<button type="submit">Add Task</button>
	</form>

	<h3>Tasks:</h3>
	<ul>
		<li
			v-for="(task, index) in tasks"
			:key="task">
			<span>
				{{ task }}
			</span>
			<button @click="deleteTask(index)">Delete</button>
		</li>
	</ul>

	<!-- <a v-bind:href="link">Click for go Google</a> -->
	<!-- <a :href="link">Click for go Google</a> -->

	<!-- <button v-on:click="toggleStatus">Change Status</button> -->
	<button @click="toggleStatus">Change Status</button>
</template>
