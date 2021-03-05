<template>
	<view class="picker-container">
		<jc-cell-group title="基础用法">
			<jc-cell title="选择器" isLink @click="openPicker('picker1')" :value='content1'></jc-cell>
		</jc-cell-group>
		<jc-cell-group title="多列选择">
			<jc-cell title="多列选择" isLink @click="openPicker('picker2')" :value='content2'></jc-cell>
			<jc-cell title="联动选择" isLink @click="openPicker('picker3')" :value='content3'></jc-cell>
		</jc-cell-group>

		<jc-picker ref='picker1' mode='selector' :columns='columns1' :defaultIndex='defaultIndex' @change='onChange1'></jc-picker>
		<jc-picker ref='picker2' mode='multiSelector' :columns='columns2' @change='onChange2'></jc-picker>
		<jc-picker ref='picker3' mode='multiSelector' :columns='columns3' @change='onChange3' :value='value'></jc-picker>
	</view>
</template>

<script>
	import jcCellGroup from '@/components/jc-cell-group/jc-cell-group.vue'
	import jcCell from '@/components/jc-cell/jc-cell.vue'
	import jcPicker from '@/components/jc-picker/jc-picker.vue'
	export default {
		components: {
			jcCellGroup,
			jcCell,
			jcPicker
		},
		data() {
			return {
				columns1: ['北京', '上海', '广州', '深圳', '郑州', '武汉', '成都'],
				content1: '',
				content2: '',
				content3: '',
				columns2: [{
						values: ['周一', '周二', '周三', '周四', '周五'],
						defaultIndex: 2,
					},
					{
						values: ['上午', '下午', '晚上'],
						defaultIndex: 1,
					}
				],
				value: ['浙江', '金华', '义乌市'],
				columns3: [{
						text: '浙江',
						children: [{
								text: '杭州',
								children: [{
									text: '西湖区'
								}, {
									text: '余杭区'
								}],
							},
							{
								text: '温州',
								children: [{
									text: '鹿城区'
								}, {
									text: '瓯海区'
								}],
							},
							{
								text: '金华',
								children: [{
									text: '金东区'
								}, {
									text: '武义县'
								}, {
									text: '义乌市'
								}]
							}
						],
					},
					{
						text: '福建',
						children: [{
								text: '福州',
								children: [{
									text: '鼓楼区'
								}, {
									text: '台江区'
								}],
							},
							{
								text: '厦门',
								children: [{
									text: '思明区'
								}, {
									text: '海沧区'
								}],
							},
						],
					},
				],
				defaultIndex: 1
			}
		},
		methods: {
			openPicker(name) {
				this.$refs[name].open()
			},
			onChange1(values, columns, index) {
				if (!isNaN(index)) {
					this.defaultIndex = index;
				}
				this.content1 = values.join('/');
			},
			onChange2(values, columns, index) {
				this.columns2 = columns;
				this.content2 = values.join('/')
			},
			onChange3(values, columns, index) {
				this.content3 = values.join('/')
			}
		}
	}
</script>

<style lang="scss" scoped>
</style>
