<template>
	<view class="jc-radio" :class="{'jc-radio-disable': disabled}" @click="changeRadio">
		<view class="jc-radio-icon">
			<slot name="icon" v-if="$slots.icon"></slot>
			<jc-icon :name='icon' :size='iconSize' :color='color' v-else></jc-icon>
		</view>
		<text class="jc-radio-label">
			<slot></slot>
		</text>
	</view>
</template>

<script>
	import jcIcon from "@/components/jc-icon/jc-icon.vue"
	export default{
		name: 'jcRadio',
		components: { jcIcon },
		props: {
			name: {
				type: String,
				default: ''
			},
			checkedColor: {
				type: String,
				default: '#912222'
			},
			inCheckedcolor: {
			  type: String,
			  default: '#999999'
			},
			iconSize: {
				type: [Number,String],
				default: 30
			}
		},
		computed:{
			icon() {
				return this.isChecked ? 'radio-active' : 'radio';
			},
			color(){
				if(this.disabled){
					return '#DDDDDD';
				}
				return (this.isChecked ? this.checkedColor :  this.inCheckedcolor);
			},
			isChecked() {
				let parent = this.getParent()
				if(parent){
					if(parent.value === this.name){
						return true
					}else{
						return false;
					}
				}
				return false;
			},
			disabled(){
				let parent = this.getParent()
				return !!parent.disabled;
			}
		},
		data() {
			return {
				
			}
		},
		methods:{
			getParent(){
				let parent = this.$parent;
				while(parent){
					if(parent.$options._componentTag !== "jc-radio-group"){
						parent = parent.$parent;
					}else{
						return parent;
					}
				}
			},
			changeRadio(){
				const parent = this.getParent();
				if(this.disabled || parent.readOnly)return;
				parent.$emit('input',this.name)
			}
		}
	}
</script>

<style lang="scss" scoped>
	.jc-radio{
		display: flex;
		align-items: center;
		margin-right: 20rpx;	
	}
	.jc-radio-disable{
		color: #DDD;
	}
</style>
