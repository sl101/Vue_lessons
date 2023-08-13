<template>
	<div class="container">
		<div class="app">
			<h1>Страница с постами</h1>
			<CustomInput class="search" v-model="searchQuery" placeholder="search" />
			<div class="app_top">
				<CustomButton @click="showDialog">Создать пост</CustomButton>
				<CustomSelect v-model="selectedSort" :options="options" />
			</div>
			<CustomDialog v-model:show="dialogVisible">
				<PostForm @create="addPost" />
			</CustomDialog>

			<PostList :posts="sortAndSearchPostByTitle" @remove="removePost" v-if="!isPostsLoading" />
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
			isPostsLoading: false,
			selectedSort: '',
			searchQuery: '',
			options: [
				{ id: 1, value: 'title', name: "По наименованию" },
				{ id: 2, value: 'body', name: "По описанию" }
			]
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
				const response = await axios.get('https://jsonplaceholder.typicode.com/posts?_limit=10');
				this.posts = response.data;
			} catch (error) {
				alert("Ошибка!")
			} finally {
				this.isPostsLoading = false;
			}
		},
	},
	mounted() {
		this.fetchPosts();
	},
	//watch: {
	//	selectedSort(newValue) {
	//this.posts.sort((post1, post2) => {
	//return post1[newValue]?.localeCompare(post2[newValue]);
	//})
	//	}
	//},
	computed: {
		sortedPosts() {
			return [...this.posts].sort((post1, post2) => post1[this.selectedSort]?.localeCompare(post2[this.selectedSort]))
		},
		sortAndSearchPostByTitle() {
			return this.sortedPosts.filter(post => post.title.toLowerCase().includes(this.searchQuery.toLowerCase()))
		}
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

.search {
	margin-top: 20px;
	max-width: 500px;
	width: 100%;
}

.app_top {
	margin: 20px 0;
	display: flex;
	justify-content: space-between;
	align-items: center;
	gap: 50px;
}
</style>