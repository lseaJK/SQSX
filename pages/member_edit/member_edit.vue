<template>
	<view>
		<activity-head :name="name"></activity-head>

		<view class="infowrap">
			<u-row gutter="16" justify="space-between">
				<u-col span="4">
					<image class="infoimg" src="../../static/member/兑换.png" mode="center"></image>
					<a style="margin-left: 50rpx;letter-spacing: 0.32rpx;text-align: left;font-size: 24rpx;">点击替换</a>
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
		
		<view class="infomation">
			<u-form :model="form" ref="uForm">
				<u-form-item class="formitem" label="姓名" prop="name">
					<u-input v-model="form.name" />
				</u-form-item>
				<u-form-item class="formitem" :label-position="labelPosition" label="性别" >
					<u-input :border="border" type="select" :select-open="actionSheetShow" v-model="sex"
						placeholder="请选择性别" @click="actionSheetShow = true"></u-input>
				</u-form-item>
				<!-- <u-action-sheet :list="actionSheetList" v-model="showSex" @click="actionSheetCallback"></u-action-sheet> -->
				<view @click="showDate = true">
					<u-form-item class="formitem" label="入党日期" label-width="150">
						{{date}}
					</u-form-item>
				</view>
				<u-form-item  class="formitem" :rightIconStyle="{color: '#888', fontSize: '32rpx'}" :label-position="labelPosition"
					label="联系方式" label-width="150">
					<u-input :border="border" placeholder="请输入手机号" v-model="phone" type="number"></u-input>
				</u-form-item>
				<u-form-item class="formitem" label="亮出承诺" prop="intro"  label-width="150">
					<u-input v-model="form.intro" />
				</u-form-item>
			</u-form>
			<u-button @click="submit" style="margin-top: 60rpx;background-color: rgb(226,62,40);color: #fff;">保存</u-button>
		</view>
		<u-calendar v-model="showDate" :mode="mode" @change="changeDate"></u-calendar>
		<u-action-sheet :list="actionSheetList" v-model="actionSheetShow" @click="actionSheetCallback"></u-action-sheet>
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
				showDate: false,
				mode: 'date',
				sex: '请选择性别',
				border: false,
				actionSheetShow: false,
				labelPosition: 'left',
				date: '请选择日期',
				phone: '',
				actionSheetList: [{
						text: '男'
					},
					{
						text: '女'
					}
				],
				form: {
					name: '',
					intro: '',
				},
				rules: {
					name: [{
						required: true,
						message: '请输入姓名',
						// 可以单个或者同时写两个触发验证方式 
						trigger: ['change', 'blur'],
					}],
					// sex: [{
					// 	required: true,
					// 	message: '请选择性别',
					// 	trigger: 'change'
					// }, ],
					intro: [{
						min: 5,
						message: '简介不能少于5个字',
						trigger: 'change'
					}],
					// phone: [{
					// 		required: true,
					// 		message: '请输入手机号',
					// 		trigger: ['change', 'blur']
					// 	},
					// 	{
					// 		validator: (rule, value, callback) => {
					// 			// 调用uView自带的js验证规则，详见：https://www.uviewui.com/js/test.html
					// 			return this.$u.test.mobile(value);
					// 		},
					// 		message: '手机号码不正确',
					// 		// 触发器可以同时用blur和change，二者之间用英文逗号隔开
					// 		trigger: ['change', 'blur']
					// 	}
					// ]
				}
			}
		},
		methods: {
			submit() {
				this.$refs.uForm.validate(valid => {
					if (valid) {
						console.log('验证通过');
					} else {
						console.log('验证失败');
					}
				});
			},
			changeDate(e) {
				this.date = e.result;
				console.log(e);
			},
			changeSex(e) {
				console.log(e);
			},
			// 点击actionSheet回调
			actionSheetCallback(index) {
				this.sex = this.actionSheetList[index].text;
				console.log(this.sex)
			}
		},
		onReady() {
			this.$refs.uForm.setRules(this.rules);
		}
	}
</script>

<style lang="scss">
	.infowrap {
		padding-left: 35rpx;
		padding-top: 10rpx;
	
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
	
	.infomation{
		height: 300rpx;
		// background-color: #18B566;
		.formitem{
			padding-left: 35rpx;
			border: 1rpx solid #DCDFE6;
			box-sizing: border-box;
		}
	}

	.wrap {
		padding: 30rpx;
	}

	.u-row {
		margin: 40rpx 0;
	}

	.demo-layout {
		left: 35rpx;
		top: 305rpx;
		height: 200rpx;
		border-radius: 8rpx;
	}

	.bg-purple {
		background: #d3dce6;
	}

	.bg-purple-light {
		background: #e5e9f2;
	}
</style>
