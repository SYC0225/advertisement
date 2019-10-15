<template>
	<view class="body">
		<image src="../../static/1.jpg" mode=""></image>
		<!-- 注册 -->
		<view class="login">
			<view class="title">
				注册
			</view>
			<!-- 用户名 -->
			<input type="text" v-model="username" placeholder="邮箱/电话号码"/>
			<!-- 验证码 -->
			<input type="text" v-model="code" placeholder="请输入验证码"/>
			<!-- 密码 -->
			<input type="text" v-model="password" placeholder="密码8-18为数字和字母的组合" />
			<view class="btn" @tap="toreg()">注册</view>
			<view class="res">					
				<view @tap="toPage('login')">已有账号?去登录吧</view>
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
				code:''
			};
		},
		methods:{
			toreg(){
				uni.hideKeyboard();
				//验证用户名
				//当用户名为邮箱时
				if((/^([a-zA-Z0-9]+[_|\_|\.]?)*[a-zA-Z0-9]+@([a-zA-Z0-9]+[_|\_|\.]?)*[a-zA-Z0-9]+\.[a-zA-Z]{2,3}$/).test(this.username)){
					let email = this.username;
					console.log(email,"eeeeeeeeeeeeeeeeeeeee");
					uni.showToast({
						title:'邮箱注册成功',
						icon: "none"
					})
				}
				//当用户名为电话号码时
				if((/^1[34578]\d{9}$/).test(this.username)){
					let phone = this.username;
					console.log(phone,"ppppppppppppppppp");
					uni.showToast({
						title:'手机注册成功',
						icon: "none"
					})
				}
				// 用户名输入不规范
				if(!(/^([a-zA-Z0-9]+[_|\_|\.]?)*[a-zA-Z0-9]+@([a-zA-Z0-9]+[_|\_|\.]?)*[a-zA-Z0-9]+\.[a-zA-Z]{2,3}$/&&/^1[34578]\d{9}$/.test(this.username))){
					uni.showToast({
						title:'请输入有效用户名',
						icon: "none"
					})
					return false;
				}
				//验证验证码
				if(!(/^\w{6}/.test(this.code))){
					uni.showToast({
						title:'验证码错误',
						icon:"none"
					})
				}
				//验证密码
				if(!(/^[1-9a-zA-Z]{1}[0-9a-zA-Z]{7,17}$/.test(this.password))){
					uni.showToast({
						title:'密码错误',
						icon:'none'
					})
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
			justify-content:flex-end;
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


  