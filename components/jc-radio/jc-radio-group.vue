<template>
	<view class="jc-radio-group" :style="{'flex-direction': direction}">
		<slot></slot>
	</view>
</template>

<script>
export default{
	name: 'jcRadioGroup',
	props: {
		value: {
			type: String
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
	.jc-radio-group{
		display: flex;
	}
	
</style>
