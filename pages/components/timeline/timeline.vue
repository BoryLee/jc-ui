<template>
	<view class="timeline-container">
		<view class="jc-section">
			<view class="jc-section-header">
				<text>基础用法</text>
			</view>
			<view class="jc-section-body">
				<jc-timeline>
					<block v-for="(item,index) in activities" :key='index'>
						<jc-timeline-item :title="item.title" :content="item.content"></jc-timeline-item>
					</block>
				</jc-timeline>
			</view>
		</view>
		<view class="jc-section">
			<view class="jc-section-header">
				<text>轴点类型</text>
			</view>
			<view class="jc-section-body">
				<jc-timeline>
					<block v-for="(item,index) in activities" :key='index'>
						<jc-timeline-item :title="item.title" :content="item.content" :dotColor='item.color' :dotType='item.dotType'></jc-timeline-item>
					</block>
				</jc-timeline>
			</view>
		</view>
		<view class="jc-section">
			<view class="jc-section-header">
				<text>自定义轴点样式</text>
			</view>
			<view class="jc-section-body">
				<jc-timeline>
					<jc-timeline-item title="2021-03-04" content="您提交了订单，请等待系统确认">
						<template #dot>
							<image src="/static/logo.png" mode="" class="dot-img"></image>
						</template>
					</jc-timeline-item>
					<jc-timeline-item title="2021-03-04" content="您提交了订单，请等待系统确认" dotColor='f00' dotType='stroke'>
					</jc-timeline-item>
					<jc-timeline-item title="2021-03-04" content="您提交了订单，请等待系统确认" dotColor='rgb(69, 103, 0)' dotType='stroke'>
					</jc-timeline-item>
					<jc-timeline-item title="2021-03-04" content="您提交了订单，请等待系统确认" dotColor='f00'>
					</jc-timeline-item>
				</jc-timeline>
			</view>
		</view>

	</view>
</template>

<script>
	import jcTimeline from '@/components/jc-timeline/jc-timeline.vue'
	import jcTimelineItem from "@/components/jc-timeline/jc-timeline-item.vue"
	import jcIcon from '@/components/jc-icon/jc-icon.vue'
	export default {
		components: {
			jcTimeline,
			jcTimelineItem,
			jcIcon
		},
		data() {
			return {
				activities: [{
					title: '2021-03-04',
					content: '您提交了订单，请等待系统确认',

				}, {
					title: '2021-03-04',
					content: '您提交了订单，请等待系统确认',
				}, {
					title: '2021-03-04',
					content: '您提交了订单，请等待系统确认',
				}, {
					title: '2021-03-04',
					content: '您提交了订单，请等待系统确认'
				}],
				activities: [{
					title: '2021-03-04',
					content: '您提交了订单，请等待系统确认',
					color: '#f00'

				}, {
					title: '2021-03-04',
					content: '您提交了订单，请等待系统确认',
					color: '#f00',
					dotType: 'stroke'
				}, {
					title: '2021-03-04',
					content: '您提交了订单，请等待系统确认',
					color: 'rgb(69, 103, 0)'
				}, {
					title: '2021-03-04',
					content: '您提交了订单，请等待系统确认',
					color: '#f00'
				}]
			}
		}
	}
</script>
<style lang="scss" scoped>
	.timeline-container {
		padding: 30rpx;
		width: 100%;
		height: 100%;
		overflow: auto;
		background-color: #fff;

		.jc-section {
			display: flex;
			flex-direction: column;
			.dot-img{
				width: 30rpx;
				height: 30rpx;
				border-radius: 50%;
			}
			.jc-section-body {
				margin: 20rpx 0;
			}
		}

	}
</style>
