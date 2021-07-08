<template>
	<view class="actheadBG">
		<view class="title">
			{{name}}
		</view>

		<view class="tools">
			<u-icon class="toolItems" name="camera" color="#fff" size="48"></u-icon>

			<u-toast ref="uToast"></u-toast>
			<u-search v-model="value" @search="search" :shape="shape" :clearabled="clearabled" :show-action="showAction"
				:input-align="inputAlign" @clear="clear" placeholder="关键词搜索" placeholder-color="rgb(249,224,222)"
				bg-color="rgb(231,123,109)" color="#fff"></u-search>

			<u-icon class="toolItems" name="scan" color="#fff" size="48"></u-icon>
		</view>
	</view>
</template>
<script>
	export default {
		data() {
			return {
				name: "我的活动",

				//  搜索框参数
				value: '',
				shape: 'square',
				clearabled: true,
				showAction: false,
				inputAlign: 'left'

			}
		},
		//  监视搜索框的内容
		watch: {
			// 这里的演示为证明通过v-model绑定值，它是双向绑定的，意味着您无需监听change事件
			// 也能知道value值当前的内容
			key(val) {
				// console.log(val);
			}
		},
		methods: {
			//  搜索函数
			search(key) {
				this.$refs.uToast.show({
					title: '搜索内容为：' + key,
					type: 'success'
				})
			},
			clear() {
				// console.log(this.value);
			},

		}
	}
</script>

<style lang="scss" scoped>
	.actheadBG {
		height: 268rpx;
		width: 750rpx;
		border-bottom-left-radius: 80rpx;
		border-bottom-right-radius: 80rpx;
		background-color: rgb(226, 62, 40);
		padding-top: 55rpx;
		color: #fff;

		.title {
			height: 80rpx;
			font-size: 40rpx;
			letter-spacing: 10rpx;
			text-align: center;
			margin-bottom: 20rpx;
		}

		.tools {
			height: 70rpx;
			display: flex;

			.toolItems {
				margin: 0 50rpx;
			}
		}
	}
</style>
