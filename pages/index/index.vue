<template>
	<index-head :name="name" :src="src" :list="list"></index-head>
	
	
	
</template>

<script>
	import indexHead from "@/components/index-head";
	export default {
		components:{
			indexHead
		},
		data() {
			return {
				name:"首页",
				src:"../../static/banner.png",
				list:["XXXX欢迎您","没有前端不好吗"]
				
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
