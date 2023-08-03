<template>
	<form class="form" @submit.prevent>
		<h2 class="title">Create user</h2>
		<CustomInput type="text" v-model="post.title" placeholder="Title" />
		<CustomInput type="text" v-model="post.body" placeholder="Summary" />
		<CustomButton @click="createPost" text="Add user" />
	</form>
</template>

<script>
export default {
	data() {
		return {
			post: {
				title: '',
				body: ''
			},
			btn: "Send",
		}
	},
	methods: {
		createPost() {
			if (this.post.title && this.post.body) {

				this.post.id = Date.now();
				this.$emit('create', this.post);
				this.post = {
					title: '',
					body: '',
				}
			}
		}
	}
}
</script>

<style>
.form {
	margin-top: 20px;
	max-width: 300px;
	display: flex;
	flex-direction: column;
	gap: 20px;
}
</style>