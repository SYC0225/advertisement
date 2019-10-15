<template>
	<view class="body">
		<image src="../../static/1.jpg" mode=""></image>
		<!-- 登录 -->
		<view class="login">
			<view class="title">
				登录
			</view>
			<!-- 用户名 -->
			<input type="text" v-model="username" placeholder="邮箱/电话号码"/>
			<!-- 密码 -->
			<input type="text" v-model="password" placeholder="密码6-10为数字和字母的组合" />
			<view class="btn" @tap="toLogin()">登录</view>
			<view class="res">					
				<view @tap="toPage('reg')">用户注册</view>
				<view @tap="toPage('resetpwd')">忘记密码?</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				username:'',
				password:'',
				// email:'',
				// phone:'',
			};
		},
		methods:{
			toLogin(){
				uni.hideKeyboard();
				if(!(/^([a-zA-Z0-9]+[_|\_|\.]?)*[a-zA-Z0-9]+@([a-zA-Z0-9]+[_|\_|\.]?)*[a-zA-Z0-9]+\.[a-zA-Z]{2,3}$/&&/^1[34578]\d{9}$/.test(this.username))){
					uni.showToast({
						title:'格式错误，请重新输入',
						icon: "none"
					})
					return false;
				}
				// 验证密码
				if(!(/^([0-9a-zA-Z]){8,18}$/.test(this.password))){
					uni.showToast({
						title:'密码错误',
						icon:'none'
					});
					return false;
				}
			},
			toPage(page) {
				uni.hideKeyboard()
				uni.navigateTo({
					url: page
				});
			},
		}
	}
</script>

<style lang="scss">
	.body{
		width:100%;
		height:100%;
		// background:#000;
		image{
			position:fixed;
			left:0;
			top:0;
			opacity:.4;
			z-index:998;
			width: 100%;
			height: 100%;
		}
		.login{
			position:absolute;
			z-index:999;
			width:70%;
			height:60%;
			// border: 1px solid #ff0000;
			top: 20%;
			left:15%;
			.title{
				color:#171717;
				font-size: 32px;
			}
			input{
				border: 1px solid #6e6e6e;
				border-radius: 5px;
				height:35px;
				margin-top: 20px;
			}
		}
		.res {
			display: flex;
			justify-content: space-between;
			align-items: center;
			height: 100upx;
			// color: rgba($color: #ffffff, $alpha: 0.8);
			color: #6e6e6e;
			font-size: 16px;
		}
		.btn {
			color: #6e6e6e;
			width: 100%;
			height: 35px;
			margin-top: 20px;
			display: flex;
			justify-content: center;
			align-items: center;
			border-radius: 5px;
			border: 1px solid #6e6e6e;
			// background-color: #fff;
			font-size: 40upx;
		}
	}
</style>
