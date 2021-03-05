<template>
	<view class="jc-checkbox-group" :style="{'flex-direction': direction}">
		<slot></slot>
	</view>
</template>

<script>
export default{
	name: 'jcCheckboxGroup',
	props: {
		value: {
			type: Array,
			default: () => []
		},
		direction: {
			type: String,
			default: 'row'
		},
		disabled:{
			type: Boolean,
			default: false
		},
		readOnly:{
			type: Boolean,
			default: false
		},
	}
}
</script>

<style lang="scss" scoped>
	.jc-checkbox-group{
		display: flex;
	}
	
</style>
