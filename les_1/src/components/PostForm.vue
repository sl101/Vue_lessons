<template>
	<form @submit.prevent>
		<h4 class="title">Создать пост</h4>
		<input class="input" v-model="post.title" type="text" placeholder="Название">
		<input class="input" v-model="post.body" type="text" placeholder="Описание">
		<button class="button" type="submit" @click="createPost">
			Добавить пост
		</button>
	</form>
</template>

<script>
export default {
	data() {
		return {
			post: {
				title: '',
				body: ''
			}
		}
	},
	methods: {
		createPost() {
			this.post.id = Date.now();
			this.$emit('create', this.post);
			this.post = {
				title: '',
				body: ''
			}
		}
	}
}
</script>

<style scoped>
.button,
.input {
	display: block;
	padding: 10px 15px;
	margin-top: 15px;
	width: 50%;
	border: 2px solid teal;
}

.button {
	width: 200px;
	background-color: transparent;
	font-weight: 600;
	cursor: pointer;
}
</style>