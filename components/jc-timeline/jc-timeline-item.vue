<template>
	<view class="timeline-item">
		<view class="timeline-item-left">
			<view class="timeline-dot" :style="{width: size+'rpx'}">
				<slot name='dot' v-if='$slots.dot'></slot>
				<view class="circle" :style="dotStyleObj" v-else></view>
			</view>
			<view class="timeline-line" :style="{'background-color': lineColor}"></view>
		</view>
		<view class="timeline-item-right">
			<view class="timeline-item-title" :style="{'line-height': size+'rpx',color: titleColor}">
				{{title}}
			</view>
			<view class="timeline-item-content" :style="{'line-height': size+'rpx',color: contentColor}">
				{{content}}
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		name: 'jcTimelineItem',
		props: {
			title: {
				type: String,
				default: ''
			},
			titleColor: {
				type: String,
				default: '#333'
			},
			content: {
				type: String,
				default: ''
			},
			contentColor: {
				type: String,
				default: '#999'
			},
			size: {
				type: Number,
				default: 24
			},
			dotType: { //fill 填充 stroke 描边
				type: String,
				default: 'fill'
			},
			dotColor: {
				type: String,
				default: '#f00'
			},
			lineColor: {
				type: String,
				default: '#c2c2c2'
			}
		},
		computed:{
			dotStyleObj(){
				let w = this.size - 2;
				let styleObj = {
					width: w + 'rpx',
					height: w + 'rpx'
				};
				if(this.dotType === 'fill'){
					styleObj['background-color'] = this.dotColor;
					styleObj['border-color'] = this.dotColor;
				}else if(this.dotType === 'stroke'){
					styleObj['background-color'] = '#fff';
					styleObj['border-color'] = this.dotColor;
				}
				return styleObj;
			}
		}

	}
</script>

<style lang="scss" scoped>
	.timeline-item {
			display: flex;
			.timeline-item-left {
				display: flex;
				flex-direction: column;
				align-items: center;
	
				.timeline-dot {
					position: relative;
					display: flex;
					justify-content: center;
	
					.circle {
						border-radius: 50%;
						border: 2rpx solid #f00;
						background-color: #f00;
					}
				}
	
				.timeline-line {
					width: 2rpx;
					height: 100%;
				}
			}
	
			.timeline-item-right {
				padding-left: 20rpx;
				padding-bottom: 30rpx;
				font-size: 24rpx;
	
				.timeline-item-title {
					padding-left: 14rpx;
					margin-bottom: 14rpx;
					position: relative;
					font-size: 30rpx;
				}
	
				.timeline-item-content {
					padding-left: 14rpx;
					font-size: 26rpx;
				}
			}
	
			&:last-child {
				.timeline-line {
					height: 0 !important;
				}
			}
		}
	
</style>


