<template>
	<view class="btn-cells">
		<view class="btn-cell">
			<text>项目按钮</text>
			<view class="btn-conatiner">
				<view class="btn-block">
					<jc-button color="#912222">直角按钮</jc-button>
				</view>
				<view class="btn-block">
					<jc-button color="#912222" disabled>直角按钮</jc-button>
				</view>
				<view class="btn-block">
					<jc-button color="#912222" plain>直角按钮</jc-button>
				</view>
				<view class="btn-block">
					<jc-button color="#912222" plain disabled>直角按钮</jc-button>
				</view>
				<view class="btn-block">
					<jc-button round plain color="#912222">圆形按钮</jc-button>
				</view>
			</view>
		</view>
		<view class="btn-cell">
			<text>按钮类型</text>
			<view class="btn-conatiner">
				<view class="btn-block">
					<jc-button type="primary" text="主要按钮"></jc-button>
				</view>
				<view class="btn-block">
					<jc-button type="info" text="信息按钮"></jc-button>
				</view>
				<view class="btn-block">
					<jc-button text="默认按钮"></jc-button>
				</view>
				<view class="btn-block">
					<jc-button type="warning" text="警告按钮"></jc-button>
				</view>
				<view class="btn-block">
					<jc-button type="danger" text="危险按钮"></jc-button>
				</view>
			</view>
		</view>
		<view class="btn-cell">
			<text>朴素按钮</text>
			<view class="btn-conatiner">
				<view class="btn-block">
					<jc-button plain type="primary" text="主要按钮"></jc-button>
				</view>
				<view class="btn-block">
					<jc-button plain type="info" text="信息按钮"></jc-button>
				</view>
			</view>
		</view>
		<view class="btn-cell">
			<text>图标类型</text>
			<view class="btn-conatiner">
				<view class="btn-block">
					<jc-button plain type="primary" icon='add'></jc-button>
				</view>
				<view class="btn-block">
					<jc-button plain type="primary" icon='add'>按钮</jc-button>
				</view>
				<view class="btn-block">
					<jc-button plain type="info" icon='person'>按钮</jc-button>
				</view>
			</view>
		</view>
		<view class="btn-cell">
			<text>按钮形状</text>
			<view class="btn-conatiner">
				<view class="btn-block">
					<jc-button round type="primary" text="圆形按钮"></jc-button>
				</view>
				<view class="btn-block">
					<jc-button square type="info" text="方形按钮"></jc-button>
				</view>
			</view>
		</view>
		<view class="btn-cell">
			<text>按钮尺寸</text>
			<view class="btn-conatiner">
				<view class="btn-block">
					<jc-button type="primary" size="large">大号按钮</jc-button>	
				</view>
				<view class="btn-block">
					<jc-button type="primary" size="normal">普通按钮</jc-button>
				</view>
				<view class="btn-block">
					<jc-button type="primary" size="small">小型按钮</jc-button>
				</view>
				<view class="btn-block">
					<jc-button type="primary" size="mini">迷你按钮</jc-button>
				</view>
			</view>
		</view>
		<view class="btn-cell">
			<text>标签按钮</text>
			<view class="btn-conatiner">
				<view class="btn-block">
					<jc-button color="#7B9BDB" round size='small'>标签</jc-button>
				</view>
				<view class="btn-block">
					<jc-button color="#7B9BDB" round disabled size='small'>标签</jc-button>
				</view>
				<view class="btn-block">
					<jc-button color="#FFC76D" round size='small'>标签</jc-button>
				</view>
				<view class="btn-block">
					<jc-button color="#FFC76D" round disabled size='small'>标签</jc-button>
				</view>
				<view class="btn-block">
					<jc-button color="#912222" round size='small'>标签</jc-button>
				</view>
				<view class="btn-block">
					<jc-button color="#912222" round disabled size='small'>标签</jc-button>
				</view>
			</view>
		</view>
		<view class="btn-cell">
			<view class="btn-conatiner">
				<view class="btn-block">
					<jc-button color="#7B9BDB" round plain size='small'>标签</jc-button>
				</view>
				<view class="btn-block">
					<jc-button color="#FFC76D" round plain size='small'>标签</jc-button>
				</view>
				<view class="btn-block">
					<jc-button color="#912222" round plain size='small'>标签</jc-button>
				</view>
			</view>
		</view>
		<view class="btn-cell">
			<view class="btn-conatiner">
				<view class="btn-block">
					<jc-button color="#666" round plain size='mini'>标签</jc-button>
				</view>
				<view class="btn-block">
					<jc-button color="#666" round plain disabled size='mini'>标签</jc-button>
				</view>
			</view>
		</view>
		<view class="btn-cell">
			<text>自定义颜色</text>
			<view class="btn-conatiner">
				<view class="btn-block">
					<jc-button color="#7232dd" text="主要按钮"></jc-button>
				</view>
				<view class="btn-block">
					<jc-button plain color="#7232dd" text="主要按钮"></jc-button>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	import jcButton from '@/components/jc-button/jc-button.vue';
	import jcIcon from '@/components/jc-icon/jc-icon.vue';
	export default {
		components: {
			jcButton,
			jcIcon
		}
	}
</script>

<style lang="scss" scoped>
	.btn-cells {
		padding: 30rpx 0;

		.btn-cell {
			width: 92%;
			margin: 0 auto;

			.btn-conatiner {
				display: flex;
				flex-wrap: wrap;

				.btn-block {
					margin-right: 32rpx;
					margin-top: 20rpx;
				}
			}
		}
	}
</style>
