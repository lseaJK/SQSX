<template>
	<view>
		<view class="titlebar"></view>
		
		<view class="head">
			<image class="head_logo" mode="widthFix" src="../../static/logo.png"></image>
			<text class="head_title">
				\n上海大学计算机学院\n数字化党建平台
			</text>
		</view>
		
		<view class="login_wrapper">
			<view class="login_content">
				<view class="login_item">
					<a style="float: right;">获取验证码</a>
					<input type="number" placeholder="请输入手机号" />
				</view>
			</view>
			<view class="login_content">
				<view class="login_item">
					<input type="text" placeholder="请输入验证码" />
				</view>
			</view>
			<view class="login_content">
				<view class="login_item">
					<input type="text" placeholder="请输入登陆密码" />
				</view>
			</view>
			
			<view class="login_btn">
				<view @click="login()">登录</view>
			</view>
		</view>
		
		<view class="login_opt">忘记密码请找管理员重置</view>
		
		<view @click="loginAsVisitor()" class="login_visitor">使用游客身份</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {

			};
		}
	}
</script>

<style lang="scss">
	.titlebar {
		height: 128rpx;
	}

	.head {
		width: 326rpx;
		height: 254rpx;
		margin: 0 auto;
		text-align: center;
		box-sizing: content-box;

		.head_logo {
			width: 70rpx;
			margin: 0 auto;
		}

		.head_title {
			font-size: 35rpx;
			font-weight: bold;
			letter-spacing: 1rpx;
			color: #000;

		}
	}

	.login_wrapper {
		padding-top: 60rpx;

		.login_content {
			width: 686rpx;
			margin: 0 auto;
		}

		.login_item {
			padding: 10rpx;
			font-size: 16rpx;
			letter-spacing: 1rpx;
			height: 58rpx;
			border-bottom: 1rpx solid rgba($color: #000000, $alpha: 0.2);
			margin-bottom: 28rpx;
		}
		
		.login_btn{
			margin: 53rpx auto ;
			width: 686rpx;
			height: 96rpx;
			line-height: 96rpx;
			text-align: center;
			letter-spacing: 10rpx;
			background-color: rgb(226,62,40);
			color: #FFFFFF;
			border-radius: 10rpx;
		}
	}
	.login_opt{
		height: 40rpx;
		width: 370rpx;
		margin: 0 auto;
		text-align: center;
		color: #8F8F94;
		letter-spacing: 1rpx;
	}
	.login_visitor{
		position: absolute;
		bottom: 80rpx;
		left:290rpx;
		color: #8F8F94;
		letter-spacing: 1rpx;
	}
</style>
