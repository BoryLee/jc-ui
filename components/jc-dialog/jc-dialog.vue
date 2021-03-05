<template>
	<view v-if="visible">
		<view class="jc-overlay" v-if="overlay" @click="close"></view>
		<view class="jc-dialog" :style="{width: width,'border-radius': borderRadius }">
			<view class="dialog-body">
				<view class="dialog-icon">
					<slot name='icon' v-if="$slots.icon"></slot>
					<jc-icon :name='icon' size="50" color="#D8D8D8" v-else></jc-icon>
				</view>
				<view class="dialog-title" v-if="title">{{title}}</view>
				<slot name="content" v-if="$slots.content"></slot>
				<template v-else>
					<view class="dialog-content" v-if="content">{{content}}</view>
				</template>
			</view>
			<view class="dialog-divide" v-if="showConfirmButton || showCancelButton"></view>
			<view class="dialog-footer">
				<slot name='footer' v-if="$slots.footer"></slot>
				<template v-else>
					<view class="dialog-button" :style="{color: cancelButtonColor}" v-if="showCancelButton" @click="cancel">
						{{cancelButtonText}}
					</view>
					<view class="button-divide" v-if="showConfirmButton && showCancelButton"></view>
					<view class="dialog-button" :style="{color: confirmButtonColor}" v-if="showConfirmButton" @click="confirm"> 
						{{confirmButtonText}}
					</view>
				</template>
				
			</view>
		</view>
	</view>
</template>

<script>
	import jcIcon from '@/components/jc-icon/jc-icon.vue'
	import jcButton from '@/components/jc-button/jc-button.vue'
	export default{
		name: 'jcDialog',
		components: { jcIcon,jcButton },
		props: {
			icon: {
				type: String
			},
			width: {
				type: String,
				default: '560rpx'
			},
			borderRadius: {
				type: String,
				default: '16rpx'
			},
			title: {
				type: String
			},
			content: {
				type: String
			},
			showConfirmButton: {
				type: Boolean,
				default: true
			},
			showCancelButton: {
				type: Boolean,
				default: false
			},
			confirmButtonText: {
				type: String,
				default: '确认'
			},
			confirmButtonColor: {
				type: String,
				default: '#912222'
			},
			cancelButtonText: {
				type: String,
				default: '取消'
			},
			cancelButtonColor: {
				type: String,
				default: '#333333'
			},
			overlay: {
				type: Boolean,
				default: true
			},
			beforeConfirm: {
				type: Function
			},
			beforeCancel: {
				type: Function
			},
		},
		data() {
			return {
				visible: false
			}
		},
		methods:{
			open(){
				 this.visible = true;
			},
			close(){
				this.visible = false;
			},
			cancel(){
				if(this.beforeCancel){
					this.beforeCancel('cancel',this.close)
				}else{
					this.close();
					this.$emit('cancel')
				}
			},
			confirm(){
				if(this.beforeConfirm){
					this.beforeConfirm('confirm',this.close)
				}else{
					this.close();
					this.$emit('confirm')
				}
				
			}
		}
	}
</script>

<style lang="scss" scoped>
	.jc-overlay{
		position: fixed;
		top: 0;
		left: 0;
		width: 100%;
		height: 100%;
		background-color: rgba($color: #000000, $alpha: 0.3);
		z-index: $jc-overlay-zIndex;
	}
	.jc-dialog{
		position: fixed;
		top: 40%;
		left: 50%;
		transform: translate(-50%,-50%);
		background-color: #fff;
		z-index: $jc-overlay-zIndex + 10;
		.dialog-body{
			padding: 40rpx 24rpx;
			display: flex;
			flex-direction: column;
			align-items: center;
			.dialog-icon{
				margin-bottom: 24rpx;
			}
			.dialog-title{
				margin-bottom: 16rpx;
				color: #333333;
				font-size: 36rpx;
				font-weight: 700;
				
			}
			.dialog-content{
				text-align: center;
				font-size: 30rpx;
				color: #333333;
			}
		}
		.dialog-divide{
			background-color: #f5f5f5;
			width: 100%;
			height: 2rpx;
		}
		.dialog-footer{
			width: 100%;
			display: flex;
			font-size: 36rpx;
			.button-divide{
				width: 2rpx;
				background-color: #f5f5f5;
			}
			.dialog-button{
				flex: 1;
				text-align: center;
				padding: 24rpx 0;
				&:active{
					background-color: $jc-bg-color-hover;
				}
			}
		}
	}
</style>
