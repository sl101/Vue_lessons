<template>
	<button class="btn">
		<slot></slot>
	</button>
</template>

<script>
export default {
	name: "CustomButton"
}
</script>

<style  scoped>
.btn {
	padding: 6px 15px;
	border: 1px solid var(--brand);
	border-radius: 4px;
	cursor: pointer;
}
</style>