<template>
	<view class="dialog-content">
		<jc-cell-group title="基础用法">
			<jc-cell title="提示弹窗" @click="cellClick('dialog1')"></jc-cell>
			<jc-cell title="提示弹窗(无标题)" @click="cellClick('dialog2')"></jc-cell>
			<jc-cell title="提示弹窗(只有标题)" @click="cellClick('dialog4')"></jc-cell>
			<jc-cell title="确认弹窗" @click="cellClick('dialog3')"></jc-cell>
		</jc-cell-group>
		<jc-cell-group title="异步调用">
			<jc-cell title="提示弹窗" @click="cellClick('dialog5')"></jc-cell>
		</jc-cell-group>
		<jc-cell-group title="带图标">
			<jc-cell title="图标弹窗" @click="cellClick('dialog6')"></jc-cell>
			<jc-cell title="自定义图标弹窗" @click="cellClick('dialog7')"></jc-cell>
		</jc-cell-group>
		<jc-cell-group title="自定义内容">
			<jc-cell title="自定义内容弹窗" @click="cellClick('dialog8')"></jc-cell>
		</jc-cell-group>
		<jc-dialog ref='dialog1' title="你好" content="说明当前状态、提示用户解决方案最好不要超过两行。"></jc-dialog>
		<jc-dialog ref='dialog2' content="说明当前状态、提示用户解决方案最好不要超过两行。"></jc-dialog>
		<jc-dialog ref='dialog3' showCancelButton title="你好" content="说明当前状态、提示用户解决方案最好不要超过两行。"></jc-dialog>
		<jc-dialog ref='dialog4' showCancelButton title="你好"></jc-dialog>
		<jc-dialog ref='dialog5' showCancelButton title="你好" content="说明当前状态、提示用户解决方案最好不要超过两行。" :before-confirm='beforeConfirm' :before-cancel='beforeCancel'></jc-dialog>
		<jc-dialog ref='dialog6'  icon='astro-l'  showCancelButton title="你好" content="说明当前状态、提示用户解决方案最好不要超过两行。">
		</jc-dialog>
		<jc-dialog ref='dialog7' showCancelButton title="你好" content="说明当前状态、提示用户解决方案最好不要超过两行。">
			<template #icon>
				<image src="/static/logo.png" mode="" class="dialog-icon"></image>
			</template>
		</jc-dialog>
		<jc-dialog ref='dialog8' showCancelButton title="你好">
			<template #content>
				<view class="dialog-custom">
					<text class="dialog-custom-title">内容标题</text>
					<text class="dialog-custom-content">说明当前状态、提示用户解决方案最好不要超过两行。说明当前状态、提示用户解决方案最好不要超过两行。说明当前状态、提示用户解决方案最好不要超过两行。说明当前状态、提示用户解决方案最好不要超过两行。说明当前状态、提示用户解决方案最好不要超过两行。说明当前状态、提示用户解决方案最好不要超过两行。</text>
				</view>
			</template>
		</jc-dialog>
	</view>
</template>

<script>
	import jcCellGroup from '@/components/jc-cell-group/jc-cell-group.vue'
	import jcCell from '@/components/jc-cell/jc-cell.vue'
	import jcDialog from '@/components/jc-dialog/jc-dialog.vue'
	export default{
		components: { jcCellGroup,jcCell,jcDialog },
		methods:{
			cellClick(name){
				this.$refs[name].open()
			},
			beforeCancel(action,done){
				if(action==='cancel'){
					setTimeout(()=>{
						done()
					},1000)
				}
			},
			beforeConfirm(action,done){
				if(action==='confirm'){
					setTimeout(()=>{
						done()
					},1000)
				}
			}
		}
	}
</script>

<style lang="scss" scoped>
	.dialog-icon{
		width: 280rpx;
		height: 280rpx;
	}
	.dialog-custom{
		display: flex;
		flex-direction: column;
		color: #333333;
		font-size: 30rpx;
		.dialog-custom-title{
			font-weight: 700;
		}
	}
</style>
