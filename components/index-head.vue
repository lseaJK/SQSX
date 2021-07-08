<template>
	<view class="navheadBG">
		<view class="title">
			{{name}}
		</view>

		<view class="tools">
			<u-icon class="toolItems" name="camera" color="#fff" size="48"></u-icon>

			<u-search v-model="value" @search="search" :shape="shape" :clearabled="clearabled" :show-action="false"
				:input-align="inputAlign" @clear="clear" placeholder="关键词搜索" placeholder-color="rgb(249,224,222)"
				bg-color="rgb(231,123,109)" color="#fff"></u-search>

			<u-icon class="toolItems" name="scan" color="#fff" size="48"></u-icon>

		</view>

		<view class="hint">
			<view class="u-demo-area">
				<u-toast :type="type" ref="uToast"></u-toast>
				<u-notice-bar :autoplay="autoplay" :playState="playState" :speed="speed" :list="list"
					:volumeIcon="volumeIcon" :duration="duration" :isCircular="isCircular"></u-notice-bar>
			</view>
		</view>

		<view class="banner">
			<image mode="widthFix" :src="src"></image>
		</view>
	</view>
</template>

<script>
	export default {
		name: "index-head",
		props: {
			name: String,
			src: String,
			list: Object
		},
		data() {
			return {
				//  搜索框参数
				value: '',
				shape: 'square',
				clearabled: true,
				inputAlign: 'left',
				show: true,
				//  横幅参数
				autoplay: false,
				type: 'warning',
				mode: 'horizontal',
				playState: 'play',
				speed: 100,
				duration: 2000,
				moreIcon: true,
				volumeIcon: true,
				isCircular: true,
				current: 0
			}
		},
		watch: {
			// 这里的演示为证明通过v-model绑定值，它是双向绑定的，意味着您无需监听change事件
			// 也能知道value值当前的内容
			value(val) {
				// console.log(val);
			}
		},
		methods: {
			//  搜索函数
			search(value) {
				this.$refs.uToast.show({
					title: '搜索内容为：' + value,
					type: 'success'
				})
			},
			clear() {
				// console.log(this.value);
			},
			//  横幅函数
			toast(title) {
				this.$refs.uToast.show({
					title: title,
					type: 'warning'
				})
			},

		}
	}
</script>

<style lang="scss" scoped>
	.navheadBG {
		position: relative;
		height: 360rpx;
		width: 750rpx;
		border-bottom-left-radius: 80rpx;
		border-bottom-right-radius: 80rpx;
		background-color: rgb(226, 62, 40);
		padding-top: 20rpx;
		color: #fff;

		.title {
			height: 80rpx;
			font-size: 35rpx;
			letter-spacing: 10rpx;
			text-align: center;
		}

		.tools {
			height: 70rpx;
			display: flex;

			.toolItems {
				margin: 0 50rpx;
			}
		}

		.hint {
			height: 75rpx;
			width: 748rpx;
			border: 1rpx solid rgb(250, 127, 45);
			position: absolute;
			top: 240rpx;
			background-color: rgb(254, 252, 235);
			color: rgb(250, 127, 45);
			padding-left: 32rpx;
			padding-right: 32rpx;
			text-align: bottom;
			z-index: 999;

		}

		.banner {
			margin: 32rpx;
			width: 686rpx;
			height: 260rpx;
			overflow: hidden;

		}
	}
</style>
