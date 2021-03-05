<template>
	<view 
			class="jc-switch" 
			:class="{'jc-switch-disable': disabled,'jc-switch-on': !!this.value}" 
			:style="switchStyleObj"
			@click='switchChange'
			>
		<view class="jc-switch-node" :style="switchNodeStyleObj"></view>
	</view>
</template>

<script>
	export default {
		name: 'jc-switch',
		props: {
			value: {
				type: [Boolean, String]
			},
			readOnly: {
				type: Boolean
			},
			disabled: {
				type: Boolean,
				default: false
			},
			width: {
				type: Number,
				default: 100
			},
			activeColor: {
				type: String,
				default: '#912222'
			},
			inActiveColor: {
				type: String,
				default: '#DDDDDD'
			}
		},
		computed:{
			height(){
				const rate = this.width / 100;
				let height = rate === 1 ? 50 : 50 * rate;
				return height;
			},
			switchStyleObj(){
				const checked = !!this.value;
				let styleObj = {
					width:this.width+ 'rpx',
					height:this.height+ 'rpx',
					'border-radius':this.height+ 'rpx' 
				};
				if(checked){
					styleObj['background-color'] = this.activeColor;
				}else{
					styleObj['background-color'] = this.inActiveColor;
				}
				return styleObj;
			},
			switchNodeStyleObj(){
				const checked = !!this.value;
				let height = this.height - 8;
				let styleObj = {
					width: height + 'rpx',
					height:height + 'rpx'
				}
				if(checked){
					styleObj['left'] =  this.width - 4 - height + 'rpx';
				}else{
					styleObj['left'] = '4rpx';
				}
				return styleObj;
			}
		},
		methods:{
			switchChange(){
				if(this.disabled || this.readOnly) return;
				const checked = !!!this.value;
				this.$emit('input',checked)
			}
		}
	}
</script>

<style lang="scss" scoped>
	.jc-switch {
		position: relative;
		display: inline-block;
		box-sizing: content-box;
		font-size: 30rpx;
		// border: 2px solid rgba(0, 0, 0, 0.1);
		cursor: pointer;
		transition: background-color 0.3s;
		&.jc-switch-disable{
			opacity: 0.3;
		}
		.jc-switch-node {
			position: absolute;
			top: 4rpx;
			left: 4rpx;
			border-radius: 50%;
			background-color: #fff;
			box-shadow: -2px 4px 4px 0px rgba(0, 0, 0, 0.1), 0px 4px 23px 0px rgba(0, 0, 0, 0.08), 0px 0px 4px 0px rgba(0, 0, 0, 0.2);
			transition: left 0.3s;
		}
		
	}
</style>
