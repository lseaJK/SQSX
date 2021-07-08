<template>
	<view>
			<u-waterfall v-model="flowList" ref="uWaterfall">
					<template v-slot:left="{ leftList }">
						<view class="demo-warter" v-for="(item, index) in leftList" :key="index" >
							<!-- 微信小程序需要hx2.8.11版本才支持在template中引入其他组件，比如下方的u-lazy-load组件 -->
							<view @click="goStudy(item.id)">
								<u-lazy-load threshold="-450" :image="item.image" :index="index"></u-lazy-load>
									<view class="demo-title">{{ item.title }}</view>
									<view class="demo-shop">{{ item.content }}</view>
									<view class="demo-like"><u-icon name="heart-fill" size="40" color="#d81e06"></u-icon>{{ item.like_num }}</view>
							</view>
						</view>
					</template>
					<template v-slot:right="{ rightList }" >
						<view class="demo-warter" v-for="(item, index) in rightList" :key="index">
							<view @click="goStudy(item.id)">
								<u-lazy-load threshold="-450" :image="item.image" :index="index"></u-lazy-load>
									<view class="demo-title">{{ item.title }}</view>
									<view class="demo-shop">{{ item.content }}</view>
									<view class="demo-like"><u-icon name="heart-fill" size="40" color="#d81e06"></u-icon>{{ item.like_num }}</view>
							</view>
						</view>
					</template>
				</u-waterfall>
				<!-- <u-loadmore bg-color="rgb(240, 240, 240)" :status="loadStatus" @loadmore="addRandomData"></u-loadmore> -->
	<!-- 弹出课件详情 -->
	<u-popup border-radius="10" v-model="show"
		@close="close" @open="open" mode="center"
		length="80%" mask="true"
		closeable="true"
		close-icon-pos="top-right"
		close-icon-color="#d81e06"
	>
<!-- 	<view style="height: 400rpx">
		<view class="close-btn">
			<u-button @click="show = false;" size="medium">关闭弹窗</u-button>
		</view>
	</view> -->
	<view style="height: 800rpx">
		<view> 标题：{{list[openIndex].title}}</view>
		<view> 内容：{{list[openIndex].content}}</view>
		<image :src='list[openIndex].image'></image>
	<view class="u-icon-item u-border-bottom u-border-right icon-box">
						 	<u-icon name="chat" size="40" color="#909399"></u-icon>&nbsp;&nbsp;{{list[openIndex].chat_num}}&nbsp;&nbsp;
							<u-icon name="share" size="40" color="#909399"></u-icon>&nbsp;&nbsp;{{list[openIndex].share_num}}&nbsp;&nbsp;
							<u-icon name="heart" size="40" color="#909399"></u-icon>&nbsp;&nbsp;{{list[openIndex].like_num}}
	</view>
		<!-- 评论 -->
		<view>

		</view>
	</view>
	</u-popup>
	</view>
</template>

<script>
	export default {
		data() {
				return {
					loadStatus: 'loadmore',
					flowList: [],
					//弹出层
					show:false,
					openIndex:0,
					list: [
						{
							id:1,
							title: '学习课件111',
							content:'内容简介',
							image: '/static/member/兑换.png',
							url:'',
							chat_num:0,
							share_num:0,
							like_num:11,
						},
						{
							id:2,
							title: '学习课件222',
							content:'内容简介',
							chat_num:0,
							share_num:0,
							like_num:22,
							image:  '/static/member/兑换.png',
							url:''
						},
					{
						id:3,
						title: '学习课件333',
						content:'内容简介',
						chat_num:0,
						share_num:0,
						like_num: 33,
						image: '/static/member/兑换.png',
						url:''
					},
					{
						id:4,
						title: '学习课件444',
						content:'内容简介',
						chat_num:0,
						share_num:0,
						like_num: 44,
						image: '/static/member/兑换.png',
						url:''
					},
					]
				};
			},
			onLoad() {
				this.addRandomData();
			},
			onReachBottom() {
				this.loadStatus = 'loading';
				// 模拟数据加载
				setTimeout(() => {
					// this.addRandomData();
					this.loadStatus = 'loadmore';
				}, 1000);
			},
			methods: {
				addRandomData() {
					for (let i = 0; i < this.list.length; i++) {
						// let index = this.$u.random(0, this.list.length - 1);
						let index = this.list[i].id-1;
						// 先转成字符串再转成对象，避免数组对象引用导致数据混乱
						let item = JSON.parse(JSON.stringify(this.list[index]));
						item.id = index+1;
						this.flowList.push(item);
					}
				},
				clear() {
					this.$refs.uWaterfall.clear();
				},
				goStudy(id){
					this.show = true;
					this.openIndex=id;
					console.log('item.id:',id);
				},
				close() {
					// console.log('close');
				},
				open() {
					// console.log('open');
				},
			},

		mounted() {
			uni.setNavigationBarColor({frontColor:'#ffffff', backgroundColor: '#d81e06'})
			uni.setNavigationBarTitle({title:"学习课件"})
		}
	}
</script>

<style lang="scss" scoped>
.demo-warter {
	border-radius: 8px;
	margin: 5px;
	background-color: #ffffff;
	padding: 8px;
	position: relative;
}

.u-close {
	position: absolute;
	top: 32rpx;
	right: 32rpx;
}

.demo-img-wrap {
}

.demo-image {
	width: 100%;
	border-radius: 4px;
}

.demo-title {
	font-size: 30rpx;
	margin-top: 5px;
	color: $u-main-color;
	word-break: break-all;
}
.demo-like{

}
.demo-shop {
	font-size: 22rpx;
	color: $u-tips-color;
	margin-top: 10px;
	margin-bottom: 10px;
}
//弹出
	.wrap {
		padding: 24rpx;
	}

	.close-btn {
		height: 100%;
		display: flex;
		align-items: center;
		justify-content: center;
	}
</style>

