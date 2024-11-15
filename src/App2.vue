<script>
export default {
	data() {
		return {
			name: "Sapri",
			status: "active",
			tasks: ["Task 1", "Task 2", "Task 3"],
			link: "https://google.com",
		};
	},
	methods: {
		toggleStatus() {
			this.status = this.status === "active" ? "pending" : "active";
		},
	},
};
</script>

<template>
	<h1>{{ name }}</h1>
	<h1 v-if="status == 'active'">User is Active</h1>
	<h1 v-else-if="status == 'pending'">User is Pending</h1>
	<h1 v-else>User is Not Active</h1>

	<h3>Tasks:</h3>
	<ul>
		<li
			v-for="task in tasks"
			:key="task">
			{{ task }}
		</li>
	</ul>

	<!-- <a v-bind:href="link">Click for go Google</a> -->
	<a :href="link">Click for go Google</a>

	<!-- <button v-on:click="toggleStatus">Change Status</button> -->
	<button @click="toggleStatus">Change Status</button>
</template>
