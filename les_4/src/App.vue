<template>
	<div class="container">
		<div class="wrapper">
			<PostForm @create="createPost" />
			<PostList :posts="posts" @remove="removePost" />
		</div>
	</div>
</template>

<script>
import PostForm from '@/components/PostForm.vue';
import PostList from '@/components/PostList.vue'
export default {
	components: {
		PostForm, PostList
	},
	data() {
		return {
			posts: [
				{ id: 1, title: "Post 1", body: "some body 1" },
				{ id: 2, title: "Post 2", body: "some body 2" },
				{ id: 3, title: "Post 3", body: "some body 3" },
			]
		}
	},
	methods: {
		createPost(post) {
			this.posts.unshift(post)
		},
		removePost(post) {
			this.posts = this.posts.filter(elem => elem.id !== post.id)
		}
	}

}
</script>

<style >
* {
	margin: 0;
	padding: 0;
	box-sizing: border-box;

	--white: #fff;
	--black: #000;
	--teal: teal;
	--red: red;

	--transition: .4s ease-in-out;
}

.wrapper {
	padding: 20px;
}

.title {
	margin-top: 15px;
}
</style>