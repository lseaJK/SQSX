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
		height: 128px;
	}

	.head {
		width: 326px;
		height: 254px;
		margin: 0 auto;
		text-align: center;
		box-sizing: content-box;

		.head_logo {
			width: 140rpx;
			margin: 0 auto;
		}

		.head_title {
			font-size: 26px;
			font-weight: bold;
			letter-spacing: 2rpx;
			color: #000;

		}
	}

	.login_wrapper {
		padding-top: 120rpx;

		.login_content {
			width: 686px;
			margin: 0 auto;
		}

		.login_item {
			padding: 10px;
			font-size: 16px;
			letter-spacing: 2rpx;
			height: 58px;
			border-bottom: 1px solid rgba($color: #000000, $alpha: 0.2);
			margin-bottom: 28px;
		}
		
		.login_btn{
			margin: 53px auto ;
			width: 686px;
			height: 96px;
			line-height: 96px;
			text-align: center;
			letter-spacing: 10px;
			background-color: rgb(226,62,40);
			color: #FFFFFF;
			border-radius: 10px;
		}
	}
	.login_opt{
		height: 40px;
		width: 370px;
		margin: 0 auto;
		text-align: center;
		color: #8F8F94;
		letter-spacing: 1px;
	}
	.login_visitor{
		position: absolute;
		bottom: 80px;
		left:290px;
		color: #8F8F94;
		letter-spacing: 1px;
	}
</style>
