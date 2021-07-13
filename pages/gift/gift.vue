<template>
	<view>
		<score-head :name="name" :src="src" ></score-head>
		<!-- 五个图标功能 -->
		<view class="welcome">xx 现有积分：88</view>
		<view>
			<u-toast ref="uToast"></u-toast>
			<u-grid :col="4" :border="false" >
				<u-grid-item  v-for="(item,index) in typeList" :key="index">
					<view @click="changeGiftType(index)">
						<image class="iconimg" :src="item.img"></image>
						<view class="grid-text">{{item.name}}</view>
					</view>
				</u-grid-item>
			</u-grid>
		</view>
		<!-- 列表 -->
		<u-waterfall v-model="giftList" ref="uWaterfall" >
			<template v-slot:left="{ leftList }" >
				<view class="demo-warter" v-for="(item, index) in leftList" :key="item.id">
					<!-- 微信小程序需要hx2.8.11版本才支持在template中引入其他组件，比如下方的u-lazy-load组件 -->
					<view @click="goStudy(item.id)">
						<u-lazy-load threshold="-450" :image="item.image" :index="index"></u-lazy-load>
						<view class="demo-title">{{ item.name }}</view>
						<view class="demo-shop">{{ item.point }}</view>
						<view class="demo-like">
							<u-icon name="heart-fill" size="30" color="#d81e06"></u-icon>{{ item.like_num }}
						</view>
					</view>
				</view>
			</template>
			<template v-slot:right="{ rightList }">
				<view class="demo-warter" v-for="(item, index) in rightList" :key="item.id">
					<view @click="goStudy(item.id)">
						<u-lazy-load threshold="-450" :image="item.image" :index="index"></u-lazy-load>
						<view class="demo-title">{{ item.name }}</view>
						<view class="demo-shop">{{ item.point }}</view>
						<view class="demo-like">
							<u-icon name="heart-fill" size="30" color="#d81e06"></u-icon>{{ item.like_num }}
						</view>
					</view>
				</view>
			</template>
		</u-waterfall>
	</view>
</template>

<script>
	import scoreHead from "@/components/score-head";
	export default {
		components: {
			scoreHead
		},
		data() {
			return {
				name:"积分兑换",
				src:"/static/banner.png",
				typeList:[{
					name:'党建书籍',
					img:'/static/gift/书籍.png'},
					{
					name:'党建纪念品',
					img:'/static/gift/礼品.png'},
					{
					name:'党建邮票',
					img:'/static/gift/礼品.png'},
					{
					name:'文创礼品',
					img:'/static/gift/文创云07.png'},
				],
				giftList: [{
							id:0,
							name: 'undo学习课件111',
							point: '66',
							image: '/static/member/兑换.png',
							like_num: 11,
						},
						{
							id:0,
							name: 'undo学习课件111',
							point: '66',
							image: '/static/member/兑换.png',
							like_num: 11,
						},
						{
							idx:2,
							id:0,
							name: 'undo学习课件111',
							point: '66',
							image: '/static/member/兑换.png',
							like_num: 11,
						},
						{
							id:0,
							name: 'undo学习课件111',
							point: '66',
							image: '/static/member/兑换.png',
							like_num: 11,
						},
					]
				
			};
		},
		methods:{
			changeGiftType(index){
				console.log("gift:",index);
			}
		}
	}
</script>

<style lang="scss">
	.welcome {
		margin-top: 110rpx;
		margin-left: 40rpx;
		font-size: 40rpx;
		line-height: 60rpx;
	}
.iconimg {
		width: 80rpx;
		height: 80rpx;
		overflow: hidden;
	}

	.grid-text {
		margin-top: 6rpx;
		font-size: 24rpx;
		line-height: 32rpx;
		color: $u-type-info;
	}
	
	//block
	.thumb-box {
		width: 33.333333%;
		display: flex;
		align-items: center;
		justify-content: center;
		flex-direction: column;
		margin-top: 20rpx;
	}
	
	.item-menu-image {
		width: 120rpx;
		height: 120rpx;
	}
	.demo-warter {
		border-radius: 8px;
		margin: 5px;
		background-color: #ffffff;
		padding: 8px;
		position: relative;
		width: 335rpx;
	}
	.demo-title {
		margin-top: 5rpx;
		color: $u-main-color;
		word-break: break-all;
		font-family: PingFangSC-Medium;
		font-size: 26rpx;
		color: #333333;
		text-align: justify;
		line-height: 34px;
		overflow: hidden;
	}
	
	.demo-like {
		height: 40rpx;
		color: #999999;
		line-height: 40rpx;
		font-size: 24rpx;
	}
	
	.demo-shop {
		font-family: PingFangSC-Regular;
		font-size: 24rpx;
		line-height: 50rpx;
		color: #999999;
		text-align: justify;
		text-overflow: ellipsis;
		white-space: nowrap;
		overflow: hidden;
	
	}
</style>
