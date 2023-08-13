<template>
	<form class="form" @submit.prevent>
		<h2>Добавить Пост</h2>
		<div class="form__content">
			<CustomInput v-model="post.title" type="text" placeholder="Наименование: " />
			<CustomInput v-model="post.body" type="text" placeholder="Описание: " />
			<CustomButton @click="createPost" style="align-self: end;">Добавить</CustomButton>
		</div>
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

<style scoped>
.form__content {
	margin-top: 20px;
	min-width: 400px;
	display: flex;
	flex-direction: column;
	gap: 20px;
}
</style>