<template>
	<div class="app">
		<PostForm @create="createPost" />
		<PostList :posts="posts" />
	</div>
</template>

<script>
import PostForm from '@/components/PostForm.vue';
import PostList from '@/components/PostList.vue';
export default {
	components: {
		PostForm, PostList
	},
	data() {
		return {
			posts: [
				{ id: 1, title: "Jav 1", body: "body text 1" },
				{ id: 2, title: "Jav 2", body: "body text 2" },
				{ id: 3, title: "Jav 3", body: "body text 3" }
			],

		}
	},
	methods: {
		createPost(post) {
			this.posts.unshift(post);
		},
	}
}
</script>

<style>
* {
	margin: 0;
	padding: 0;
	box-sizing: border-box;
}

ul,
li {
	list-style: none;
}

.app {
	padding: 30px;
}

.app * {
	border-radius: 5px;
}
</style>
