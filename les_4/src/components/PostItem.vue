<template>
	<li class="post">
		<div class="post__content">
			<p>{{ post.title }}</p>
			<p>{{ post.body }}</p>
		</div>
		<CustomButton @click="$emit('remove', post)" text="Delete" />
	</li>
</template>

<script>
export default {
	props: {
		post: {
			type: Object,
			required: true
		}
	},
	//methods: {
	//	removePost() {
	//		console.log(this.post.id);
	//	}
	//}
}
</script>

<style>
.post {
	padding: 8px 15px;
	display: flex;
	justify-content: space-between;
	align-items: center;
	gap: 50px;
	border: 2px solid teal;
}

.post__content {
	display: flex;
	gap: 20px;
	align-items: center;
}

.button {
	padding: 4px 15px;
}
</style>