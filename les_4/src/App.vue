<template>
	<div class="app">
		<h1>Страница с постами</h1>
		<div class="app__top">
			<CustomButton @click="openDialog">Добавить пост</CustomButton>
			<!--<CustomSelect v-model:selectOption.sync="selectOption" :options="options" />-->
			<CustomSelect v-model="selectOption" :options="options" />
		</div>
		<div>
			<CustomDialog v-model:show="isDialogVisible">
				<PostForm @create="addPost" />
			</CustomDialog>
			<PostList :posts="posts" @remove="removePost" v-if="!isLoaded" />
			<p>Идет загрузка...</p>
		</div>
	</div>
</template>

<script>
import PostForm from '@/components/PostForm.vue';
import PostList from '@/components/PostList.vue';
import axios from 'axios'

export default {
	components: { PostForm, PostList },

	data() {
		return {
			posts: [],
			isDialogVisible: false,
			isLoaded: false,
			selectOption: '',
			options: [
				{ id: 1, value: 'title', name: 'По названию' },
				{ id: 2, value: 'body', name: 'По содержимому' }
			]
		};
	},
	methods: {
		addPost(newPost) {
			console.log("🚀 ~ file: App.vue:25 ~ addPost ~ newPost:", newPost)
			this.posts.unshift(newPost);
			this.isDialogVisible = false
		},
		openDialog() {
			this.isDialogVisible = true
		},
		removePost(post) {
			this.posts = this.posts.filter(elem => elem.id !== post.id)
		},
		async fetchPosts() {
			this.isLoaded = true;
			try {
				const response = await axios('https://jsonplaceholder.typicode.com/posts?_limit=10');
				this.posts = response.data;

			} catch (error) {
				alert("Ошибка")
			} finally {
				this.isLoaded = false;
			}
		},
	},
	mounted() {
		this.fetchPosts();
	}
}

</script>

<style>
.app {
	padding: 50px;
}

.app__top {
	margin: 20px 0;
	display: flex;
	justify-content: space-between;
	align-items: center;
	gap: 20px;
}
</style>