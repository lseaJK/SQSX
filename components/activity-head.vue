<template>
	<view class="actheadBG">
		<view class="title">
			{{name}}
		</view>

		<view class="tools">
			<u-icon class="toolItems" name="camera" color="#fff" size="48"></u-icon>

				<u-toast ref="uToast"></u-toast>
				<u-search v-model="value"  @search="search" :shape="shape" :clearabled="clearabled" 
				:show-action="showAction" :input-align="inputAlign" @clear="clear" placeholder="关键词搜索" placeholder-color="rgb(249,224,222)" bg-color="rgb(231,123,109)" color="#fff"></u-search>

			<u-icon class="toolItems" name="scan" color="#fff" size="48"></u-icon>
		</view>
	</view>
</template>

<script>
	export default {
		name:"activity-head",
		props:{
			name:String
		},
		data() {
			return {
				//  搜索框参数
				value: '',
				shape: 'square',
				clearabled: true,
				showAction: false,
				inputAlign: 'left'
			};
		}
	}
</script>

<style lang="scss" scoped>
	.actheadBG {
		height: 208rpx;
		width: 750rpx;
		border-bottom-left-radius: 80rpx;
		border-bottom-right-radius: 80rpx;
		background-color: rgb(226, 62, 40);
		padding-top: 30rpx;
		color: #fff;

		.title {
			height: 60rpx;
			font-size: 32rpx;
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
