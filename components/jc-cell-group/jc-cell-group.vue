<template>
	<view class="cell-group" :style="{'border-radius': borderRadius + 'px'}">
		<text class="title" v-if="title">{{title}}</text>
		<slot></slot>
		<view class="space-white"></view>
	</view>
</template>

<script>
	export default{
		name: 'jcCellGroup',
		props: {
			title: {
				type: String
			},
			borderRadius: {
				type: [Number,String],
				default: 4
			}
		}
	}
</script>

<style lang="scss" scoped>
	.cell-group{
		display: flex;
		flex-direction: column;
		.title{
			font-size: 30rpx;
			padding: 10rpx 24rpx;
			color: #999999;
		}
		.space-white{
			height: 24rpx;
			width: 100%;
		}
	}
</style>
