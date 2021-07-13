<template>
	<view>
		<activity-head :name="name"></activity-head>

		<view class="mainframe">
			<!-- 分类滑块 -->
			<u-tabs :list="tabs_list" is-scroll="false" :current="tabs_current" @change="tabs_change" bar-width="66"
				active-color="#108EE9" font-size="30"></u-tabs>
			<!-- 活动分类 -->
			<view class="actCata">
				<view class="cataTitle">活动分类</view>
				<view class="cataContent">
					<u-toast ref="cataToast"></u-toast>
					<u-grid :col="col" @click="cataClick" :border="border">
						<block v-for="(cataitem,cataindex) of catalist" key="cataindex">
							<u-grid-item class="grid-item" index="cataindex" @click="cataitemClick">
								<view class="grid-text">{{cataitem}}</view>
							</u-grid-item>
						</block>
					</u-grid>
				</view>
			</view>
			<!-- #活动分类 -->
			<!-- 活动列表 -->
			<view class="actList" v-if="showDone">
				<view class="listTitle">活动列表</view>
				<view >
					<u-waterfall v-model="donelist" ref="uWaterfall" >
						<template v-slot:left="{ leftList }" >
							<view class="demo-warter" v-for="(item, index) in leftList" :key="index">
								<!-- 微信小程序需要hx2.8.11版本才支持在template中引入其他组件，比如下方的u-lazy-load组件 -->
								<view @click="goStudy(item.id)">
									<u-lazy-load threshold="-450" :image="item.image" :index="index"></u-lazy-load>
									<view class="demo-title">{{ item.title }}</view>
									<view class="demo-shop">{{ item.content }}</view>
									<view class="demo-like">
										<u-icon name="heart-fill" size="30" color="#d81e06"></u-icon>{{ item.like_num }}
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
										<u-icon name="heart-fill" size="30" color="#d81e06"></u-icon>{{ item.like_num }}
									</view>
								</view>
							</view>
						</template>
					</u-waterfall>
					<!-- <u-loadmore bg-color="rgb(240, 240, 240)" :status="loadStatus" @loadmore="addRandomData"></u-loadmore> -->
					<!-- 弹出课件详情 -->
					<u-popup border-radius="10" v-model="show" @close="close" @open="open" mode="center" width="680rpx"
						mask="true" closeable="true" close-icon-pos="top-right" close-icon-color="#d81e06">
						<view class="popframe">
							<view class="popinfo">
								<view class="poptitle">{{list[openIndex].title}}</view>
								<view class="popcontent">{{list[openIndex].content}}</view>
								<view class="u-icon-item u-border-bottom icon-box popicon">
									<u-icon class="iconItem" name="chat" size="30" color="rgb(79,149,236)"></u-icon>
									<text class="textItem">{{list[openIndex].chat_num}}</text>
									<u-icon class="iconItem" name="share" size="26" color="#000"></u-icon>
									<text class="textItem">{{list[openIndex].share_num}}</text>
									<u-icon class="iconItem" name="heart-fill" size="30" color="rgb(242,92,98)">
									</u-icon>
									<text class="textItem">{{list[openIndex].like_num}}</text>
								</view>
							</view>
							<view class="popimg">
								<image :src='list[openIndex].image' mode="aspectFit"></image>
							</view>
							<!-- 评论 -->
							<view>

							</view>
						</view>
					</u-popup>
				</view>
			</view>
			<!-- #活动列表 -->
			<!-- 活动列表 -->
			<view class="actList" v-if="showUndo">
				<view class="listTitle">活动列表</view>
				<view >
					<u-waterfall v-model="undolist" ref="uWaterfall" >
						<template v-slot:left="{ leftList }" >
							<view class="demo-warter" v-for="(item, index) in leftList" :key="item.id">
								<!-- 微信小程序需要hx2.8.11版本才支持在template中引入其他组件，比如下方的u-lazy-load组件 -->
								<view @click="goStudy(item.id)">
									<u-lazy-load threshold="-450" :image="item.image" :index="index"></u-lazy-load>
									<view class="demo-title">{{ item.title }}</view>
									<view class="demo-shop">{{ item.content }}</view>
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
									<view class="demo-title">{{ item.title }}</view>
									<view class="demo-shop">{{ item.content }}</view>
									<view class="demo-like">
										<u-icon name="heart-fill" size="30" color="#d81e06"></u-icon>{{ item.like_num }}
									</view>
								</view>
							</view>
						</template>
					</u-waterfall>
					<!-- <u-loadmore bg-color="rgb(240, 240, 240)" :status="loadStatus" @loadmore="addRandomData"></u-loadmore> -->
					<!-- 弹出课件详情 -->
					<u-popup border-radius="10" v-model="show" @close="close" @open="open" mode="center" width="680rpx"
						mask="true" closeable="true" close-icon-pos="top-right" close-icon-color="#d81e06">
						<view class="popframe">
							<view class="popinfo">
								<view class="poptitle">{{list[openIndex].title}}</view>
								<view class="popcontent">{{list[openIndex].content}}</view>
								<view class="u-icon-item u-border-bottom icon-box popicon">
									<u-icon class="iconItem" name="chat" size="30" color="rgb(79,149,236)"></u-icon>
									<text class="textItem">{{list[openIndex].chat_num}}</text>
									<u-icon class="iconItem" name="share" size="26" color="#000"></u-icon>
									<text class="textItem">{{list[openIndex].share_num}}</text>
									<u-icon class="iconItem" name="heart-fill" size="30" color="rgb(242,92,98)">
									</u-icon>
									<text class="textItem">{{list[openIndex].like_num}}</text>
								</view>
							</view>
							<view class="popimg">
								<image :src='list[openIndex].image' mode="aspectFit"></image>
							</view>
							<!-- 评论 -->
							<view>
			
							</view>
						</view>
					</u-popup>
				</view>
			</view>
			<!-- #活动列表 -->
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
				name: "我的活动",
				//tabs的参数
				tabs_current: 0,
				tabs_list: [{
					name: '已结束活动'
				}, {
					name: '未开始活动'
				}],
				//  grid的参数
				border: true,
				col: 3,
				catalist:  ['integral', 'kefu-ermai', 'coupon', 'gift', 'scan', 'pause-circle', 'wifi', 'email','list'],
				//'integral', 'kefu-ermai', 'coupon', 'gift', 'scan', 'pause-circle', 'wifi', 'email', 'list'
				// 【需要传值】活动的分类数组 
				// Flist: ['integral', 'kefu-ermai', 'coupon', 'gift', 'scan', 'pause-circle', 'wifi', 'email', 'list'],
				// Ulist: ,
				//  waterfall需要的数据
				compkey:1,
				loadStatus: 'loadmore',
				DoneflowList: [],
				UndoflowList: [],
				//弹出层
				show: false,
				openIndex: 0,
				showDone:true,
				showUndo:false,
				list:[],
				donelist: [{
						id:0,
						act_id: 1,
						title: '学习课件111',
						content: '内容简介font-family: PingFangSC-Regular;font-size: 24px;color:#999999;text-align:justify;777777777777',
						image: '/static/member/兑换.png',
						url: '',
						chat_num: 0,
						share_num: 0,
						like_num: 11,
					},
					{
						id:1,
						act_id: 2,
						title: '学习课件222',
						content: '内容简介',
						chat_num: 0,
						share_num: 0,
						like_num: 22,
						image: '/static/member/兑换.png',
						url: ''
					},
					{
						id:2,
						act_id: 3,
						title: '学习课件333',
						content: '内容简介',
						chat_num: 0,
						share_num: 0,
						like_num: 33,
						image: '/static/member/兑换.png',
						url: ''
					},
					{
						id:3,
						act_id: 4,
						title: '学习课件444',
						content: '内容简介',
						chat_num: 0,
						share_num: 0,
						like_num: 44,
						image: '/static/member/兑换.png',
						url: ''
					},
				],
				undolist: [{
						id:0,
						act_id: 1,
						title: 'undo学习课件111',
						content: '内容简介font-family: PingFangSC-Regular;font-size: 24px;color:#999999;text-align:justify;777777777777',
						image: '/static/member/兑换.png',
						url: '',
						chat_num: 0,
						share_num: 0,
						like_num: 11,
					},
					{
						id:1,
						act_id: 2,
						title: 'undo学习课件222',
						content: '内容简介',
						chat_num: 0,
						share_num: 0,
						like_num: 22,
						image: '/static/member/兑换.png',
						url: ''
					},
					{
						idx:2,
						act_id: 3,
						title: 'undo学习课件333',
						content: '内容简介',
						chat_num: 0,
						share_num: 0,
						like_num: 33,
						image: '/static/member/兑换.png',
						url: ''
					},
					{
						id:3,
						act_id: 4,
						title: 'undo学习课件444',
						content: '内容简介',
						chat_num: 0,
						share_num: 0,
						like_num: 44,
						image: '/static/member/兑换.png',
						url: ''
					},
				]
			}
		},
		onLoad() {
			this.getDoneUndoList();
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
			//访问后端
			getDoneUndoList(){//获取已结束和未开始的活动列表
				
			},
			//tabs
			// tabs_finished() {
			// 	return this.tabs_current == 0 ? true : false;
			// },
			tabs_change(index) {
				// this.chang_list=false;
				this.tabs_current = index;
				// this.getCata(index);
				console.log("index",index);
				// this.onLoad();
				if(index == 0){
					this.getDone();
				}
				else{
					this.getUndo();
				}
			
			},
			//已结束grid
			cataclick(index) {
				this.$refs.cataToast.show({
					title: `点击了第${index + 1}宫格`,
					type: 'warning'
				})
			},
			// 针对单个grid-item的事件
			cataitemClick(index) {
				// console.log(index);
			},
			//  获取分类标签，0表示已结束，1表示未开始
			getCata(index) {
				this.catalist = ['integral', 'kefu-ermai', 'coupon', 'gift', 'scan', 'pause-circle', 'wifi', 'email',
					'list'
				]
			},
			// waterfall
			getDone() {
				// this.DoneflowList= this.donelist;
				// for (let i = 0; i < this.donelist.length; i++) {
				// 	// let index = this.$u.random(0, this.list.length - 1);
				// 	let index = this.donelist[i].id - 1;
				// 	// 先转成字符串再转成对象，避免数组对象引用导致数据混乱
				// 	let item = JSON.parse(JSON.stringify(this.donelist[index]));
				// 	item.id = index;
				// 	this.flowList.push(item);
				// }
				this.list=this.donelist;
				this.showUndo=false;
				this.showDone=true;
				console.log("done",this.DoneflowList)
			},
			getUndo() {
				// this.UndoflowList=this.undolist;
				// for (let i = 0; i < this.undolist.length; i++) {
				// 	// let index = this.$u.random(0, this.list.length - 1);
				// 	let index = this.undolist[i].id - 1;
				// 	// 先转成字符串再转成对象，避免数组对象引用导致数据混乱
				// 	let item = JSON.parse(JSON.stringify(this.undolist[index]));
				// 	item.id = index;
				// 	this.UndoflowList.push(item);
				// }
				this.list=this.undolist;
				this.showDone=false;
				this.showUndo=true;
				console.log("undo",this.UndoflowList)
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
		}

	}
</script>

<style lang="scss" scoped>
	.mainframe {
		width: 750rpx;
		// height: 400rpx;
		padding-left: 32rpx;
		padding-right: 32rpx;
		padding-top: 32rpx;

		.actCata {
			height: 400rpx;
			padding-top: 32rpx;

			.cataTitle {
				color: #999999;
			}

			.cataContent {
				margin-top: 20rpx;
			}
		}

		.demo-warter {
			border-radius: 8px;
			margin: 5px;
			background-color: #ffffff;
			padding: 8px;
			position: relative;
			width: 335rpx;
		}

		.u-close {
			position: absolute;
			top: 32rpx;
			right: 32rpx;
		}

		.demo-img-wrap {}

		.demo-image {
			width: 100%;
			border-radius: 4rpx;
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
	}
</style>
