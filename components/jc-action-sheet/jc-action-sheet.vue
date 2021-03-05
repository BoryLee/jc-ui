<template>
	<view>
		<jc-popup position="bottom" size='auto' ref='popup' round>
			
			<view class="jc-action-sheet">
				<view class="header" :style="headerStyleObj">
					<text class="title" v-if="title">{{title}}</text>
					<text class="subtitle" v-if="subtitle">{{subtitle}}</text>
				</view>
				<slot v-if="$slots.default"></slot>
				<template v-else>
					<view class="body">
						<block v-for="(action,index) in actions">
							<view class="action-sheet-item" @click="actionClick(action,index)">
								<text class="action-name">{{action.name}}</text>
								<text class="action-subname">{{action.subname}}</text>
							</view>
						</block>
					</view>
					<view class="footer" v-if="cancelText">
						<view class="divide"></view>
						<view class="action-sheet-btn" @click="cancel">
							{{cancelText}}
						</view>
					</view>
				</template>
			</view>
		</jc-popup>
	</view>
</template>

<script>
	import jcPopup from '@/components/jc-popup/jc-popup.vue';
	export default {
		name: 'jcActionSheet',
		components: {
			jcPopup
		},
		props: {
			actions: {
				type: Array,
				default: () => []
			},
			cancelText: {
				type: String,
				default: ''
			},
			title: {
				type: String,
				default: ''
			},
			subtitle: {
				type: String,
				default: ''
			}
		},
		data() {
			return {
				visible: false
			}
		},
		computed: {
			headerStyleObj() {
				if (this.title || this.subtitle) {
					return {
						'padding': '30rpx',
						'border-bottom': '2rpx solid #f5f5f5'
					}
				}
			}
		},
		methods: {
			open() {
				this.$refs['popup'].open();
			},
			close() {
				this.$refs['popup'].close();
			},
			cancel() {
				this.close()
				this.$emit('cancel', this.cancelText);
			},
			actionClick(action, index) {
				this.close()
				this.$emit('select', action, index);
			}
		}
	}
</script>

<style lang="scss" scoped>
	.jc-action-sheet {
		width: 100%;

		.header {
			display: flex;
			flex-direction: column;
			align-items: center;
			font-size: 32rpx;
			color: #333;

			.title {}

			.subtitle {
				color: #999;
				font-size: 28rpx;
			}
		}

		.body {
			font-size: 32rpx;

			.action-sheet-item {
				display: flex;
				flex-direction: column;
				align-items: center;
				padding: 30rpx 0;
				border-bottom: 2rpx solid #f5f5f5;

				.action-name {
					color: #333;
				}

				.action-subname {
					color: #999;
					font-size: 28rpx;
				}

				&:active {
					background-color: $jc-bg-color-hover;
				}

			}
		}

		.footer {
			display: flex;
			flex-direction: column;
			align-items: center;
			font-size: 30rpx;

			.divide {
				width: 100%;
				height: 16rpx;
				background-color: #F5F5F5;
			}

			.action-sheet-btn {
				width: 100%;
				padding: 30rpx 0;
				text-align: center;

				&:active {
					background-color: $jc-bg-color-hover;
				}
			}
		}

	}
</style>
