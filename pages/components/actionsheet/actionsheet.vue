<template>
	<view class="">
		<jc-cell-group title="基础用法">
			<jc-cell isLink title="基础用法" @click="cellClick('actionsheet1')"></jc-cell>
			<jc-cell isLink title="展示取消" @click="cellClick('actionsheet2')"></jc-cell>
			<jc-cell isLink title="展示标题" @click="cellClick('actionsheet3')"></jc-cell>
			<jc-cell isLink title="展示描述" @click="cellClick('actionsheet4')"></jc-cell>
		</jc-cell-group>
		<jc-cell-group title="自定义面板">
			<jc-cell isLink title="自定义面板" @click="cellClick('actionsheet5')"></jc-cell>

		</jc-cell-group>
		<jc-action-sheet ref='actionsheet1' :actions='actions1' @select='onSelect'></jc-action-sheet>
		<jc-action-sheet ref='actionsheet2' :actions='actions1' cancel-text="取消" @select='onSelect' @cancel='onCancel'></jc-action-sheet>
		<jc-action-sheet ref='actionsheet3' title="标题" subtitle="这是标题描述" :actions='actions1' cancel-text="取消" @select='onSelect' @cancel='onCancel'></jc-action-sheet>
			<jc-action-sheet ref='actionsheet4' title="标题" subtitle="这是标题描述" :actions='actions2' cancel-text="取消" @select='onSelect' @cancel='onCancel'></jc-action-sheet>
			<jc-action-sheet ref='actionsheet5'>
				<view class="content">内容</view>
			</jc-action-sheet>
		
	</view>
</template>

<script>
	import jcCellGroup from '@/components/jc-cell-group/jc-cell-group.vue'
	import jcCell from '@/components/jc-cell/jc-cell.vue'
	import jcActionSheet from '@/components/jc-action-sheet/jc-action-sheet.vue'
	export default {
		components: {
			jcCellGroup,
			jcCell,
			jcActionSheet
		},
		data() {
			return {
				actions1: [{
						name: '选项一',
					},
					{
						name: '选项二',
					},
					{
						name: '选项三',
					},
				],
				actions2: [{
						name: '选项一',
						subname: '这是选项一的描述'
					},
					{
						name: '选项二',
					},
					{
						name: '选项三',
					},
				],
			}
		},
		methods: {
			cellClick(name) {
				this.$refs[name].open()
			},
			onCancel(name) {
				uni.showToast({
					title: name,
					icon: 'none'
				})
			},
			onSelect(action, index) {
				uni.showToast({
					title: action.name,
					icon: 'none'
				})
			}
		}
	}
</script>

<style lang="scss" scoped>
	.content{
		height: 300rpx;
		padding: 30rpx;
		width: 100%;
	}
</style>
