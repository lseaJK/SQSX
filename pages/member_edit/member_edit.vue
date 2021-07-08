<template>
<view class="navheadBG">
		<view class="title">
			我是党员
		</view>
		<view class="tools">
			<u-icon class="toolItems" name="camera-fill" color="#fff" size="48"></u-icon>

			<u-search placeholder="关键词搜索" v-model="keyword" :clearabled="true" :show-action="false" shape="square"
				size="48"></u-search>

			<u-icon class="toolItems" name="scan" color="#fff" size="48"></u-icon>

		</view>
		<view class="wrap">
				<u-row gutter="16" justify="space-between">
					<u-col span="4">
						<image class="demo-layout" src="../../static/member/兑换.png" mode="center"></image>
					</u-col>
					<u-col span="8">
						<view class="demo-layout">
							<view>姓名</view>
							<view>积分</view>
						</view>
					</u-col>
				</u-row>
			</view>
		<view class="infomation">
				<u-form :model="form" ref="uForm">
					<u-form-item label="姓名" prop="name">
						<u-input v-model="form.name" />
					</u-form-item>
					<u-form-item :label-position="labelPosition" label="性别" prop="sex">
						<u-input :border="border" type="select" :select-open="actionSheetShow" v-model="sex" placeholder="请选择性别" @click="actionSheetShow = true"></u-input>
					</u-form-item>
					<!-- <u-action-sheet :list="actionSheetList" v-model="showSex" @click="actionSheetCallback"></u-action-sheet> -->
					<view @click="showDate = true">
						<u-form-item label="入党日期">
							{{date}}
						</u-form-item>
					</view>
					<u-form-item :rightIconStyle="{color: '#888', fontSize: '32rpx'}" :label-position="labelPosition" label="联系方式" prop="phone" label-width="150">
						<u-input :border="border" placeholder="请输入手机号" v-model="phone" type="number"></u-input>
					</u-form-item>
				<u-form-item label="亮出承诺" prop="intro">
						<u-input v-model="form.intro" />
					</u-form-item>
				</u-form>
				<u-button @click="submit">修改</u-button>
		</view>
		<u-calendar v-model="showDate" :mode="mode" @change="changeDate()"></u-calendar>
		<u-action-sheet :list="actionSheetList" v-model="actionSheetShow" @click="actionSheetCallback"></u-action-sheet>
	</view>

</template>

<script>
	export default {
		data() {
			return {
				showDate: false,
				mode: 'date',
				sex:'sex',
				border: false,
				actionSheetShow: false,
				labelPosition: 'left',
				date:'请选择日期',
				phone: '',
				actionSheetList: [
									{
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
								name: [
									{ 
										required: true, 
										message: '请输入姓名', 
										// 可以单个或者同时写两个触发验证方式 
										trigger: ['change','blur'],
									}
								],
								sex: [
									{
										required: true,
										message: '请选择性别',
										trigger: 'change'
									},
								],
								intro: [
									{
										min: 5, 
										message: '简介不能少于5个字', 
										trigger: 'change'
									}
								],
								phone: [
									{
										required: true,
										message: '请输入手机号',
										trigger: ['change','blur']
									},
									{
										validator: (rule, value, callback) => {
											// 调用uView自带的js验证规则，详见：https://www.uviewui.com/js/test.html
											return this.$u.test.mobile(value);
										},
										message: '手机号码不正确',
										// 触发器可以同时用blur和change，二者之间用英文逗号隔开
										trigger: ['change','blur']
									}
								]
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
					this.date=e.result;
						console.log(e);
					},
			changeSex(e){
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
.navheadBG {
		position:relative;
		height: 220rpx;
		width: 750rpx;
		border-bottom-left-radius: 80rpx;
		border-bottom-right-radius: 80rpx;
		background-color: rgb(226,62,40);
		padding-top: 20rpx;
		color: #fff;

		.title {
			height:80rpx;
			font-size: 35rpx;
			letter-spacing: 10rpx;
			text-align: center;
		}
		.tools {
			height: 70rpx;
			display: flex;
		
			.toolItems {
				margin: 0 50rpx;
			}
		}
		
	}
	.wrap {
			padding: 30rpx;
		}
	
		.u-row {
			margin: 40rpx 0;
		}
	
		.demo-layout {
			left:35rpx;
			top:305rpx;
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
