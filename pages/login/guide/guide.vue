<template>
	<view class="content">
		<swiper class="swiper" 
		:autoplay="autoplay" 
		:duration="duration">
			<swiper-item>
				<view class="swiper-item">
					<!-- <view class="swiper-item-img"><image src="../../../static/guide/title_01.png" mode="aspectFit"></image></view> -->
					<!-- <view class="swiper-item-img"><image src="../../../static/guide/icon_01.png" mode="aspectFit"></image></view> -->
					<view class="swiper-item-img">
						<image src="../../../static/1.jpg" mode=""></image>
					</view>
				</view>
				<view class="jump-over" @tap="launchFlag()">{{jumpover}}</view>
			</swiper-item>
			<swiper-item>
				<view class="swiper-item">
					<view class="swiper-item-img"><image src="../../../static/guide/title_02.png" mode="aspectFit"></image></view>
					<view class="swiper-item-img"><image src="../../../static/guide/icon_02.png" mode="aspectFit"></image></view>
				</view>
				<view class="jump-over" @tap="launchFlag()">{{jumpover}}</view>
			</swiper-item>
			<swiper-item>
				<view class="swiper-item">
					<view class="swiper-item-img"><image src="../../../static/guide/title_03.png" mode="aspectFit"></image></view>
					<view class="swiper-item-img"><image src="../../../static/guide/icon_03.png" mode="aspectFit"></image></view>
				</view>
				<view class="jump-over" @tap="launchFlag()">{{jumpover}}</view>
			</swiper-item>
			<swiper-item>
				<view class="swiper-item">
					<view class="swiper-item-img"><image src="../../../static/guide/title_04.png" mode="aspectFit"></image></view>
					<view class="swiper-item-img"><image src="../../../static/guide/icon_04.png" mode="aspectFit"></image></view>
				</view>
				<view class="experience" @tap="launchFlag()">{{experience}}</view>
			</swiper-item>
		</swiper>
		<!-- <view class="uniapp-img"><image src="../../../static/guide/uniapp4@2x.png" mode="aspectFit"></image></view> -->
	</view>
</template>

<script>
	export default {
		data() {
			return {
				background: ['color1', 'color2', 'color3'],
				autoplay: false,
				duration: 500,
				jumpover: '跳过',
				experience: '立即体验'
			}
		},
		methods: {
			launchFlag: function(){
				/**
				 * 向本地存储中设置launchFlag的值，即启动标识；
				 */
				uni.setStorage({
						key: 'launchFlag',
						data: true,
				});
				uni.switchTab({
					url: '/pages/login/login'
				});
				
			}
		}
	}
</script>
<style>
	page,
	.content{
		width: 100%;
		height: 100%;
		/* background-size: 100% auto; */
		padding: 0;
	}
	.swiper{
		width: 100%;
		height: 100%;
		background: #FFFFFF;
	}
	.swiper-item {
		width: 100%;
		height: 100%;
		/*text-align: center; 
		position: relative;
		display: flex;
		justify-content: center;
		align-items:flex-end;
		flex-direction:column-reverse; */
		border: 1px solid #ff0000;
	}
	.swiper-item-img{
		width: 100%;
		height: 100%;
		/* height: auto; */
		/* margin: 0 auto; */
		border: 1px solid #00ff00;
		image{
			width:100%;
			height:100%;
		}
	}
	
	.jump-over,.experience{
		position: absolute;
		height: 60upx;
		line-height: 60upx;
		padding: 0 40upx;
		border-radius: 30upx;
		font-size: 32upx;
		color: #454343;
		border: 1px solid #FFFFFF;
		z-index: 999;
	}
	.jump-over{
		right: 45upx;
		top: 125upx;
		color: #FFFFFF;
	}
	.experience{
		right: 50%;
		margin-right: -105upx;
		bottom: 0;
	}
</style>
