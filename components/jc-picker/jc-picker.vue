<template>
	<view class="">
		<jc-popup ref='popup' position='bottom' round>
			<view class="jc-picker">
				<view class="jc-picker-toolbar" v-if="showToolbar">
					<text class="jc-picker-btn jc-picker-cancel" :style="{color: cancelButtonColor}" @click="cancel">{{cancelButtonText}}</text>
					<view class="jc-ellipsis jc-picker-title">{{title}}</view>
					<text class="jc-picker-btn jc-picker-confirm" :style="{color: confirmButtonColor}" @click="confirm">{{confirmButtonText}}</text>
				</view>
				<view class="jc-picker-coumns">
					<picker-view class="jc-picker-view" indicator-style="height: 80rpx;" :value="multiArray" @change="bindChange">
						<template v-if="mode === 'selector'">
							<picker-view-column>
								<view class="item" v-for="(item,index) in showColumns" :key="index">
									{{ item[keyValue] ?  item[keyValue] : item }}
								</view>
							</picker-view-column>
						</template>
						<template v-else>
							<block v-for="(column,columnIndex) in showColumns" :key='columnIndex'>
								<picker-view-column>
									<view class="item" v-for="(item,index) in column" :key="index">
										{{ item[keyValue] ?  item[keyValue] : item }}
									</view>
								</picker-view-column>
							</block>
						</template>
					</picker-view>
				</view>

			</view>
		</jc-popup>
	</view>
</template>

<script>
	import jcPopup from '@/components/jc-popup/jc-popup.vue'
	export default {
		name: 'jcPicker',
		components: {
			jcPopup
		},
		props: {
			mode: {
				type: String,
				default: 'selector'
			},
			confirmButtonText: {
				type: String,
				default: '确定'
			},
			confirmButtonColor: {
				type: String,
				default: '#912222'
			},
			cancelButtonText: {
				type: String,
				default: '取消'
			},
			cancelButtonColor: {
				type: String,
				default: '#333333'
			},
			title: {
				type: String,
				default: '标题'
			},
			showToolbar: {
				type: Boolean,
				default: true
			},
			columns: {
				type: Array,
				default: () => []
			},
			keyValue: {
				type: String,
				default: 'text'
			},
			value: {
				type: Array,
				default: () => []
			},
			defaultIndex: {
				type: [String, Number],
				default: 0
			}
		},
		watch: {
			columns() {
				this.formateData()
			}
		},
		data() {
			return {
				showColumns: [],
				multiArray: []
			}
		},
		methods: {
			getData(columns) {
				let data = this.columns
				columns.forEach(column => {
					let array = data.map(item => item[this.keyValue]);
					this.showColumns.push(array);
					let index = array.findIndex(item => item === column);
					this.multiArray.push(index);
					if (data[index]['children']) {
						data = data[index]['children']
					}
				})
			},
			scrollData(multiArray) {
				this.showColumns = [];
				let data = this.columns
				let scrollIndex = this.getOneColumn(multiArray);
				multiArray = multiArray.map((item, index) => {
					if (index > scrollIndex) {
						return 0
					}
					return item
				})
				multiArray.forEach((multi, multiIndex) => {
					let array = data.map(item => item[this.keyValue]);
					this.showColumns.push(array);
					let len = array.length;
					let name = array[multi];
					// if(len - 1 < multi){
					// 	multiArray.splice(multiIndex,1,len-1)
					// 	name = array[len-1]
					// }else{
					// 	name = array[multi]
					// }
					let index = data.findIndex(item => item[this.keyValue] === name);
					if (data[index]['children']) {
						data = data[index]['children']
					}

				})
				return multiArray

			},
			getOneColumn(array) {
				for (let i = 0; i < array.length; i++) {
					if (array[i] != this.multiArray[i]) {
						return i
					}
				}
			},
			formateData() {
				this.showColumns = [];
				this.multiArray = [];
				const {
					columns
				} = this;
				if (this.mode === 'selector') {
					this.showColumns = columns;
					this.multiArray = [this.defaultIndex];
					this.multiData = [this.showColumns[this.multiArray[0]]]
					this.selectIndex = this.defaultIndex;
				} else if (this.mode === 'multiSelector') {
					if (this.value.length > 0) {
						this.getData(this.value)
					} else {
						columns.forEach((column) => {
							if (column['values']) {
								this.showColumns.push(column['values'])
							}
							if (!isNaN(column['defaultIndex'])) {
								this.multiArray.push(column['defaultIndex'])
							}
						})
					}
					this.multiData = this.multiArray.map((item, index) => {
						return this.showColumns[index][item]
					})
				}
			},
			open() {
				this.$refs['popup'].open();
			},
			confirm() {
				this.cancel()
				this.passData()
			},
			cancel() {
				this.$refs['popup'].close();
			},
			passData() {
				const {
					multiArray,
					multiData,
					selectIndex,
					columns
				} = this;
				let array = [];
				if (this.mode === 'multiSelector') {
					if (!this.value.length) {
						array = columns.map((item, index) => {
							item['defaultIndex'] = multiArray[index];
							return item;
						})
					}
				}

				this.$emit('change', multiData, array, selectIndex)
			},
			bindChange(e) {
				const {
					mode,
					columns
				} = this;
				let multiArray = e.detail.value;
				let multiData = [],
					selectIndex;
				if (mode === 'selector') {
					multiData = [this.showColumns[multiArray[0]]];
					selectIndex = multiArray[0];
				} else if (this.mode === 'multiSelector') {
					if (this.value.length > 0) {
						multiArray = this.scrollData(multiArray)
					}
					multiData = multiArray.map((item, index) => {
						return this.showColumns[index][item]
					})
				}
				this.multiArray = multiArray;
				this.multiData = multiData;
				this.selectIndex = selectIndex;
				if (!this.showToolbar) {
					this.passData()
				}
			},
		},
		mounted() {
			this.formateData()
		}
	}
</script>

<style lang="scss" scoped>
	.jc-ellipsis {
		overflow: hidden;
		white-space: nowrap;
		text-overflow: ellipsis;
	}

	.jc-picker {
		display: flex;
		flex-direction: column;
		height: 100%;

		.jc-picker-toolbar {
			display: flex;
			align-items: center;
			justify-content: space-between;
			height: 90rpx;
			font-size: 30rpx;
			border-bottom: 2rpx solid #f5f5f5;

			.jc-picker-title {
				max-width: 50%;
				font-weight: 500;
				font-size: 36rpx;
				text-align: center;
			}

			.jc-picker-btn {
				padding: 0 32rpx;
			}
		}

		.jc-picker-coumns {
			flex: 1;

			.jc-picker-view {
				height: 100%;
			}

			.item {
				height: 80rpx;
				line-height: 80rpx;
				text-align: center;
			}
		}
	}
</style>
