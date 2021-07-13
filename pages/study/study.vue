<template>
	<view>
		<activity-head :name="name"></activity-head>
		<!-- 分类滑块 -->
		<u-grid :col="2" :border="false">
			<u-grid-item @click="changetoVideo()">
				<u-icon name="play-circle-fill" :size="66" color="#5677fc" v-if="type=='video'?true:false"></u-icon>
				<u-icon name="play-circle" :size="66" v-if="type!='video'?true:false"></u-icon>
				<!-- <image class="iconimg" src="/static/index/待阅.png"></image> -->
				<view class="grid-text">视频课件</view>
			</u-grid-item>
			<u-grid-item @click="changetoBook()">
				<!-- <image class="iconimg" src="/static/index/点评.png" ></image> -->
				<u-icon name="file-text-fill" :size="66" color="rgb(255,186,0)" v-if="type=='book'?true:false"></u-icon>
				<u-icon name="file-text" :size="66" v-if="type!='book'?true:false"></u-icon>
				<view class="grid-text">电子书籍</view>
			</u-grid-item>
		</u-grid>
		<!-- 视频列表 -->
		<view class="videoframe">
			<u-waterfall v-model="flowList" ref="uWaterfall" v-if="type=='video'?true:false">
				<template v-slot:left="{ leftList }">
					<view class="demo-warter" v-for="(item, index) in leftList" :key="index">
						<!-- 微信小程序需要hx2.8.11版本才支持在template中引入其他组件，比如下方的u-lazy-load组件 -->
						<view @click="goStudy(item.id)">
							<u-lazy-load threshold="-450" :image="item.image" :index="index"></u-lazy-load>
							<view class="demo-title">{{ item.title }}</view>
							<view class="demo-shop">{{ item.content }}</view>
							<view class="demo-like">
								<u-icon name="heart-fill" size="40" color="#d81e06"></u-icon>{{ item.like_num }}
							</view>
						</view>
					</view>
				</template>
				<template v-slot:right="{ rightList }">
					<view class="demo-warter" v-for="(item, index) in rightList" :key="index">
						<view @click="goStudy(item.id)">
							<u-lazy-load threshold="-450" :image="item.image" :index="index"></u-lazy-load>
							<view class="demo-title">{{ item.title }}</view>
							<view class="demo-shop">{{ item.content }}</view>
							<view class="demo-like">
								<u-icon name="heart-fill" size="40" color="#d81e06"></u-icon>{{ item.like_num }}
							</view>
						</view>
					</view>
				</template>
			</u-waterfall>
			<!-- <u-loadmore bg-color="rgb(240, 240, 240)" :status="loadStatus" @loadmore="addRandomData"></u-loadmore> -->
			<!-- 弹出课件详情 -->
		</view>
		<!-- #视频列表 -->
		
		<!-- 书籍列表 -->
		<view v-for="(item, index) in bookList" :key="index" v-if="type=='book'?true:false">
			<view class="u-flex user-box u-p-l-30 u-p-r-20 u-p-b-30">
				<view class="u-m-r-10">
					<u-avatar :src="item.img" size="120"></u-avatar>
				</view>
				<view class="u-flex-1">
					<view class="u-font-28 u-p-b-20" style="line-height: 60rpx;height: 60rpx;">{{item.title}}</view>
					<u-button :plain="plain" shape="circle" size="mini" :ripple="false" :hairLine="true" type="warning">
						{{item.type}}
					</u-button>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	import activityHead from "@/components/activity-head";
	
	export default {
		components: {
			activityHead,
		},
		data() {
			return {
				name: "学习课件",
				//tab
				type: "video",
				tabs_current: 0,
				tabs_list: [{
					name: '视频课件'
				}, {
					name: '电子书籍'
				}],
				//waterfall
				loadStatus: 'loadmore',
				flowList: [],
				//booklist
				bookList: [{
						id: 0,
						title: '标题',
						img: '/static/index/活动.png',
						type: '类别'
					},
					{
						id: 1,
						title: '标题',
						img: '/static/index/活动.png',
						type: '类别'
					},
				],
				//弹出层
				show: false,
				openIndex: 0,
				list: [{
						id: 1,
						title: '学习课件111',
						content: '内容简介',
						image: '/static/member/兑换.png',
						url: '',
						chat_num: 0,
						share_num: 0,
						like_num: 11,
					},
					{
						id: 2,
						title: '学习课件222',
						content: '内容简介',
						chat_num: 0,
						share_num: 0,
						like_num: 22,
						image: '/static/member/兑换.png',
						url: ''
					},
					{
						id: 3,
						title: '学习课件333',
						content: '内容简介',
						chat_num: 0,
						share_num: 0,
						like_num: 33,
						image: '/static/member/兑换.png',
						url: ''
					},
					{
						id: 4,
						title: '学习课件444',
						content: '内容简介',
						chat_num: 0,
						share_num: 0,
						like_num: 44,
						image: '/static/member/兑换.png',
						url: ''
					},
				]
			};
		},
		onLoad() {
			this.addRandomData();
			this.changetoVideo();
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
			//tab
			tabs_change(index) {
				// this.chang_list=false;
				this.tabs_current = index;
				// this.getCata(index);
				console.log("index", index);
				// this.list=this.donelist;

			},
			changetoVideo() {
				//获取列表
				this.type = "video";
				console.log("type", this.type);
			},
			changetoBook() {
				//获取列表
				this.type = "book";
				console.log("type", this.type);
			},
			addRandomData() {
				for (let i = 0; i < this.list.length; i++) {
					// let index = this.$u.random(0, this.list.length - 1);
					let index = this.list[i].id - 1;
					// 先转成字符串再转成对象，避免数组对象引用导致数据混乱
					let item = JSON.parse(JSON.stringify(this.list[index]));
					item.id = index + 1;
					this.flowList.push(item);
				}
			},
			clear() {
				this.$refs.uWaterfall.clear();
			},
			goStudy(id) {
				this.show = true;
				this.openIndex = id;
				console.log('item.id:', id);
			},
			close() {
				// console.log('close');
			},
			open() {
				// console.log('open');
			},
		},

		mounted() {
			uni.setNavigationBarColor({
				frontColor: '#ffffff',
				backgroundColor: '#d81e06'
			})
			uni.setNavigationBarTitle({
				title: "学习课件"
			})
		}
	}
</script>

<style lang="scss" scoped>
	.videoframe {
		padding-left: 22rpx;
		padding-right: 22rpx;
	}
.popframe {
			padding-top: 53rpx;
			padding-left: 13rpx;
			padding-right: 13rpx;
			margin-bottom: 52rpx;
		
			.popinfo {
				padding-left: 30rpx;
				padding-right: 30rpx;
		
				.poptitle {
					font-family: PingFangSC-Medium;
					font-size: 34rpx;
					color: #333333;
					text-align: left;
				}
		
				.popcontent {
					margin-top: 9rpx;
					font-family: PingFangSC-Light;
					font-size: 28rpx;
					color: #999999;
					text-align: left;
				}
		
				.popicon {
					font-family: PingFangSC-Regular;
					font-size: 20rpx;
					color: #000000;
					margin-top: 10rpx;
					margin-bottom: 30rpx;
		
					.iconItem {
						margin-right: 10rpx;
					}
		
					.textItem {
						margin-right: 14rpx;
					}
				}
			}
		
			.popimg {
				width: 626rpx;
				margin: 0 auto;
			}
		}
	.iconimg {
		width: 130rpx;
		height: 130rpx;
		overflow: hidden;
		// background-color: #18B566;
	}

	.grid-text {
		font-size: 35rpx;
		margin-top: 4rpx;
		color: $u-type-info;
	}

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

	.demo-img-wrap {}

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

	.demo-like {}

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

	.tagitem {
		margin-right: 10rpx;
		margin-bottom: 10rpx;
	}
</style>
