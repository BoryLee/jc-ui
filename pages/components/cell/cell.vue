<template>
	<view class="cell-container">
		<jc-cell-group title="基础用法">
			<jc-cell title="单元格" value="内容"></jc-cell>
			<jc-cell title="单元格" description="描述" value="内容"></jc-cell>
		</jc-cell-group>
		<jc-cell-group title="展示图标">
			<jc-cell title="单元格" icon="time-location-l" value="内容"></jc-cell>
			<jc-cell title="自定义图标" value="内容">
				<template #icon>
					<image src="/static/logo.png" mode="" class="icon-img"></image>
				</template>
			</jc-cell>
		</jc-cell-group>
		<jc-cell-group title="展示箭头">
			<jc-cell title="单元格" isLink></jc-cell>
			<jc-cell title="单元格" value="内容" isLink></jc-cell>
		</jc-cell-group>
		<jc-cell-group title="页面导航">
			<jc-cell title="单元格" isLink to='/pages/index/index'></jc-cell>
			<jc-cell title="单元格" value="内容" isLink></jc-cell>
		</jc-cell-group>
		<jc-cell-group title="展示徽标">
			<jc-cell title="单元格" dot isLink dotColor='red'></jc-cell>
			<jc-cell title="自定义颜色" dot isLink dotColor='blue'></jc-cell>
			<jc-cell title="单元格" dot isLink dotColor='red' value="详细描述"></jc-cell>
			<jc-cell title="单元格" dot isLink badge="100" dotColor='red'></jc-cell>
		</jc-cell-group>
		<jc-cell-group title="slot自定义">
			<jc-cell>
				<template #left>
					<view>左边内容</view>
				</template>
				<template #right>
					<view>右边内容</view>
				</template>
			</jc-cell>
			<jc-cell isLink>
				<template #left>
					<view>左边内容</view>
				</template>
				<template #right>
					<view>右边内容</view>
				</template>
			</jc-cell>
		</jc-cell-group>
	</view>
</template>

<script>
	import jcCellGroup from '@/components/jc-cell-group/jc-cell-group.vue';
	import jcCell from '@/components/jc-cell/jc-cell.vue';
	export default{
		components: { jcCellGroup,jcCell },
	}
	
</script>

<style lang="scss" scoped>
	.cell-container{
		padding: 32rpx;
		background-color: #f5f5f5;
		.icon-img{
			width: 40rpx;
			height: 40rpx;
		}
	}
</style>
