<template>
	<view class="radio-container">
		<view class="jc-section">
			<view class="jc-section-header">
				<text>基础用法</text>
			</view>
			<view class="jc-section-body">
				<jc-radio-group v-model='radio'>
					<jc-radio name='1'>项目一</jc-radio>
					<jc-radio name='2'>项目二</jc-radio>
				</jc-radio-group>
			</view>
		</view>
		<view class="jc-section">
			<view class="jc-section-header">
				<text>竖直排列</text>
			</view>
			<view class="jc-section-body">
				<jc-radio-group v-model='radio' direction='column'>
					<jc-radio name='1'>项目一</jc-radio>
					<jc-radio name='2'>项目二</jc-radio>
				</jc-radio-group>
			</view>
		</view>
		<view class="jc-section">
			<view class="jc-section-header">
				<text>只读状态</text>
			</view>
			<view class="jc-section-body">
				<jc-radio-group v-model='radio' read-only>
					<jc-radio name='1'>项目一</jc-radio>
					<jc-radio name='2'>项目二</jc-radio>
				</jc-radio-group>
			</view>
		</view>
		<view class="jc-section">
			<view class="jc-section-header">
				<text>禁止状态</text>
			</view>
			<view class="jc-section-body">
				<jc-radio-group v-model='radio' disabled>
					<jc-radio name='1'>项目一</jc-radio>
					<jc-radio name='2'>项目二</jc-radio>
				</jc-radio-group>
			</view>
		</view>
		<view class="jc-section">
			<view class="jc-section-header">
				<text>自定义颜色</text>
			</view>
			<view class="jc-section-body">
				<jc-radio-group v-model='radio'>
					<jc-radio name='1' checkedColor="blue">项目一</jc-radio>
					<jc-radio name='2' checkedColor="blue">项目二</jc-radio>
				</jc-radio-group>
			</view>
		</view>
	</view>
</template>

<script>
	import jcRadioGroup from '@/components/jc-radio/jc-radio-group.vue'
	import jcRadio from '@/components/jc-radio/jc-radio.vue'
	export default {
		components: { jcRadioGroup,jcRadio },
		data() {
			return {
				radio: '1'
			}
		}
	}
</script>

<style lang="scss" scoped>
	.radio-container{
		padding: 30rpx;
		.jc-section{
			display: flex;
			flex-direction: column;
		}
		
	}
</style>
