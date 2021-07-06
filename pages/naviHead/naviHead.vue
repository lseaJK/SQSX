<template>

	<view class="navheadBG">
		<view class="title">
			首页
		</view>

		<view class="tools">
			<!-- <image class="camera" src="../../static/拍照.png"></image> -->
			<u-icon class="toolItems" name="camera-fill" color="#fff" size="48"></u-icon>

			<u-search placeholder="关键词搜索" v-model="keyword" :clearabled="true" :show-action="false" shape="square"
				size="40"></u-search>

			<u-icon class="toolItems" name="scan" color="#fff" size="48"></u-icon>


		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				keyword: ''
			}
		},
		methods: {

		}
	}
</script>

<style lang="scss">
	.navheadBG {
		height: 240px;
		width: 750px;
		border-bottom-left-radius: 80px;
		border-bottom-right-radius: 80px;
		background-color: rgb(226,62,40);
		padding-top: 20px;
		color: #fff;

		.title {
			height:80px;
			font-size: 35px;
			letter-spacing: 10px;
			text-align: center;
		}

		.tools {
			height: 70px;
			display: flex;

			.toolItems {
				margin: 0 30px;
			}
		}
	}
</style>
