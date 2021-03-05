<template>
	<view class="cell" :class="{'cell-active': isLink}"  @click="cellClick">
		<view class="cell-body" :style="borderStyleObj">
			<view class="left">
				<view class="left-icon" v-if="icon || $slots.icon">
					<jc-icon :name="icon" :size="size" color="#333" v-if="icon"></jc-icon>
					<slot name="icon" v-else></slot>
				</view>
				<view v-if="title" class="title">
					<text>{{title}}</text>
					<text class="description" v-if="description">{{description}}</text>
				</view>
				<slot name="left"></slot>
			</view>
			<view class="right">
				<text v-if="dot && dotPosition === 'left'" class="badge-text" :style="dotStyleObj">
					{{ Number(badge) ? badge : ''}}
				</text>
				<text v-if="value" class="right-txt">{{value}}</text>
				<text v-if="dot && dotPosition === 'right'" class="badge-text" :style="dotStyleObj">{{badge ? badge : ''}}</text>
				<slot name="right"></slot>
				<jc-icon name="arrow-right" :size="size" color="#CCCCCC" v-if="isLink"></jc-icon>
			</view>
		</view>
	</view>
</template>

<script>
	import jcIcon from '@/components/jc-icon/jc-icon.vue'
	export default {
		name: 'jcCell',
		components: {
			jcIcon
		},
		props: {
			icon: {
				type: String
			},
			title: {
				type: String,
			},
			description: {
				type: String
			},
			value: {
				type: String,
			},
			size: {
				type: [String, Number],
				default: 20
			},
			to: {
				type: String
			},
			replace: {
				type: Boolean,
				default: false
			},
			border: {
				type: Boolean,
				default: true
			},
			isLink: {
				type: Boolean,
				default: false
			},
			badge: {
				type: [String, Number]
			},
			dot: {
				type: Boolean,
				default: false
			},
			dotColor: {
				type: String,
				default: 'red'
			},
			dotPosition: {
				type: String,
				default: 'left'
			}
		},
		computed: {
			borderStyleObj() {
				if (this.border) {
					return {
						'border-bottom': '2rpx solid #f5f5f5'
					}
				}
			},
			dotStyleObj() {
				if (this.dot) {
					let badge = Number(this.badge)
					if (!isNaN(badge)) {
						if (badge > 0) {
							return {
								display: 'inline-block',
								'box-sizing': 'border-box',
								'min-width': '16px',
								'padding': '0 3px',
								'color': '#fff',
								'font-weight': 500,
								'font-size': '12px',
								'line-height': 1.2,
								'text-align': 'center',
								'border': '1px solid #fff',
								'border-radius': '999px',
								'background-color': this.dotColor
							}
						} else {
							return {
								'padding': '6rpx',
								'border-radius': '6rpx',
								'background-color': this.dotColor
							}
						}
					} else {
						return {
							'padding': '6rpx',
							'border-radius': '6rpx',
							'background-color': this.dotColor
						}
					}
				}
			}
		},
		methods: {
			cellClick() {
				if (this.to) {
					if(this.replace){
						uni.redirectTo({
							url: this.to
						})
					}else{
						uni.navigateTo({
							url: this.to
						})
					}
				} else {
					this.$emit('click')
				}
			}
		}
	}
</script>

<style lang="scss" scoped>
	.cell {
		padding: 0 24rpx;
		background-color: #fff;
		&.cell-active{
			&:active {
				background-color: $jc-bg-color-hover;
			}
		}
		.cell-body {
			padding: 26rpx 0;
			display: flex;
			justify-content: space-between;
			align-items: center;

			.left {
				flex: 1;
				font-size: 32rpx;
				color: #333;
				display: flex;

				.left-icon {
					margin-right: 10rpx;
				}
				.title{
					display: flex;
					flex-direction: column;
					.description{
						color: #999;
						font-size: 28rpx;
					}
				}
			}

			.right {
				color: #999;
				font-size: 30rpx;
				display: flex;
				justify-content: flex-end;
				align-items: center;
				.right-txt{
					margin-left: 10rpx;
				}
			}
		}
	}
</style>
