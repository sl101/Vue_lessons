<template>
	<h2>Список постов</h2>
	<ul>
		<PostItem v-for="post in posts" :post="post" @remove="$emit('remove', post)" :key="post.id" />
	</ul>
</template>

<script>
import PostItem from './PostItem.vue';

export default {
	components: { PostItem },
	props: {
		posts: {
			type: Array,
			required: true
		},
	}
}
</script>

<style lang="scss" scoped></style>