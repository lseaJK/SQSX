<template>
	<view>
		<activity-head :name="name"></activity-head>

<u-form :model="form" ref="uForm">
		<view class="cardwrap">
			<view class="carditem" prop="act_title">
				<view class="cardtitlewrap">
					<view class="people">标题
						<!-- <text style="color: red;">*</text> -->
					</view>
				</view>
				<view class="cardcontent">
					<input type="text" placeholder="请输入标题" style="font-size: 26rpx;padding-top: 10rpx;" />
				</view>
			</view>

			<view class="carditem" prop="act_content">
				<view class="cardtitlewrap">
					<view class="people">简介
						<!-- <text style="color: red;">*</text> -->
					</view>
				</view>
				<view class="cardcontent">
					<input type="text" placeholder="请输入简介" style="font-size: 26rpx;padding: 10rpx;height: 100rpx;" />
				</view>
			</view>

			<view class="carditem" >
				<view class="cardtitlewrap" @click="showDate = true">
					<text class="people">开始时间：{{date}}</text>
					<u-calendar v-model="showDate" mode="date" @change="changeDate"></u-calendar>
				</view>
				<view class="cardcontent">
						<text @click="showSartTime=true">{{ start_time ? start_time : '请选择开始时刻' }} - </text>
						<u-picker mode="time" :defaultTime="defaultTime" v-model="showSartTime" :params="params"
							@confirm="setStart"></u-picker>

						<text @click="showEndTime=true">{{ end_time ? end_time : '请选择结束时刻' }} </text>
						<u-picker mode="time" :defaultTime="defaultTime" v-model="showEndTime" :params="params"
							@confirm="setEnd"></u-picker>
				</view>
			</view>

			<view class="carditem" prop="act_type">
				<view class="cardtitlewrap">
					<text class="people">结算方式</text>
				</view>
				<view class="cardcontent">
					<u-radio-group v-model="radio" @change="radioGroupChange" width="auto" :wrap="false">
						<u-radio shape="circle" v-for="(item, index) in radioList" :key="index" :name="item.name">
							{{ item.name }}
						</u-radio>
					</u-radio-group>
				</view>
			</view>

			<u-button @click="submit">提交</u-button>

		</view>

</u-form>
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
				name: "发布组织生活",
				showDate: false,
				date: '请选择',
				datemode: 'date',
				catalist: ['integral', 'kefu-ermai', 'coupon', 'gift', 'scan', 'pause-circle'],
				//表单
				form: {
					act_title: '',
					act_content: '',
					act_type: '',
					act_start_time: '',
					act_end_time: ''
				},
				rules: {
					act_title: [{
						required: true,
						message: '请输入活动标题',
						trigger: ['blur', 'change']
					}],
					act_content: [{
						required: true,
						message: '请输入活动简介',
						trigger: ['blur', 'change']
					}],
					act_type: [{
						required: true,
						message: '请选择活动标签',
						trigger: 'change'
					}],
				},
				//时间选择
				start_time: '',
				end_time: '',
				showSartTime: false,
				showEndTime: false,
				params: {
					hour: true,
					minute: true,
					timestamp: true
				},
				defaultTime: '9:00',
				input: '',
				//活动标签选择
				radioList: [{
						name: '标签1',
						checked: true,
						disabled: false
					},
					{
						name: '标签2',
						checked: false,
						disabled: false
					},
					{
						name: '标签3',
						checked: false,
						disabled: false
					},
					{
						name: '标签4',
						checked: false,
						disabled: false
					}
				],
				radio: '标签1',
			}
		},
		onReady() {
			this.$refs.uForm.setRules(this.rules);
		},
		methods: {
			changeDate(e) {
				this.date = e.result;
				console.log(e);
			},
			//已结束grid
			cataClick(index) {
				this.$refs.cataToast.show({
					title: `点击了第${index + 1}宫格`,
					type: 'warning'
				})
			},
			// 针对单个grid-item的事件
			cataitemClick(index) {
				console.log("选择标签：", index);
				this.act_type = this.catalist[index];
			},
			submit() {
				this.$refs.uForm.validate(valid => {
					if (valid) {
						console.log('验证通过');
					} else {
						console.log('验证失败');
					}
				});
			},
			//时间
			confirm(e) {
				console.log(e);
				// if (this.params.year) this.input += e.year;
				// if (this.params.month) this.input += '-' + e.month;
				// if (this.params.day) this.input += '-' + e.day;
				if (this.params.hour) this.input += ' ' + e.hour;
				if (this.params.minute) this.input += ':' + e.minute;
				// if (this.params.second) this.input += ':' + e.second;
			},

			setStart(e) {
				console.log(e);
				this.start_time = '';
				if (this.params.hour) this.start_time += ' ' + e.hour;
				if (this.params.minute) this.start_time += ':' + e.minute;
			},
			setEnd(e) {
				console.log(e);
				this.end_time = '';
				if (this.params.hour) this.end_time += ' ' + e.hour;
				if (this.params.minute) this.end_time += ':' + e.minute;
			},
			//活动标签
			radioGroupChange(e) {
				this.form.act_type = e;
			},
		},
	}
</script>

<style lang="scss" scoped>
	page {
		background-color: rgb(243, 243, 243);
	}

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

	.cardwrap {
		padding: 20rpx;

		.carditem {
			padding-bottom: 20rpx;
			background-color: #fff;
			margin-bottom: 30rpx;

			.cardtitlewrap {
				height: 70rpx;
				line-height: 70rpx;

				.people {
					width: 460rpx;
					font-size: 32rpx;
					float: left;
					margin-left: 40rpx;
				}

				.time {
					color: #999999;
					text-align: right;
					margin-right: 20rpx;
				}

				.activity {
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
					color: rgb(224, 60, 38);
					font-size: 28rpx;
					text-align: right;
					margin-right: 40rpx;
				}
			}
		}

	}
</style>
