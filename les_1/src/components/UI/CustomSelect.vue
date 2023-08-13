<template>
	<select class='select' @change="changeOption" :input="modelValue">
		<option disabled value="">Выберите вариант</option>
		<option v-for="option in options" :key="option.value" :value="option.value"> {{ option.name }}</option>
	</select>
</template>

<script>
export default {
	name: 'CustomSelect',
	props: {
		modelValue: {
			type: String,
		},
		options: {
			type: Array,
			default: () => []
		}
	},
	methods: {
		changeOption(event) {
			this.$emit('update:modelValue', event.target.value)
		}
	}
}
</script>

<style scoped>
.select {
	padding: 4px 10px;
	border-radius: 4px;
	border: 1px solid var(--accent);
	cursor: pointer;
	outline: none;
}
</style>