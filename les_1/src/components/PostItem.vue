<template>
	<li class="post_item">
		<div>
			<p><strong style="margin-right: 5px;">Наименование:</strong> {{ post.title }}</p>
			<p><strong style="margin-right: 5px;">Описание:</strong> {{ post.body }}</p>
		</div>
		<CustomButton @click="this.$emit('remove', post)">Удалить</CustomButton>
	</li>
</template>

<script>
export default {
	props: {
		post: {
			type: Object,
		}
	}
}
</script>

<style scoped>
.post_item {
	padding: 10px;
	display: flex;
	justify-content: space-between;
	align-items: center;
	gap: 50px;
	border: 2px solid var(--brand);
	border-radius: 4px;
}
</style>