<template>
	<view>
		<index-head :name="name" :src="src" :list="notelist"></index-head>
		<!-- <u-button type="error" @click="myComment">点击显示评论列表</u-button> -->
		<view class="welcome">欢迎回来：xx</view>
		<!-- 五个图标功能 -->
		<view>
			<u-toast ref="uToast"></u-toast>
			<u-grid :col="5" :border="false">
				<u-grid-item @click="myMessage">
					<image class="iconimg" src="/static/index/待阅.png"></image>
					<view class="grid-text">通知</view>
				</u-grid-item>
				<!-- 待阅弹出框 -->
				<u-popup v-model="showMessage" border-radius="10" mode="center" @close="close" @open="open" length="80%"
					:mask="mask" :closeable="closeable" close-icon-pos="top-right" close-icon-color="#d81e06">
					
						<view class="messageframe">
							<view class="messagehead">
								<view class="messagetitle"> 待阅信息</view>
								<view class="messagesubtitle">共 X 条</view>
							</view>
							<view class="messagebody">
								<scroll-view scroll-y="true">
									<view class="message" v-for="(res, index) in messageList" :key="res.id">
										<u-tag class="messagetag" :text="res.start_time" mode="light" shape="square" show="false" />
										<view class="messagetitle">{{res.title}}</view>
									</view>
								</scroll-view>
							</view>
						</view>
				
				</u-popup>
				<!-- #待阅弹出框 -->
				<u-grid-item @click="myComment">
					<image class="iconimg" src="/static/index/点评.png"></image>
					<!-- <u-icon name="lock" :size="46"></u-icon> -->
					<view class="grid-text">点评</view>
				</u-grid-item>
				<!-- 点评弹出框 -->
				<u-popup v-model="showComment" border-radius="10" mode="center" @close="close" @open="open" length="80%"
					:mask="mask" :closeable="closeable" close-icon-pos="top-right" close-icon-color="#d81e06">
					<view class="commentframe">
						<!-- 评论列表 -->
						<view class="commenthead">
							<view class="commenttitle"> 我的点评 </view>
							<view class="commentsubtitle">共 X 条</view>
						</view>
						<view class="commentbody">
							<scroll-view scroll-y="true" style="height:800rpx">
								<view class="comment" v-for="(res, index) in commentList" :key="res.id">
									<view class="left">
										<image :src="res.avatarurl" mode="aspectFill"></image>
									</view>
									<view class="right">
										<view class="top">
											<view class="name">{{ res.username }}</view>
										</view>
										<view> 评论了我的动态：{{res.my_pyq_content}}</view>
										<view>
											<text class="bodycontent">{{ res.content }}</text>
										</view>
										<view class="bottom">
											{{ res.time }}
											<view class="reply">回复</view>
										</view>
									</view>
								</view>
							</scroll-view>
						</view>
					</view>
				</u-popup>
				<!-- #点评弹出框 -->
				<u-grid-item>
					<image class="iconimg" src="/static/index/朋友圈.png"></image>
					<!-- <u-icon name="hourglass" :size="46"></u-icon> -->
					<view class="grid-text">动态</view>
				</u-grid-item>
				<u-grid-item>
					<image class="iconimg" src="/static/index/活动.png"></image>
					<!-- <u-icon name="hourglass" :size="46"></u-icon> -->
					<view class="grid-text">活动</view>
				</u-grid-item>
				<u-grid-item>
					<image class="iconimg" src="/static/index/兑换.png"></image>
					<!-- <u-icon name="hourglass" :size="46"></u-icon> -->
					<view class="grid-text">兑换</view>
				</u-grid-item>
			</u-grid>
		</view>
		<!-- 轮播图 -->
		<view class="swipperwrap">
			<u-swiper :list="swipperlist" @change="change" duration="3000" :circular="true"></u-swiper>
		</view>
		<!-- 分类滑块 -->
		<view class="catawrap">
			<u-tabs :offset="offset" :list="tabs_list" :is-scroll="false" :current="tabs_current" @change="tabs_change"
				bar-width="66" active-color="#108EE9" font-size="30"></u-tabs>
		</view>
		<!-- 活动瀑布流 -->
		<view class="waterfallwrap">
			<u-waterfall v-model="list" ref="uWaterfall">
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
			<!-- 弹出活动信息 -->
			<!-- 弹出课件详情 -->
			<u-popup border-radius="10" v-model="show" @close="close" @open="open" mode="center" width="680rpx"
				:mask="mask" :closeable="closeable" close-icon-pos="top-right" close-icon-color="#d81e06">
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

</template>

<script>
	import indexHead from "@/components/index-head";
	export default {
		components: {
			indexHead
		},
		data() {
			return {
				name: "首页",
				src: "/static/banner.png",
				notelist: ["XXXX欢迎您", "没有前端不好吗"],
				showMessage: false,
				messageList:[],
				showComment: false,
				commentList: [],
				//tab
				tabs_current: 0,
				tabs_list: [{
					name: '学习'
				}, {
					name: '活动',
				}, {
					name: '支部'
				}],
				offset: [5, 10],
				//swipperlist
				swipperlist: [{
						image: 'https://cdn.uviewui.com/uview/swiper/1.jpg',
						title: '昨夜星辰昨夜风，画楼西畔桂堂东'
					},
					{
						image: 'https://cdn.uviewui.com/uview/swiper/2.jpg',
						title: '身无彩凤双飞翼，心有灵犀一点通'
					},
					{
						image: 'https://cdn.uviewui.com/uview/swiper/3.jpg',
						title: '谁念西风独自凉，萧萧黄叶闭疏窗，沉思往事立残阳'
					}
				],
				//列表
				mask: true,
				closeable: true,
				openIndex: 0,
				show: false,
				goStudy(id) {
					this.show = true;
					this.openIndex = id;
					console.log('item.id:', id);
				},
				list: [{
						id: 0,
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
						id: 1,
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
						id: 2,
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
						id: 3,
						act_id: 4,
						title: '学习课件444',
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

		},
		mounted() {
			uni.setNavigationBarColor({
				frontColor: '#ffffff',
				backgroundColor: '#d81e06'
			})
			uni.setNavigationBarTitle({
				title: "首页"
			})
		},
		methods: {
			change(index) {
				// console.log(index);
			},
			close() {
				// console.log('close');
			},
			open() {
				// console.log('open');
			},
			myComment() {
				this.getComment();
				this.showComment = true;
			},
			myMessage(){
					this.getMessage();
					this.showMessage=true;
			},
			//tab
			tabs_change(index) {
				// this.chang_list=false;
				this.tabs_current = index;
				// this.getCata(index);
				console.log("index", index);
				// this.list=this.donelist;

			},
			goStudy(id) {
				this.show = true;
				this.openIndex = id;
				console.log('item.id:', id);
			},
			// 通知列表
			close() {
				// console.log('close');
			},
			open() {
				// console.log('open');
			},
			getMessage() {
				this.messageList = [{
						id:0,
						title:"3月党日活动",
						start_time:"2021-7-13"
					},
					{
						id: 1,
						title:"4月党日活动",
						start_time:"2021-7-13"
					},
					{
						id: 2,
						title:"5月党日活动",
						start_time:"2021-7-13"
					},
					{
						id: 3,
						title:"6月党日活动",
						start_time:"2021-7-13"
					}
				];
			},
			close() {
				// console.log('close');
			},
			open() {
				// console.log('open');
			},
			// 评论列表
			getComment() {
				this.commentList = [{
						id: 0,
						my_pyq_id: 1,
						my_pyq_content: '我的朋友圈内容',
						username: '叶轻眉',
						time: '12-25 18:58',
						content: '评论内容https://cdn.uviewui.com/uview/template/SmilingDog.jpg',
						avatarurl: 'https://cdn.uviewui.com/uview/template/SmilingDog.jpg',
					},
					{
						id: 1,
						my_pyq_id: 1,
						my_pyq_content: '我的朋友圈内容',
						username: '叶轻眉',
						time: '12-25 18:58',
						content: '评论内容https://cdn.uviewui.com/uview/template/SmilingDog.jpg',
						avatarurl: 'https://cdn.uviewui.com/uview/template/SmilingDog.jpg',
					},
					{
						id: 2,
						my_pyq_id: 1,
						my_pyq_content: '我的朋友圈内容',
						username: '叶轻眉',
						time: '12-25 18:58',
						content: '评论内容',
						avatarurl: 'https://cdn.uviewui.com/uview/template/SmilingDog.jpg',
					},
					{
						id: 3,
						my_pyq_id: 1,
						my_pyq_content: '我的朋友圈内容',
						username: '叶轻眉',
						time: '12-25 18:58',
						content: '评论内容',
						avatarurl: 'https://cdn.uviewui.com/uview/template/SmilingDog.jpg',
					}
				];
			}
		}
	}
</script>
<style lang="scss" scoped>
	.welcome {
		margin-top: 110rpx;
		margin-left: 40rpx;
		font-size: 40rpx;
		line-height: 60rpx;
	}

	.content {
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
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

	.swipperwrap,
	.catawrap,
	.waterfallwrap {
		width: 686rpx;
		margin: 0 auto;
	}

	.waterfallwrap {
		padding-bottom: 60rpx;
	}

	.catawrap {
		text-align: center;
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
	.messageframe {
		
		.messagehead {
			margin-top: 38rpx;
			margin-left: 32rpx;
			font-family: PingFangSC-Medium;
			color: #333333;
			width: 350rpx;
			padding-bottom: 20rpx;

			.messagetitle {
				font-size: 34rpx;
				line-height: 48rpx;
				display: inline;
				margin-right: 40rpx;
			}

			.messagesubtitle {
				font-size: 24rpx;
				text-align: right;
				display: inline;
			}
		}

		.messagebody{
			padding-left: 29rpx;
			.message{
				height: 70rpx;
				.messagetag{
					display: inline-block;
				}
				.messagetitle{
					display: inline-block;
					margin-left: 30rpx;
					line-height: 50rpx;
					font-size: 28rpx;
					letter-spacing: 1rpx;
					color: #999999;
				}
				
			}
		}
	}


	.commentframe {
		padding-top: 20rpx;
		
		.commenthead {
			margin-top: 38rpx;
			margin-left: 32rpx;
			font-family: PingFangSC-Medium;
			color: #333333;
			width: 350rpx;
			padding-bottom: 10rpx;

			.commenttitle {
				font-size: 34rpx;
				line-height: 48rpx;
				display: inline;
				margin-right: 40rpx;
			}

			.commentsubtitle {
				font-size: 24rpx;
				text-align: right;
				display: inline;
			}
		}

		.commentbody {
			padding-bottom: 60rpx;
			.comment {
				display: flex;
				padding-top: 30rpx;
				padding-left: 30rpx;

				.left {
					image {
						width: 64rpx;
						height: 64rpx;
						border-radius: 50%;
						background-color: #f2f2f2;
					}
				}

				.right {
					flex: 1;
					padding-left: 20rpx;
					font-size: 30rpx;

					.top {
						display: flex;
						justify-content: space-between;
						align-items: center;
						margin-bottom: 10rpx;

						.name {
							color: #5677fc;
						}

						.highlight {
							color: #5677fc;

							.num {
								color: #5677fc;
							}
						}


					}

					.bodycontent {
						width: 120rpx;
						overflow: hidden;
						word-break: normal;
						word-wrap: break-word;
					}

					.bottom {
						margin-top: 20rpx;
						display: flex;
						font-size: 24rpx;
						color: #9a9a9a;

						.reply {
							color: #5677fc;
							margin-left: 10rpx;
						}
					}
				}
			}

		}
	}

	.logo {
		height: 200rpx;
		width: 200rpx;
		margin-top: 200rpx;
		margin-left: auto;
		margin-right: auto;
		margin-bottom: 50rpx;
	}

	// .text-area {
	// 	display: flex;
	// 	justify-content: center;
	// }

	.title {
		font-size: 36rpx;
		color: #8f8f94;
	}
</style>
