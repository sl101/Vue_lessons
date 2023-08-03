<template>
	<ul class="posts" v-if="posts.length > 0">
		<h2 class="title">Users list</h2>
		<PostItem v-for="post in posts" :post="post" :key="post.id" @remove="$emit('remove', post)" />
	</ul>
	<div v-else>
		<h2 class="title" style="color: var(--red)">Post list is empty</h2>
	</div>
</template>

<script>
import PostItem from '@/components/PostItem.vue';
export default {
	components: {
		PostItem
	},
	props: {
		posts: {
			type: Array,
			required: true,
		}
	}

}
</script>

<style >
.posts {
	margin-top: 30px;
	display: flex;
	flex-direction: column;
	gap: 25px;
}
</style>