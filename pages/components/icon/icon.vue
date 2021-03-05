<template>
	<view class="icon-conatiner">
		<block v-for="(value,key) in icons">
			<view class="icon-cell" >
				<jc-icon :name='key' @click='selectIcon(key)'></jc-icon>
				<text class="txt">{{key}}</text>
			</view>
		</block>
		
	</view>
</template>

<script>
	import jcIcon from '@/components/jc-icon/jc-icon.vue'
	import icons from  './icon.js'
	export default {
		components: { jcIcon },
		data() {
		  return {
			  icons
		  }
		},
		methods:{
			selectIcon(name){
				// #ifdef APP-PLUS
				uni.setClipboardData({
					data: name,
					success(){
						uni.showToast({
							icon:"success",
							title: `图标${name}复制成功`
						})
					}
				})
				// #endif
			}
		}
	}
</script>

<style lang="scss" scoped>
	.icon-conatiner{
		display: flex;
		flex-wrap: wrap;
		.icon-cell{
			display: flex;
			flex-direction: column;
			align-items: center;
			width: 25%;
			margin: 20rpx 0;
			.txt{
				font-size: 26rpx;
			}
		}

	}
</style>
