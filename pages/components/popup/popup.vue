<template>
	<view class="popup-container">
		<jc-cell-group title="基础用法">
			<jc-cell title="展示弹出层" isLink @click="cellClick('popup')"></jc-cell>
		</jc-cell-group>
		<jc-cell-group title="弹出位置">
			<jc-cell title="顶部弹出" isLink @click="cellClick('popup1')"></jc-cell>
			<jc-cell title="底部弹出" isLink @click="cellClick('popup2')"></jc-cell>
			<jc-cell title="左部弹出" isLink @click="cellClick('popup3')"></jc-cell>
			<jc-cell title="右部弹出" isLink @click="cellClick('popup4')"></jc-cell>
		</jc-cell-group>
		<jc-cell-group title="圆角弹窗">
			<jc-cell title="圆角弹窗" isLink @click="cellClick('popup5')"></jc-cell>
		</jc-cell-group>
		<jc-popup ref='popup'>内容</jc-popup>
		<jc-popup ref='popup1' position="top"></jc-popup>
		<jc-popup ref='popup2' position="bottom" :style="{width:'50%'}"></jc-popup>
		<jc-popup ref='popup3' position="left"></jc-popup>
		<jc-popup ref='popup4' position="right"></jc-popup>
		<jc-popup ref='popup5' round position="bottom"></jc-popup>
	</view>
</template>

<script>
	import jcCellGroup from '@/components/jc-cell-group/jc-cell-group.vue'
	import jcCell from '@/components/jc-cell/jc-cell.vue'
	import jcPopup from '@/components/jc-popup/jc-popup.vue'
	export default{
		components: { jcCellGroup,jcCell,jcPopup },
		methods:{
			cellClick(name){
				this.$refs[name].open()
			}
		}
	}
</script>

<style lang="scss" scoped>
	.popup-container{
		width: 100%;
		height: 100%;
		overflow: auto;
		background-color: #f5f5f5;
	}
</style>
