<template>
	<!-- <navigate-head><view>111</view></navigate-head> -->
	<view>首页
	</view>
	
	
	
</template>

<script>
	// import navigateHead from "@/components/navigate-head";
	export default {
		data() {
			return {
				
			}
		},
		onLoad() {

		},
		mounted(){
		  uni.setNavigationBarColor({frontColor:'#ffffff', backgroundColor: '#d81e06'})
		  uni.setNavigationBarTitle({title:"首页"})
		},
		methods: {

		}
	}
</script>

<style>
	.content {
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
	}

	.logo {
		height: 200rpx;
		width: 200rpx;
		margin-top: 200rpx;
		margin-left: auto;
		margin-right: auto;
		margin-bottom: 50rpx;
	}

	.text-area {
		display: flex;
		justify-content: center;
	}

	.title {
		font-size: 36rpx;
		color: #8f8f94;
	}
</style>
