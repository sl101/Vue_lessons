<template>
	<div>
		<h3 class="title">Список пользователей</h3>
		<ul class="post__list">
			<PostItem v-for="post in posts" :post="post" />
		</ul>
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
			required: true
		}
	}

}
</script>

<style scoped>
.title {
	margin-top: 30px;
}

.post__list {
	margin-top: 30px;
}
</style>