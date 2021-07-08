<template>
	<view class="">
		<view class="wrap">
				<u-row gutter="16" justify="space-between">
					<u-col span="4">
						<image class="demo-layout" src="../../static/member/兑换.png" mode="center"></image>
					</u-col>
					<u-col span="8">
						<view class="demo-layout">
							<view >姓名</view>
							<view >积分</view>
							<view>
								<u-icon name="gift-fill" size="46" color="#111111"></u-icon>
							</view>
							<view><u-tag text="XXXX" mode="plain" /></view>
						</view>
					</u-col>
				</u-row>
		</view>
			<!-- 动态-活动-评论 -->
			<view class="u-demo-area">
				<u-toast ref="uToast"></u-toast>
				<u-grid :col="col" @click="click_item" :border="false">
					<u-grid-item :index="0" class="display_num">
						<view class="count-to-demo">
							<u-count-to
								class="count-to"
								useEasing="true"
								ref="uCountTo"
								autoplay="true"
								:startVal="startVal"
								:endVal="pyq_num"
								duration="1000"
								:decimals="decimals"
								bold="true"
								@end="end"
							></u-count-to>
						</view>
						<view class="grid-text">动态</view>
					</u-grid-item>
					<u-grid-item :index="1">
						<view class="count-to-demo">
							<u-count-to
								class="count-to"
								useEasing="true"
								ref="uCountTo"
								autoplay="true"
								:startVal="startVal"
								:endVal="activity_num"
								duration="1000"
								:decimals="decimals"
								bold="true"
								@end="end"
							></u-count-to>
						</view>
						<view class="grid-text">活动</view>
					</u-grid-item>
					<u-grid-item :index="2">
						<view class="count-to-demo">
							<u-count-to
								class="count-to"
								useEasing="true"
								ref="uCountTo"
								autoplay="true"
								:startVal="startVal"
								:endVal="comment_num"
								duration="1000"
								:decimals="decimals"
								bold="true"
								@end="end"
							></u-count-to>
						</view>
						<view class="grid-text">评论</view>
					</u-grid-item>
					</u-grid>
				</view>
		<view class="u-card-wrap">
			<u-card @click="click" @head-click="headClick" :title="title" :thumb="thumb" :padding="padding" :border="border">
				<view class="" slot="body">
				 <view v-for="(item,index) in list">
				 	<view class="u-body-item u-flex u-row-between u-p-b-0">
				 		<view class="u-body-item-title u-line-2">
				 		<!-- 	釉色渲染仕女图韵味被私藏，而你嫣然的一笑如含苞待放 -->
				 			{{item.title}}
				 		</view>
				 		<image src="https://img12.360buyimg.com/n7/jfs/t1/102191/19/9072/330688/5e0af7cfE17698872/c91c00d713bf729a.jpg" mode="aspectFill"></image>
				 	</view>
				 <view class="u-icon-item u-border-bottom u-border-right icon-box">
					 	<u-icon name="chat" size="40" color="#909399"></u-icon>&nbsp;&nbsp;{{item.chat_num}}&nbsp;&nbsp;
						<u-icon name="share" size="40" color="#909399"></u-icon>&nbsp;&nbsp;{{item.share_num}}&nbsp;&nbsp;
						<u-icon name="heart" size="40" color="#909399"></u-icon>&nbsp;&nbsp;{{item.like_num}}
				 </view>
				 </view>
				 </view>
			</u-card>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				//列表
				title: '动态列表',
				padding: 20,
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
				pyq_num:6,//个人动态数
				activity_num:7,//参加活动数
				comment_num:8,//参与评论数
				list:[
					{
						id:1,
						title:'内容1',
						chat_num:0,
						share_num:0,
						like_num:0,
					},
					{
						id:2,
						title:'内容2',
						chat_num:0,
						share_num:0,
						like_num:0,
					},
					{
						id:3,
						title:'内容3',
						chat_num:0,
						share_num:0,
						like_num:0,
					}
				],

			}
		},
		methods: {
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
			uni.setNavigationBarColor({frontColor:'#ffffff', backgroundColor: '#d81e06'})
			uni.setNavigationBarTitle({title:"我是党员"})
		},
	}
</script>

<style scoped lang="scss">
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
	.icon-box{
		flex: 0 0 120rpx;
	}
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
