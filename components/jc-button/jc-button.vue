<template>
	<view class="jc-btn" :class="[
		{'jc-btn-plain': plain},
		{'jc-btn-square': square},
		{'jc-btn-round': round},
		{'jc-btn-disabled': disabled},
		btnClassObj
	]"
	 :style="btnStyleObj" @click="btnClick">
		<view class="btn-icon" v-if="icon">
			<jc-icon size='20' :color="iconColor" :name='icon' ></jc-icon>
		</view>
		<!-- <text class="btn-icon" :class="`jc-icon-${icon}`" v-if="icon"></text> -->
		<view v-if="$slots.default || text" :style="iconStyleObj" class="btn-text">
			<slot v-if="$slots.default"></slot>
			<text v-else>{{text?text: ''}}</text>
		</view>
		
	</view>
</template>

<script>
	import jcIcon from '@/components/jc-icon/jc-icon.vue';
	export default {
		name: 'jcButton',
		components: {
			jcIcon
		},
		props: {
			type: {
				type: String,
				default: 'default'
			},
			size: {
				type: String,
				default: 'normal'
			},
			text: {
				type: String
			},
			color: {
				type: String
			},
			bgColor: {
				type: String
			},
			icon: {
				type: String
			},
			plain: {
				type: Boolean,
				default: false
			},
			square: {
				type: Boolean,
				default: false
			},
			round: {
				type: Boolean,
				default: false
			},
			disabled: {
				type: Boolean,
				default: false
			}
		},
		computed: {
			iconStyleObj(){
				if(this.icon){
					return {
						"margin-left": '6rpx'
					}
				}
				
			},
			iconColor() {
				const colorData = {
					'default': '#ddd',
					'primary': '#0cc15f', 
					'info':'#1b89fa',
					'warning': '#ff976a',
					'danger': '#ee0d23'
				};
				if(this.type){
					return colorData[this.type]
				}
			},
			btnClassObj() {
				let name = `jc-btn-${this.type}`
				return {
					[name]: this.type.length > 0
				}
			},
			btnStyleObj() {
				let fontSize = '32rpx';
				let styleObj = {};
				if (this.size === 'large') {
					styleObj['font-size'] = '36rpx';
					styleObj['padding'] = '20rpx 36rpx';
				} else if (this.size === 'small') {
					styleObj['font-size'] = '30rpx';
					styleObj['padding'] = '4rpx 24rpx';
				} else if (this.size === 'mini') {
					styleObj['font-size'] = '24rpx'
					styleObj['padding'] = '2rpx 28rpx';
				}
				if (this.type === 'default') {
					if (this.plain) {
						styleObj['color'] = this.color;
						styleObj['border'] = `2rpx solid ${this.color}`;
						return styleObj;
					} else {
						if (this.color) {
							styleObj['color'] = '#fff';
							styleObj['background-color'] = this.color;
							return styleObj;
						}
					}
				} else {
					return styleObj
				}
			}
		},
		methods:{
			btnClick(){
				this.$emit('click')
			}
		}
	}
</script>

<style lang="scss" scoped>
	$bgColors: ('default': #fff, 'primary':#0cc15f, 'info':#1b89fa, 'warning': #ff976a, 'danger':#ee0d23);
	$colors: ('default':#666, 'primary':#fff, 'info':#fff, 'warning': #fff, 'danger':#fff);
	$borderColors: ('default': #ddd, 'primary':#0cc15f, 'info':#1b89fa, 'warning': #ff976a, 'danger':#ee0d23);

	@each $name,
	$bgColor in $bgColors {
		.jc-btn-#{$name} {
			background-color: $bgColor;
			color: map-get($colors, $name);
			border: 2rpx solid map-get($borderColors, $name);

			&.jc-btn-plain {
				background-color: #fff;
				color: map-get($borderColors, $name)
			}
		}

	}

	.jc-btn {
		font-size: $jc-font-size-base;
		display: flex;
		justify-content: center;
		align-items: center;
		padding: 18rpx 32rpx;
		position: relative;
		transition: opacity 0.2s;
		border-radius: 4rpx;
		&::before {
			position: absolute;
			top: 50%;
			left: 50%;
			width: 100%;
			height: 100%;
			transform: translate(-50%, -50%);
			content: ' ';
			border-color: #000;
			background-color: #000;
			opacity: 0;
			border-radius: inherit;
		}

		&:active::before {
			opacity: 0.1;
		}

		&.jc-btn-round {
			border-radius: 999rpx;
		}

		&.jc-btn-square {
			border-radius: 0;
		}

		&.jc-btn-disabled {
			opacity: $jc-opacity-disabled;

			&:active::before {
				opacity: 0;
			}
		}
		.btn-text{
			display: flex;
			align-items: center;
		}
	}
</style>
