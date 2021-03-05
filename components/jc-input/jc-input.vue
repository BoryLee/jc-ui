<template>
	<view class="jc-input-container" :style="borderStyleObj" :class="{'jc-input-disable':disabled}">
		<view class="jc-input-label" :style="labelStyleObj">
			<label v-if="label" class="label-txt">{{label}}</label>
			<text v-if="required" class="require-txt">*</text>
			<slot v-if="$slots.leftIcon" name="leftIcon"></slot>
			<template  v-else>
				<jc-icon :name='leftIcon' color='#333' size='14' v-if="leftIcon"></jc-icon>
			</template>
		</view>
		<view class="jc-input-inner">
			<view class="jc-input-content">
				<template v-if="type === 'textarea'">
					<textarea class="jc-textarea" :style="textareaStyleObj" :value="value" :placeholder="placeholder"
					 :placeholder-class="placeholderClass" @input="input" :maxlength="maxlength" :disabled="disabled" v-if="!readonly"
					 :autoHeight='autoHeight' />
					<text class="jc-textarea" v-else>{{value}}</text>
					<text v-if="showWordLimit" class="limit-word-txt">{{limitWord}}/{{maxlength}}</text>
				</template>
				<template v-else>
					<input class="jc-input" :type="showType" :value="value" :placeholder="placeholder" :placeholder-class="placeholderClass"@input="input" :maxlength="maxlength" :disabled="disabled" v-if="!readonly" :focus='autofocus' @focus="inputFocus"/>
					<text class="jc-input" v-else>{{value}}</text>
					<jc-icon name='close' color='#ddd' size='16' v-if="isShowClear" @click='clear'></jc-icon>
					<jc-icon :name='passwordIcon' color='#ddd' size='16' v-if="showPassword" @click='changePasswordIcon'></jc-icon>
					<slot name="button"></slot>
				</template>
				<slot v-if="$slots.rightIcon" name="rightIcon"></slot>
				<jc-icon :name='rightIcon' color='#333' size='14' v-else></jc-icon>
			</view>
		</view>
	</view>
</template>

<script>
	import jcIcon from '@/components/jc-icon/jc-icon.vue'
	export default{
		name: 'jcInput',
		components: { jcIcon },
		props: {
			label: {
				type: String,
				default: ''
			},
			labelWidth: {
				type: [String,Number],
				default: 180
			},
			leftIcon: {
				type: String,
				default: ''
			},
			rightIcon: {
				type: String,
				default: ''
			},
			name: {
				type: String,
				default: ''
			},
			required: {
				type: Boolean,
				default: false
			},
			value: {
				type: String,
				default: ''
			},
			type: {//text,textarea, number,password
				type: String,
				default: 'text'
			},
			placeholder: {
				type: String,
				default: ''
			},
			placeholderClass: {
				type: String,
				default: 'jc-placeholder'
			},
			clearable: {
				type: Boolean,
				default: false
			},
			border: {//none 不显示边框  normal top bottom 
				type: String,
				default: 'bottom'
			},
			borderColor: {
				type: String,
				default: '#f5f5f5'
			},
			maxlength: {//输入的最大字符数
				type: [String,Number],
				default: -1
			},
			disabled: {//是否禁止输入
				type: Boolean,
				default: false
			},
			readonly:{//是否只读
				type: Boolean,
				default: false
			},
			autofocus: {
				type: Boolean,
				default: false
			},
			autoHeight: {//是否自适应内容高度，只对 textarea 有效
				type: Boolean,
				default: false
			},
			showWordLimit: { //是否显示字数统计，需要设置maxlength属性,只对 textarea 有效
				type: Boolean,
				default: false
			},
			showPassword: {
				type: Boolean,
				default: false
			},
			rules: {
				type: Array,
				default: () => []
			},
			errorMessage:{
				type: String,
				default: '11111'
			}
		},
		watch:{
			type(){
				this.getShowType()
			},
			value(){
				this.formatValue()
			}
		},
		computed: {
			isShowClear(){
				if(this.disabled || this.readonly) return false;
				if(this.clearable && this.value.length)return true;
			},
			labelStyleObj(){
				let styleObj = {};
				styleObj['width'] = `${this.labelWidth}rpx`
				if(this.type === 'textarea'){
					styleObj['align-items'] =  'flex-start';
				}
				return styleObj;
			},
			textareaStyleObj(){
				if(!this.autoHeight){
					return {
						height: '200rpx'
					}
				}else{
					return {
						height: 'auto'
					}
				}
			},
			borderStyleObj(){
				let styleObj = {};
				if(this.type === 'textarea'){
					if(this.border === 'none'){
						styleObj['border'] = 'none';
						styleObj['padding'] = '0 10rpx'
					}else{
						styleObj['border'] = `2rpx solid ${this.borderColor}`
						styleObj['border-radius'] = `8rpx`
						styleObj['padding'] = '0 10rpx';
					}
				}else{
					if(this.border === 'normal'){
						styleObj['border'] = `2rpx solid ${this.borderColor}`
						styleObj['border-radius'] = `8rpx`
						styleObj['padding'] = '0 10rpx'
					}else if(this.border === 'top'){
						styleObj['border-top'] = `2rpx solid ${this.borderColor}`
					}else if(this.border === 'bottom'){
						styleObj['border-bottom'] = `2rpx solid ${this.borderColor}`
					}else{
						styleObj['border'] = 'none'
					}
				}
				return styleObj;
			},
			limitWord(){
				return this.value.length;
			},
			passwordIcon(){
				if(this.showPassword){
					if(this.showType === 'password'){
						return 'eye-c-l'
					}else{
						return 'eye-o-l'
					}
				}
			}
		},
		data() {
			return {
				showType: 'text'
			}
		},
		methods:{
			formatValue(){
				let value = this.value
				this.$emit('input',value)
			},
			inputFocus(e){
				console.log('1111',e);
			},
			input(e){
				if(this.readonly) return;
				let value = e.detail.value;
				console.log('222',e);
				if(this.type === 'digit'){
					let regExp = /[^-0-9]/g;
					value = value.replace(regExp, '');
				}
				this.$emit('input',value)
			},
			clear(){
				this.$emit('input','')
			},
			getShowType(){
				if(this.showPassword){
					this.showType = 'password'
				}else{
					this.showType = this.type
				}
			},
			changePasswordIcon(){
				if(this.showPassword){
					if(this.showType === 'password'){
						this.showType = 'text'
					}else{
						this.showType = 'password'
					}
				}
			}
		},
		mounted(){
			this.getShowType()
		}
		
	}
</script>

<style lang="scss" scoped>
	$input-font-size: 28rpx;
	.jc-input-container{
		width: 100%;
		display: flex;
		color: #333;
		font-size: $input-font-size;
		overflow: hidden;
		&.jc-input-disable{
			color: #DDDDDD;
		}
	}
	.label-txt,.require-txt{
		margin-right: 6rpx;
	}
	
	.jc-input-label{
		display: flex;
		align-items: center;
		padding: 26rpx 0;
		.require-txt{
			color: #f00;
		}
	}
	.jc-input-disable{
		.require-txt{
			color: #DDDDDD;
		}
	}
	.jc-input-inner{
		flex: 1;
		position: relative;
		display: flex;
		align-items: center;
		.error-msg{
			position: absolute;
			bottom: 0;
			left: 0;
			font-size: 16rpx;
			color: #f00;
		}
		.jc-input-content{
			position: relative;
			display: flex;
			align-items: center;
			width: 100%;
			// box-sizing: border-box;
			padding: 26rpx 0;
			.limit-word-txt{
				position: absolute;
				bottom: 10rpx;
				right: 20rpx;
			}
			.jc-textarea{
				flex: 1;
				width: 100%;
			}
			.jc-input{
				flex: 1;
				width: 100%;
			}
			.jc-placeholder{
				color: #999;
				font-size: $input-font-size
			}
		}
		
	}
	
</style>
