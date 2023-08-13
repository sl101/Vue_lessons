<template>
	<section>
		<h2 class="posts">Список постов:</h2>
		<ul class="posts_list" v-if="posts.length > 0">
			<PostItem v-for="post in posts" :key="post.id" :post="post" @remove="this.$emit('remove', post)" />
		</ul>
		<div class="empty_message" v-else>
			<p>список пуст</p>
		</div>
	</section>
</template>

<script>
import PostItem from './PostItem.vue';

export default {
	components: { PostItem },
	props: {
		posts: {
			type: Array,
			required: true
		}
	},
}
</script>

<style scoped>
.posts_list {
	margin-top: 25px;
	display: flex;
	flex-direction: column;
	gap: 20px;
}

.empty_message {
	color: var(--error);
}
</style>