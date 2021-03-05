<template>
	<view class="checkbox-container">
		<view class="jc-section">
			<view class="jc-section-header">
				<text>基础用法</text>
			</view>
			<view class="jc-section-body">
				<jc-checkbox-group v-model="checkbox">
					<jc-checkbox name="1">项目一</jc-checkbox>
					<jc-checkbox name="2">项目二</jc-checkbox>
				</jc-checkbox-group>
			</view>
		</view>
		<view class="jc-section">
			<view class="jc-section-header">
				<text>竖直排列</text>
			</view>
			<view class="jc-section-body">
				<jc-checkbox-group v-model="checkbox" direction="column">
					<jc-checkbox name="1">项目一</jc-checkbox>
					<jc-checkbox name="2">项目二</jc-checkbox>
				</jc-checkbox-group>
			</view>
		</view>
		<view class="jc-section">
			<view class="jc-section-header">
				<text>只读状态</text>
			</view>
			<view class="jc-section-body">
				<jc-checkbox-group v-model="checkbox" readOnly>
					<jc-checkbox name="1">项目一</jc-checkbox>
					<jc-checkbox name="2">项目二</jc-checkbox>
				</jc-checkbox-group>
			</view>
		</view>
		<view class="jc-section">
			<view class="jc-section-header">
				<text>禁止状态</text>
			</view>
			<view class="jc-section-body">
				<jc-checkbox-group v-model="checkbox" disabled>
					<jc-checkbox name="1">项目一</jc-checkbox>
					<jc-checkbox name="2">项目二</jc-checkbox>
				</jc-checkbox-group>
			</view>
		</view>
		<view class="jc-section">
			<view class="jc-section-header">
				<text>自定义颜色</text>
			</view>
			<view class="jc-section-body">
				<jc-checkbox-group v-model="checkbox">
					<jc-checkbox name="1" checkedColor="blue">项目一</jc-checkbox>
					<jc-checkbox name="2" checkedColor="red">项目二</jc-checkbox>
				</jc-checkbox-group>
			</view>
		</view>
		
	</view>
</template>

<script>
	import jcCheckboxGroup from '@/components/jc-checkbox/jc-checkbox-group.vue'
	import jcCheckbox from '@/components/jc-checkbox/jc-checkbox.vue'
	export default {
		components: { jcCheckboxGroup,jcCheckbox },
		data() {
			return {
				'checkbox': ['1']
			}
		}
	}
</script>

<style lang="scss" scoped>
	.checkbox-container{
		padding: 30rpx;
		.jc-section{
			display: flex;
			flex-direction: column;
		}
		
	}
</style>
