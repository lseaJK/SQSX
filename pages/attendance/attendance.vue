<template>
	<view>
		<activity-head :name="name"></activity-head>
		<view>
			<u-toast ref="uToast"></u-toast>
			<u-tabs class="tabs" bg-color="#fff" :bold="bold" :active-color="activeColor" :list="list" @change="change"
				:current="current" :is-scroll="isScroll" :offset="offset" bar-width="66"></u-tabs>
		</view>
		<view v-show="isshow">
			<view class="cardwrap" >
				<view class="carditem">
					<view class="cardtitlewrap">
						<text class="people">XXX - 请假单</text>
						<text class="cond">
							<u-button class="pass" size="mini">通过</u-button>
							<u-button class="fail" size="mini">不通过</u-button>
						</text>
					</view>
					<view class="cardcontent">
						<text>来自【组织生活】：【2月组织生活】\n请假原因：\n【】</text>
						<view class="time">2021-7-12</view>
					</view>
				</view>
			</view>
		</view>
		<view v-show="!isshow">
			<view class="cardwrap" >
				<view class="carditem">
					<view class="cardtitlewrap">
						<text class="activity">【2月组织生活】</text>
						<view class="time">2021-7-12</view>
					</view>
					<view class="cardcontent">
						<text>应到 X 人，实到 X 人\n请假者：xxx,xxx\n</text>
					</view>
				</view>
			</view>
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
				name: "考勤管理",
				//tabs
				list: [{
					name: "请假情况"
				}, {
					name: "考勤汇总"
				}],
				current: 0,
				sectionCurrent: 0,
				isScroll: true,
				tabCountIndex: 0,
				activeColor: this.$u.color['error'],
				bold: false,
				offset: [5, 25],
				isshow: true,
			};
		},
		methods: {
			//tabs
			change(index) {
				this.current = index;
				if (this.current == 0)
					this.isshow = true;
				else
					this.isshow = false;
			},
			//card
			click(index) {
				console.log(index);
			},
			headClick(index) {
				console.log(index);
			}
		}
	}
</script>

<style lang="scss" scoped>
	page {
		background-color: rgb(243, 243, 243);
	}

	.tabs {
		margin-top: 22px;
		margin-bottom: 22px;
		text-align: center;
	}

	.cardwrap {
		padding-left: 20rpx;
		padding-right: 20rpx;

		.carditem {
			padding-bottom: 20rpx;
			background-color: #fff;
			margin-bottom: 30rpx;

			.cardtitlewrap {
				height: 70rpx;
				line-height: 70rpx;
				
				.people {
					width: 260rpx;
					font-size: 32rpx;
					float: left;
					margin-left: 40rpx;
				}

				.cond{
					color: red;
					font-size: 28rpx;
					float: right;
					margin-right: 40rpx;
					.pass,.fail{
						font-size: 26rpx;
						letter-spacing: 2rpx;
					}
					.pass{
						background-color: rgb(224,60,38);
						color: #fff;
						margin-right: 20rpx;
					}
					.fail{
						background-color: rgb(251,235,233);
						color: rgb(224,60,38);
					}
				}
				
				.time{
					color: #999999;
					text-align: right;
					margin-right: 20rpx;
				}
				
				.activity{
					width: 300rpx;
					font-size: 32rpx;
					float: left;
					margin-left: 40rpx;
				}
			}

			.cardcontent {
				font-size: 28rpx;
				letter-spacing: 2rpx;
				line-height: 50rpx;
				color: #666666;
				background-color: #fff;
				border-top: 4rpx solid rgb(243, 243, 243);
				padding-left: 50rpx;
				padding-top: 5rpx;
				.time {
					color: rgb(224,60,38);
					font-size: 28rpx;
					text-align: right;
					margin-right: 40rpx;
				}
			}
		}

	}
</style>
