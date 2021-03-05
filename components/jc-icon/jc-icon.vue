<template>
	<text :class="`jc-icon-${name}`" :style="{color: color,'font-size': size + 'px'}" @click="iconClick"></text>
</template>

<script>
	export default{
		name: 'jcIcon',
		props: {
			size: {
				type: [String,Number],
				default: 32
			},
			color: {
				type: String,
				default: '#333333'
			},
			name: {
				type: String
			}
		},
		methods:{
			iconClick(){
				this.$emit('click')
			}
		}
	}
</script>

<style scoped>
	@import url("./icon.css");
</style>
