<template>
	<div class="container">
		<div class="app">
			<h1>Страница с постами</h1>
			<!--<CustomButton @click="fetchPosts" style="margin: 20px 0;">Get Posts</CustomButton>-->
			<CustomButton @click="showDialog" style="margin: 20px 0;">Создать пост</CustomButton>

			<CustomDialog v-model:show="dialogVisible">
				<PostForm @create="addPost" />
			</CustomDialog>

			<PostList :posts="posts" @remove="removePost" v-if="!isPostsLoading" />
			<div v-else>Идет загрузка...</div>
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
			dialogVisible: false,
			isPostsLoading: false
		}
	},
	methods: {
		addPost(newPost) {
			this.posts.unshift(newPost);
			this.dialogVisible = false
		},
		removePost(post) {
			this.posts = this.posts.filter(elem => elem.id !== post.id);
		},
		showDialog() {
			this.dialogVisible = true
		},
		async fetchPosts() {
			try {
				this.isPostsLoading = true;
				//setTimeout(async () => {
				const response = await axios.get('https://jsonplaceholder.typicode.com/posts?_limit=10');
				//console.log(response.data);
				this.posts = response.data;
				//this.isPostsLoading = false;
				//}, 1000)
			} catch (error) {
				alert("Ошибка!")
			} finally {
				this.isPostsLoading = false;
			}
		},
	},
	mounted() {
		this.fetchPosts();
	}
}
</script>

<style >
.container {
	max-width: 1430px;
	width: 100%;
	padding: 0 15px;
	margin: 0 auto;
}

.app {
	padding: 50px 0;
}
</style>