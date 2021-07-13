<template>
	<view>
		<activity-head :name="name"></activity-head>
		<view class="infowrap">
			<u-row gutter="16" justify="space-between">
				<u-col span="4">
					<image class="infoimg" src="../../static/member/兑换.png" mode="center"></image>
				</u-col>
				<u-col span="8">
					<view class="infodetail">
						<view class="infoedit">
							<view class="infoname">
								<text style="margin-right: 10rpx;">姓名</text>
								<u-icon name="edit-pen-fill" color="#0091FF"></u-icon>
							</view>
							<u-icon name="gift-fill" size="36" color="rgb(226,62,40)"></u-icon>
							<view class="scoreinfo">积分</view>
						</view>
						<view class="tagwrap">
							<u-tag class="tagitem" text="XXXX" mode="plain" />
							<u-tag class="tagitem" text="XXXX" mode="plain" />
							<u-tag class="tagitem" text="XXXX" mode="plain" />
							<u-tag class="tagitem" text="XXXX" mode="plain" />
						</view>
					</view>
				</u-col>
			</u-row>
		</view>
		<view class="titlewrap">
			<view class="titleitem">
				<u-image style="display: inline-block;margin: 24rpx;" width="34rpx" mode="widthFix" :src="src1">
				</u-image>
				<text class="titlediscript">闵行区行政服务中心第一支部 - 宣传员</text>
			</view>
			<view class="titleitem">
				<u-image style="display: inline-block;margin: 24rpx;" width="34rpx" mode="widthFix" :src="src2">
				</u-image>
				<text class="titlediscript">闵行区行政服务中心第一支部 - 誓词</text>
			</view>
		</view>
		<!-- 动态-活动-评论 -->
		<view class="u-demo-area">
			<u-toast ref="uToast"></u-toast>
			<u-grid :col="col" @click="click_item" :border="false">
				<u-grid-item :index="0" class="display_num">
					<view class="count-to-demo">
						<u-count-to class="count-to" useEasing="true" ref="uCountTo" autoplay="true"
							:startVal="startVal" :endVal="pyq_num" duration="1000" :decimals="decimals" bold="true"
							@end="end"></u-count-to>
					</view>
					<view class="grid-text">动态</view>
				</u-grid-item>
				<u-grid-item :index="1">
					<view class="count-to-demo">
						<u-count-to class="count-to" useEasing="true" ref="uCountTo" autoplay="true"
							:startVal="startVal" :endVal="activity_num" duration="1000" :decimals="decimals" bold="true"
							@end="end"></u-count-to>
					</view>
					<view class="grid-text">活动</view>
				</u-grid-item>
				<u-grid-item :index="2">
					<view class="count-to-demo">
						<u-count-to class="count-to" useEasing="true" ref="uCountTo" autoplay="true"
							:startVal="startVal" :endVal="comment_num" duration="1000" :decimals="decimals" bold="true"
							@end="end"></u-count-to>
					</view>
					<view class="grid-text">评论</view>
				</u-grid-item>
			</u-grid>
		</view>
		<view class="mycirclewrap">
			<view class="mycircletitle">我的朋友圈</view>
			<!-- 活动分类 -->
			<view class="actCata">
				<view class="cataContent">
					<u-toast ref="cataToast"></u-toast>
					<u-grid :col="col" @click="cataClick" :border="border">
						<block v-for="(cataitem,cataindex) of catalist" :key="cataindex">
							<u-grid-item class="grid-item" :index="cataindex" @click="cataitemClick">
								<view class="grid-text">{{cataitem}}</view>
							</u-grid-item>
						</block>
					</u-grid>
				</view>
			</view>
			<!-- #活动分类 -->
		</view>

<view class="u-card-wrap">
				<u-card @click="click" @head-click="headClick" padding="0" :border="border" :show-head="showhead" >
					<view class="" slot="body">
						<view v-for="(item,index) in list">
							<view class="u-body-item u-flex u-row-between u-p-b-0">
								<view class="u-body-item-title u-line-2">
									<!-- 	釉色渲染仕女图韵味被私藏，而你嫣然的一笑如含苞待放 -->
									{{item.title}}
								</view>
								<image src="https://img12.360buyimg.com/n7/jfs/t1/102191/19/9072/330688/5e0af7cfE17698872/c91c00d713bf729a.jpg"mode="aspectFill"></image>
							</view>

							<view class="u-icon-item u-border-bottom u-border-right icon-box">
								<u-icon class="iconItem" name="chat" size="30" color="rgb(79,149,236)"></u-icon>
								<text class="textItem">{{item.chat_num}}</text>
								<u-icon class="iconItem" name="share" size="26" color="#000"></u-icon>
								<text class="textItem">{{item.share_num}}</text>
								<u-icon class="iconItem" name="heart-fill" size="30" color="rgb(242,92,98)">
								</u-icon>
								<text class="textItem">{{item.like_num}}</text>

							</view>
						</view>
					</view>
				</u-card>
			</view>
	</view>
</template>

<script>
	import activityHead from "@/components/activity-head";
	export default {
		components: {
			activityHead
		},
		data() {
			return {
				name: "我是党员",
				src1: "/static/zhibudangyuan.png",
				src2: "/static/chengnuo.png",
				//  grid的参数
				border: true,
				col: 3,
				catalist: ['integral', 'kefu-ermai', 'coupon', 'gift', 'scan', 'pause-circle', 'wifi', 'email', 'list'],
				//列表
				// title: '动态列表',
				showhead: false,
				// padding: 0,
				bottomSlot: true,
				border: true,
				//数字
				startVal: 0,
				separator: ',',
				decimals: 0,
				duration: 1000,
				autoplay: false,
				useEasing: true,
				current: 3,
				isStop: false, // 如果开没启动前，不允许点击状态选项的"继续"按钮，否则会导致显示NaN
				bold: true,
				pyq_num: 6, //个人动态数
				activity_num: 7, //参加活动数
				comment_num: 8, //参与评论数
				list: [{
						id: 1,
						title: '内容1',
						chat_num: 0,
						share_num: 0,
						like_num: 0,
					},
					{
						id: 2,
						title: '内容2',
						chat_num: 0,
						share_num: 0,
						like_num: 0,
					},
					{
						id: 3,
						title: '内容3',
						chat_num: 0,
						share_num: 0,
						like_num: 0,
					}
				],

			}
		},
		methods: {
			//grid
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
			click(index) {
				console.log(index);
			},
			headClick(index) {
				console.log(index);
			},
			end() {
				this.current = 3;
				this.$refs.uToast.show({
					type: 'warning',
					title: '滚动结束'
				});
			},
			click_item(index) {
				this.$refs.uToast.show({
					title: `点击了第${index + 1}宫格`,
					type: 'warning'
				})
			},
		},
		mounted() {
			uni.setNavigationBarColor({
				frontColor: '#ffffff',
				backgroundColor: '#d81e06'
			})
			uni.setNavigationBarTitle({
				title: "我是党员"
			})
		},
	}
</script>

<style scoped lang="scss">
	.infowrap {
		padding-left: 35rpx;
		padding-top: 20rpx;

		.infoimg {
			width: 200rpx;
			height: 200rpx;
			overflow: hidden;
			// background-color: #18B566;
		}

		.infodetail {
			padding-left: 45rpx;
			// background-color: #2979FF;
			display: flexbox;

			.infoedit {
				display: flex;

				.infoname {
					color: #333333;
					font-size: 40rpx;
					line-height: 45rpx;
					margin-right: 76rpx;

				}

				.scoreinfo {
					margin-left: 20rpx;
					font-size: 28rpx;
					line-height: 42rpx;
				}
			}

			.tagwrap {
				margin-top: 24rpx;

				.tagitem {
					margin-right: 10rpx;
					margin-bottom: 10rpx;
				}
			}
		}
	}

	.titlewrap {
		// background-color: #18B566;
		padding-left: 32rpx;
		height: 200rpx;

		.titleitem {
			height: 88rpx;
			width: 686rpx;
			border-bottom: 2rpx solid #EEEEEE;

			.titlediscript {
				font-family: PingFangSC-Regular;
				font-size: 28rpx;
				color: #999999;
				letter-spacing: 0.5rpx;
				text-align: left;
				line-height: 38rpx;
			}
		}
	}

	.mycirclewrap {
		// background-color: #2979FF;
		padding-top: 20rpx;
		padding-bottom: 20rpx;

		.mycircletitle {
			font-size: 40rpx;
			line-height: 50rpx;
			margin-left: 42rpx;
			color: #333333;
		}

		.actCata {
			padding: 0 25rpx;

			.cataContent {
				margin-top: 20rpx;
			}
		}
	}

	.u-demo {
		padding-top: 0;
	}

	.u-card-wrap {
		// background-color: $u-bg-color;
		padding: 1px;
	}

	.u-body-item {
		font-size: 32rpx;
		color: #333;
		padding: 20rpx 10rpx;
	}

	.u-body-item image {
		width: 120rpx;
		flex: 0 0 120rpx;
		height: 120rpx;
		border-radius: 8rpx;
		margin-left: 12rpx;
	}

	.icon-box {
		font-family: PingFangSC-Regular;
		font-size: 20px;
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

	// .icon-box {
	// 	flex: 0 0 120rpx;
	// }

	.grid-text {
		font-size: 35rpx;
		margin-top: 4rpx;
		color: $u-type-info;
	}

	.badge-icon {
		position: absolute;
		width: 40rpx;
		height: 40rpx;
	}

	.display_num {
		padding: 1px;
	}
</style>
