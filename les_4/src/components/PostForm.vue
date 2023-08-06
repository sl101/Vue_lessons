<template>
	<form class="form" @submit.prevent>
		<h2>Создание поста</h2>
		<CustomInput v-model="post.title" type="text" placeholder="Название" />
		<CustomInput v-model="post.body" type="text" placeholder="Описание" />
		<CustomButton @click="createPost"> Создать пост</CustomButton>
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
	},
}
</script>

<style  scoped>
.form {
	display: flex;
	gap: 20px;
	flex-direction: column;
	justify-content: space-between;

}
</style>