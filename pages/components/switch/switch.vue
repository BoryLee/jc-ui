<template>
	<view class="switch-content">
		<view class="cell">
			<text>基础用法</text>
			<jc-switch v-model="checked1"></jc-switch>
		</view>
		<view class="cell">
			<text>只读状态</text>
			<jc-switch v-model="checked1" readOnly></jc-switch>
		</view>
		<view class="cell">
			<text>禁用状态</text>
			<jc-switch v-model="checked1" disabled></jc-switch>
		</view>
		<view class="cell">
			<text>自定义大小</text>
			<view class="cell-body">
				<jc-switch v-model="checked1" :width="50"></jc-switch>
				<jc-switch v-model="checked1"></jc-switch>
				<jc-switch v-model="checked1" :width="150"></jc-switch>
			</view>
		</view>
		<view class="cell">
			<text>自定义颜色</text>
			<view class="cell-body">
				<jc-switch v-model="checked2" activeColor="#1989fa" inActiveColor="#f00"></jc-switch>
			</view>
		</view>
		<view class="cell">
			<text>异步控制</text>
			<view class="cell-body">
				<jc-switch :value="checked3" @input='onInput'></jc-switch>
			</view>
		</view>
		<jc-dialog ref='dialog' title="提示" content="是否切换开关?" showCancelButton></jc-dialog>
	</view>
</template>

<script>
	import jcSwitch from '@/components/jc-switch/jc-switch.vue'
	import jcDialog from '@/components/jc-dialog/jc-dialog.vue'
	export default {
		components: {
			jcSwitch,
			jcDialog
		},
		data() {
			return {
				checked1: true,
				checked2: false,
				checked3: true
			}
		},
		methods:{
			onInput(checked){
				this.$refs['dialog'].open()
			}
		}
	}
</script>

<style lang="scss" scoped>
	.switch-content {
		display: flex;
		flex-direction: column;
		background-color: #fff;
		height: 100%;
		overflow: auto;

		.cell {
			display: flex;
			flex-direction: column;
			width: 80%;
			margin: 10rpx auto;
		}
	}
</style>
