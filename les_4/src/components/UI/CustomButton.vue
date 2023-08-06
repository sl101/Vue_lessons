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

<style scoped>
.btn {
	padding: 6px 12px;
	font-weight: 600;
	border: 1px solid var(--accent);
	border-radius: 4px;
	text-transform: uppercase;
	background-color: transparent;
}
</style>