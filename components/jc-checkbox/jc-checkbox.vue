<template>
	<view class="jc-checkbox" :class="{'jc-checkbox-disable': disabled}" @click="changeCheckbox">
		<view class="jc-checkbox-icon">
			<slot name="icon" v-if="$slots.icon"></slot>
			<jc-icon :name='icon' :size='iconSize' :color='color' v-else></jc-icon>
		</view>
		<text class="jc-checkbox-label">
			<slot></slot>
		</text>
	</view>
</template>

<script>
	import jcIcon from "@/components/jc-icon/jc-icon.vue"
	export default{
		name: 'jcCheckbox',
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
				return this.isChecked ? 'checkbox-active' : 'checkbox';
			},
			color(){
				if(this.disabled){
					return '#DDDDDD';
				}
				return (this.isChecked ? this.checkedColor :  this.inCheckedcolor);
			},
			disabled(){
				let parent = this.getParent()
				return !!parent.disabled;
			}
		},
		watch:{
			name(){
				this.judgeChecked()
			}
		},
		data() {
			return {
				isChecked: false
			}
		},
		methods:{
			judgeChecked(){
				let parent = this.getParent();
				if(parent){
					if(parent.value.includes(this.name)){
						this.isChecked = true;
					}else{
						this.isChecked = false;
					}
				}
			},
			getParent(){
				let parent = this.$parent;
				while(parent){
					if(parent.$options._componentTag !== "jc-checkbox-group"){
						parent = parent.$parent;
					}else{
						return parent;
					} 
				}
			},
			changeCheckbox(){
				const parent = this.getParent();
				if(this.disabled || parent.readOnly)return;
				this.isChecked = !this.isChecked;
				let array = [];
				parent.$children[0].$children.forEach(child=>{
					if(child.isChecked){
						array.push(child.name)
					}
				})
				parent.$emit('input',array)
			}
		},
		mounted() {
			this.judgeChecked()
		}
	}
</script>

<style lang="scss" scoped>
	.jc-checkbox{
		display: flex;
		align-items: center;
		margin-right: 20rpx;	
	}
	.jc-checkbox-disable{
		color: #DDD;
	}
</style>
