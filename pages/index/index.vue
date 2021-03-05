<template>
	<view class="content">
		<block v-for="(item,index) in list">
			<jc-cell :to="`/pages/components/${item.url}/${item.url}`" :title="item.name" isLink></jc-cell>
		</block>
	</view>
</template>

<script>
	import jcCell from '@/components/jc-cell/jc-cell.vue'
	export default {
		components: { jcCell },
		data() {
			return {
				list: [
					{
						name: 'Button按钮',
						url: 'button'
					},
					{
						name: 'Icon图标',
						url: 'icon'
					},
					{
						name: 'Cell单元格',
						url: 'cell'
					},
					{
						name: 'Radio单选框',
						url: 'radio'
					},
					{
						name: 'CheckBox复选框',
						url: 'checkbox'
					},
					{
						name: 'Switch开关',
						url: 'switch'
					},
					{
						name: 'Input输入框',
						url: 'input'
					},
					{
						name: 'Picker选择器',
						url: 'picker'
					},
					{
						name: 'Dialog弹出框',
						url: 'dialog'
					},
					{
						name: 'Popup弹出层',
						url: 'popup'
					},
					{
						name: 'ActionSheet动作面板',
						url: 'actionsheet'
					},
					{
						name: 'Timeline时间线',
						url: 'timeline'
					}
				]
			}
		}
	}
</script>

<style>
	.content {
		display: flex;
		flex-direction: column;
	}
</style>
