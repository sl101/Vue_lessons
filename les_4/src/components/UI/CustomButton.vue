<template>
	<button class="button">{{ text }}</button>
</template>

<script>
export default {
	name: 'CustomButton',
	props: {
		text: String,
		required: true
	}
}
</script>

<style scoped>
.button {
	position: relative;
	padding: 6px 15px;
	font-weight: 600;
	border: 1px solid var(--teal);
	border-radius: 4px;
	background: none;
	color: var(--teal);
	text-transform: uppercase;
	cursor: pointer;
	transition: background-color var(--transition), color var(--transition);
}

.button:hover {
	background-color: var(--teal);
	color: var(--white)
}

.button:active {
	top: 1px
}
</style>