<template>
	<view>
		<activity-head :name="name"></activity-head>

		<view class="infowrap">
			<u-row gutter="16" justify="space-between">
				<u-col span="4">
					<image class="infoimg" src="../../static/member/兑换.png" mode="center"></image>
					<a
						style="margin-left: 24rpx;letter-spacing: 0.32rpx;text-align: left;font-size: 24rpx;color: #999999;">支部积分：999</a>
				</u-col>
				<u-col span="8">
					<view class="infodetail">
						<view class="infoedit">
							<view class="infoname">
								<view style="margin-right: 10rpx;">姓名</view>
								<view style="margin-right: 10rpx;">地址</view>
								<view style="margin-right: 10rpx;">时间</view>
								<view style="margin-right: 10rpx;">书记</view>
							</view>
						</view>
					</view>
				</u-col>
			</u-row>
		</view>

		<view class="u-demo-area">
			<u-toast ref="uToast"></u-toast>
			<u-grid :col="col" @click="click_item" :border="false">
				<u-grid-item :index="0" class="display_num">
					<view class="count-to-demo">
						<u-count-to class="count-to" :useEasing="true" ref="uCountTo" :autoplay="true"
							:startVal="startVal" :endVal="number_num" duration="1000" :decimals="decimals" :bold="true">
						</u-count-to>
					</view>
					<view class="grid-text">成员数量</view>
				</u-grid-item>
				<u-grid-item :index="1">
					<view class="count-to-demo">
						<u-count-to class="count-to" :useEasing="true" ref="uCountTo" :autoplay="true"
							:startVal="startVal" :endVal="activity_num" duration="1000" :decimals="decimals"
							:bold="true"></u-count-to>
					</view>
					<view class="grid-text">组织生活</view>
				</u-grid-item>
				<u-grid-item :index="2">
					<view class="count-to-demo">
						<u-count-to class="count-to" :useEasing="true" ref="uCountTo" :autoplay="true"
							:startVal="startVal" :endVal="study_num" duration="1000" :decimals="decimals" :bold="true">
						</u-count-to>
					</view>
					<view class="grid-text">支部学习</view>
				</u-grid-item>
			</u-grid>
		</view>


		<view class="btnwrap">
			<u-button class="btn" :ripple="true" style="margin-right: 30rpx;">
				<image class="btnicon" src="../../static/icon_l1tnyvfch4l/feiji.png"></image>
				发布组织活动

			</u-button>
			<u-button class="btn" :ripple="true">
				<image class="btnicon" src="../../static/icon_l1tnyvfch4l/dianji.png"></image>
				考勤管理
			</u-button>
		</view>

		<view class="infoframe">

			<view class="titleinfo">支部简介</view>
			<view class="contentinfo">支部简介支部简介支部简介支部简介支部简介支部简介支部简介支部简介</view>

			<view class="line"></view>

			<view class="titleinfo">小组信息</view>
			<u-collapse>
				<u-collapse-item :title="item.head" v-for="(item, index) in itemList" :key="index">
					{{item.body}}
				</u-collapse-item>
			</u-collapse>

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
				name: "支部信息",
				//数字
				col: 3,
				startVal: 0,
				separator: ',',
				decimals: 0,
				duration: 1000,
				autoplay: false,
				useEasing: true,
				current: 3,
				isStop: false, // 如果开没启动前，不允许点击状态选项的"继续"按钮，否则会导致显示NaN
				bold: true,
				number_num: 6, //成员数量
				activity_num: 7, //组织生活
				study_num: 8, //支部学习
				//小组信息
				itemList: [{
					head: "赏识在于角度的转换",
					body: "只要我们正确择取一个合适的参照物乃至稍降一格去看待他人，值得赏识的东西便会扑面而来",
					open: true,
					disabled: true
				}, {
					head: "生活中不是缺少美，而是缺少发现美的眼睛",
					body: "学会欣赏，实际是一种积极生活的态度，是生活的调味品，会在欣赏中发现生活的美",
					open: false,
				}, {
					head: "周围一些不起眼的人、事、物，或许都隐藏着不同凡响的智慧",
					body: "但是据说雕刻大卫像所用的这块大理石，曾被多位雕刻家批评得一无是处，有些人认为这块大理石采凿得不好，有些人嫌它的纹路不够美",
					open: false,
				}],
				
			}
		},
		mounted() {
			uni.setNavigationBarColor({
				frontColor: '#ffffff',
				backgroundColor: '#d81e06'
			})
			uni.setNavigationBarTitle({
				title: "我的支部"
			})
		},
		methods: {

		}
	}
</script>

<style scoped lang="scss">
	.infowrap {
		padding-left: 35rpx;
		padding-top: 10rpx;
		margin-bottom: 30rpx;

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
					padding-top: 20rpx;
					color: #333333;
					font-size: 28rpx;
					line-height: 60rpx;

				}

				.scoreinfo {
					margin-left: 20rpx;
					font-size: 28rpx;
					line-height: 42rpx;
				}
			}

		}
	}

	.btnwrap {
		padding-left: 55rpx;
		margin-top: 30rpx;

		.btn {
			padding: 0;
			background-color: rgb(224, 60, 38);
			font-family: PingFangSC-Regular;
			font-size: 30px;
			color: #FFFFFF;
			letter-spacing: 0;
			text-align: center;
			width: 300rpx;
			display: inline-block;

			.btnicon {
				vertical-align: middle;
				width: 44rpx;
				height: 44rpx;
				box-sizing: content-box;
				margin-right: 20rpx;
			}
		}
	}

	.infoframe {
		width: 660rpx;
		margin: 0 auto;
		padding-top: 29rpx;
		padding-bottom: 80rpx;

		.titleinfo {
			font-family: PingFangSC-Medium;
			font-size: 36rpx;
			color: #000000;
			letter-spacing: 0.75rpx;
			text-align: left;
			line-height: 50rpx;
			margin-bottom: 8rpx;
		}

		.contentinfo {
			text-indent: 2em;
			font-family: PingFangSC-Light;
			font-size: 28rpx;
			color: #000000;
			letter-spacing: 0.58rpx;
			text-align: left;
		}
	}

	.line {
		width: 646rpx;
		border: 1px solid rgba(151, 151, 151, 0.50);
		margin-top: 30rpx;
		margin-bottom: 30rpx;
	}
</style>
