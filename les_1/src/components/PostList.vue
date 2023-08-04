<template>
	<section>
		<h2 class="posts">Список постов:</h2>
		<ul class="posts_list" v-if="posts.length > 0">
			<li class="post_item" v-for="post in posts">
				<div class="post_content">
					<p>Наименование: {{ post.title }}</p>
					<p>Описание: {{ post.body }}</p>
				</div>
				<button @click="$emit('remove', post)">Удалить</button>
			</li>
		</ul>
		<div class="empty_message" v-else>
			<p>список пуст</p>
		</div>
	</section>
</template>

<script>
export default {
	props: {
		posts: {
			type: Array,
			required: true
		}
	}
}
</script>

<style scoped>
.post_item {
	margin-bottom: 20px;
	padding: 4px 10px;
	display: flex;
	justify-content: space-between;
	align-items: center;
	border: 2px solid var(--brand);
	border-radius: 4px;
}

.empty_message {
	color: var(--error);
}
</style>