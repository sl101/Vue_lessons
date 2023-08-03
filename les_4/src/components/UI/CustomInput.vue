<template>
	<input class="input" :value="modelValue" @input="updateInput">
</template>

<script>
export default {
	name: "CustomInput",
	props: {
		modelValue: [String, Number]
	},
	methods: {
		updateInput(event) {
			this.$emit('update:modelValue', event.target.value)
		}
	}
}
</script>

<style scoped>
.input {
	padding: 6px 15px;
	border: 1px solid var(--teal);
	border-radius: 4px;
	background: none;
	color: var(--black);
	cursor: text;
}
</style>