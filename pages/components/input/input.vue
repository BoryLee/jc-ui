<template>
	<view class="input-container">
		<view class="jc-section">
			<view class="jc-section-header">
				<text>基础用法</text>
			</view>
			<view class="jc-section-body">
				<jc-input label="文本" v-model='text1' placeholder="请输入文本" />
				<jc-input label="文本" v-model='text1' placeholder="请输入文本" required/>
			</view>
		</view>
		<view class="jc-section">
			<view class="jc-section-header">
				<text>自定义类型</text>
			</view>
			<view class="jc-section-body">
				<jc-input label="文本" v-model='text1' placeholder="请输入文本" />
				<jc-input label="手机号" type="digit" v-model='text2' maxlength="11" placeholder="请输入手机号" />
				<jc-input label="密码" type="password" v-model='text3' placeholder="请输入密码" />
			</view>
		</view>
		<view class="jc-section">
			<view class="jc-section-header">
				<text>禁用输入框</text>
			</view>
			<view class="jc-section-body">
				<jc-input label="文本" v-model='text4' placeholder="请输入文本" readonly/>
				<jc-input label="文本"  v-model='text5' placeholder="请输入文本" disabled/>
			</view>
		</view>
		<view class="jc-section">
			<view class="jc-section-header">
				<text>密码输入框</text>
			</view>
			<view class="jc-section-body">
				<jc-input label="密码" v-model='text4' placeholder="请输入密码" show-password>
				</jc-input>
			</view>
		</view>
		<view class="jc-section">
			<view class="jc-section-header">
				<text>显示图标</text>
			</view>
			<view class="jc-section-body">
				<jc-input left-icon="help-l" label="文本" v-model='text4' placeholder="请输入文本" readonly/>
				<jc-input label="文本" v-model='text4' placeholder="请输入文本" readonly>
					<template #leftIcon>
						<image src="@/static/logo.png" mode="" class="label-icon-img"></image>
					</template>
				</jc-input>
				<jc-input right-icon="help-l" label="文本" v-model='text4' placeholder="请输入文本" readonly/>
				<jc-input label="文本" v-model='text4' placeholder="请输入文本" readonly>
					<template #rightIcon>
						<image src="@/static/logo.png" mode="" class="label-icon-img"></image>
					</template>
				</jc-input>
			</view>
		</view>
		<view class="jc-section">
			<view class="jc-section-header">
				<text>插入按钮</text>
			</view>
			<view class="jc-section-body">
				<jc-input label="短信验证码" v-model='text6' maxlength="4" type="number" placeholder="请输入验证码">
					 <template #button>
					    <jc-button size="small" type="primary">发送验证码</jc-button>
					  </template>
				</jc-input>
				<jc-input label="文本" v-model='text6' maxlength="4" type="number" placeholder="请输入文本">
					 <template #button>
					    <jc-button color="#666" round plain size='mini'>标签</jc-button>
					  </template>
				</jc-input>
			</view>
		</view>
		<view class="jc-section">
			<view class="jc-section-header">
				<text>高度自适应</text>
			</view>
			<view class="jc-section-body">
				<jc-input label="留言" v-model='text7' type="textarea" border="none" placeholder="请输入留言" autoHeight />
			</view>
		</view>
		<view class="jc-section">
			<view class="jc-section-header">
				<text>显示字数统计</text>
			</view>
			<view class="jc-section-body">
				<jc-input label="留言" v-model='text7' type="textarea" border="none" placeholder="请输入留言" maxlength="100" showWordLimit />
			</view>
		</view>
		
		
	</view>
</template>

<script>
	import jcInput from '@/components/jc-input/jc-input.vue'
	import jcButton from '@/components/jc-button/jc-button.vue'
	export default {
		components: {
			jcInput,
			jcButton
		},
		data() {
			return {
				text1: '',
				text2: '',
				text3: '',
				text4: '输入框只读',
				text5: '输入框已禁止',
				text6: '',
				text7: ''
			}
		}
	}
</script>

<style lang="scss" scoped>
	.input-container {
		background-color: #f5f5f5;
		height: 100%;
		overflow: auto;
		.jc-section {
			display: flex;
			flex-direction: column;
			font-size: 28rpx;
			.jc-section-header{
				color: rgba(69, 90, 100, 0.6);
				margin: 20rpx 0;
				padding: 0 32rpx;
			}
			.jc-section-body{
				display: flex;
				flex-direction: column;
				color: #646566;
				background-color: #fff;
				padding: 0 40rpx;
				.label-icon-img{
					width: 30rpx;
					height: 30rpx;
				}
				.btn{
					height: 40rpx;
				}
			}
		}
	}
</style>
