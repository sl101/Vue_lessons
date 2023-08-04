<template>
	<input class="input" type="text" :value="modelValue" @input="updateInput" />
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

<style  scoped>
.input {
	padding: 6px 10px;
	border: 1px solid var(--brand);
	border-radius: 4px;
	cursor: text;
}
</style>