<template>
	<li class="post">
		<div class="post_content">
			<p>Название: {{ post.title }}</p>
			<p>Описание: {{ post.body }}</p>
		</div>
		<CustomButton @click="$emit('remove', post)">Удалить</CustomButton>
	</li>
</template>

<script>
export default {
	props: {
		post: {
			type: Object,
			required: true
		}
	}
}
</script>

<style scoped>
.post {
	padding: 10px;
	margin: 20px 0;
	border: 2px solid var(--accent);
	border-radius: 6px;
	display: flex;
	justify-content: space-between;
	align-items: center;
	gap: 50px;
}
</style>