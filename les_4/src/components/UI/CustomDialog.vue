<template>
	<div @click="closeDialog" class="dialog" v-if="show">
		<div @click.stop class="dialog_content">
			<slot></slot>
		</div>
	</div>
</template>

<script>
export default {
	name: "CustomDialog",
	props: {
		show: {
			type: Boolean,
			default: false
		}
	},
	methods: {
		closeDialog() {
			this.$emit('update:show', false)
		}
	}
}
</script>

<style  scoped>
.dialog {
	top: 0;
	right: 0;
	bottom: 0;
	left: 0;
	position: fixed;
	background-color: rgba(0, 0, 0, .5);
	display: flex;
}

.dialog_content {
	margin: auto;
	padding: 20px;
	min-width: 400px;
	min-height: 200px;
	border-radius: 12px;
	background-color: var(--white);
}
</style>