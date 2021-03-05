<template>
	<view v-if="visible">
		<view class="jc-overlay" @click="close"></view>
		<view class="jc-popup" :class="`jc-popup-${position}`" :style="popupStyleObj">
			<slot></slot>
		</view>
		
	</view>
</template>

<script>
	export default{
		name: 'jc-popup',
		props: {
			position: {
				type: String,
				default: 'center'
			},
			round: {
				type: Boolean,
				default: false
			},
			size: {
				type: String,
				default: '40%'
			}
		},
		data() {
			return {
				visible: false
			}
		},
		computed:{
			popupStyleObj(){
				let styleObj = {};
				if(this.position === 'center'){
					styleObj['padding'] = '30rpx 50rpx';
					if(this.round){
						styleObj['border-radius'] = '16rpx';
					}	
				}else if(this.position === 'top'){
					styleObj['height'] = this.size;
					if(this.round){
						styleObj['border-bottom-left-radius'] = '16rpx';
						styleObj['border-bottom-right-radius'] = '16rpx';
					}	
				}else if(this.position === 'bottom'){
					styleObj['height'] = this.size;
					if(this.round){
						styleObj['border-top-left-radius'] = '16rpx';
						styleObj['border-top-right-radius'] = '16rpx';
					}	
				}else if(this.position === 'left'){
					styleObj['width'] = this.size;
					if(this.round){
						styleObj['border-bottom-right-radius'] = '16rpx';
						styleObj['border-top-right-radius'] = '16rpx';
					}	
				}else if(this.position === 'right'){
					styleObj['width'] = this.size;
					if(this.round){
						styleObj['border-top-left-radius'] = '16rpx';
						styleObj['border-bottom-left-radius'] = '16rpx';
					}	
				}
				
				// if(Object.keys(this.style).length > 0){
				// 	styleObj = Object.assign(styleObj,this.style)
				// }
				return styleObj;
			}
		},
		methods:{
			open(){
				this.visible = true;
			},
			close(){
				this.visible = false;
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
		transition: opacity 0.3; 
	}
	.jc-popup{
		position: fixed;
		background-color: #fff;
		z-index: $jc-overlay-zIndex + 10;
		max-height: 100%;
		overflow-y: auto;
		transition: transform 0.3s;
		box-sizing: border-box;
	}
	.jc-popup-center{
		top: 50%;
		left: 50%;
		transform: translate(-50%,-50%);
		animation: fadeIn 0.3s;
	}
	.jc-popup-top{
		top: 0;
		left: 0;
		width: 100%;
		animation: slideInDown 0.3s ease;
	}
	.jc-popup-bottom{
		bottom: 0;
		left: 0;
		width: 100%;
		animation: slideInUp 0.3s ease;
	}
	.jc-popup-left{
		top: 0;
		left: 0;
		height: 100%;
		animation: slideInLeft 0.3s ease;
	}
	.jc-popup-right{
		top: 0;
		right: 0;
		height: 100%;
		animation: slideInRight 0.3s ease;
	}
</style>
