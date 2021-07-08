<template>
	<view>
		<activity-head :name="name"></activity-head>

		<view class="mainframe">
			<!-- 分类滑块 -->
			<u-tabs :list="tabs_list" :is-scroll="false" :current="tabs_current" @change="tabs_change" bar-width="66"
				active-color="#108EE9" font-size="30"></u-tabs>
			<!-- 已结束活动 -->
			<view v-show="tabs_finished()">
				<!-- 活动分类 -->
				<view class="actCata">
					<view class="cateTitle">活动分类</view>
					<view class="cateContent">
						<u-toast ref="fToast"></u-toast>
						<u-grid :col="col" @click="Fclick" :border="border">
							<block v-for="(fitem,findex) of Flist" :key="findex">
								<u-grid-item class="grid-item" :index="findex" @click="FitemClick">
									<view class="grid-text">{{fitem}}</view>
								</u-grid-item>
							</block>
						</u-grid>
					</view>
				</view>
				<!-- 活动分类 -->
				<!-- 活动列表 -->
				<view class="actList">
					<view class="listTitle">活动列表</view>
				</view>
				<!-- 活动列表 -->
			</view>
			<view v-show="!tabs_finished()">
				<!-- 活动分类 -->
				<view class="actCata">
					<view class="cateTitle">活动分类</view>
					<view class="cateContent">
						<u-toast ref="uToast"></u-toast>
						<u-grid :col="col" @click="Uclick" :border="border">
							<block v-for="(uitem,uindex) of Ulist" :key="uindex">
								<u-grid-item class="grid-item" :index="uindex" @click="UitemClick">
									<view class="grid-text">{{uitem}}</view>
								</u-grid-item>
							</block>
						</u-grid>
					</view>
				</view>
				<!-- 活动分类 -->
				<!-- 活动列表 -->
				<view class="actList">
					<view class="listTitle">活动列表</view>
				</view>
				<!-- 活动列表 -->
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
				// 【需要传值】活动的分类数组 
				Flist: ['integral', 'kefu-ermai', 'coupon', 'gift', 'scan', 'pause-circle', 'wifi', 'email', 'list'],
				Ulist: ['integral', 'kefu-ermai', 'coupon', 'gift', 'scan', 'pause-circle', 'wifi', 'email', 'list'],

			}
		},

		methods: {
			//tabs
			tabs_finished() {
				return this.tabs_current == 0 ? true : false;
			},
			tabs_change(index) {
				this.tabs_current = index;
			},
			//已结束grid
			Fclick(index) {
				this.$refs.fToast.show({
					title: `点击了第${index + 1}宫格`,
					type: 'warning'
				})
			},
			// 针对单个grid-item的事件
			FitemClick(index) {
				// console.log(index);
			},
			//未开始grid
			Uclick(index) {
				this.$refs.uToast.show({
					title: `点击了第${index + 1}宫格`,
					type: 'warning'
				})
			},
			// 针对单个grid-item的事件
			UitemClick(index) {
				// console.log(index);
			}
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

			.cateTitle {
				color: #999999;
			}

			.cateContent {
				margin-top: 20rpx;
			}
		}
	}
</style>
