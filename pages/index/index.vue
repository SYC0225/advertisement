<template>
	<view class="container999" @touchstart="refreshStart" @touchmove="refreshMove" @touchend="refreshEnd">
		<!-- 刷新事件isRefresh需要异步操作返回resolve -->
		<refresh ref="refresh" @isRefresh='isRefresh'></refresh>
		<view class='nav'>
			<!-- #ifdef H5 -->
				<view style="height: 44px;width: 100%;">边距盒子</view>
			<!-- #endif -->
			<!-- 搜索 -->
			<view class='searchInput999'>
				<view class='searchBox999'>
					<image src='/static/icon-search.png' class='search999'></image>
				</view>
				<input class='input999' placeholder="输入相关地区"></input>
			</view>
			<!-- 导航栏 agents导航栏标题 -->
			<navTab ref="navTab" :tabTitle="tabTitle" @changeTab='changeTab'></navTab>
		</view>
		<!-- swiper切换 swiper-item表示一页 scroll-view表示滚动视窗 -->
		<swiper style="min-height: 100vh;" :current="currentTab" @change="swiperTab">
			<swiper-item v-for="(listItem,listIndex) in list" :key="listIndex">
				<scroll-view style="height: 100%;" scroll-y="true" @scrolltolower="lower1" scroll-with-animation :scroll-into-view="toView">
				<view :id="'top'+listIndex" style="width: 100%;height: 180upx;">边距盒子</view>
				<view class='content'>
					<view class='card' v-for="(item,index) in listItem" v-if="listItem.length > 0" :key="index">
						<!-- 广告图片 -->
						<view class="adverImage">
							<image src="" mode=""></image>
						</view>
						<!-- 广告信息 -->
						<view class="info">
							<!-- 广告地址 -->
							<view class="address">
								<!-- 地址图标 -->
								<image src="" mode=""></image>
								<!-- 广告地址 -->
								<view class="addr">
									21111111111111111111111111
								</view>
							</view>
							<!-- 广告价位 -->
							<view class="price">
								广告租金:￥2333
							</view>
							<!-- 广告租期(长租、短租、月租、年租) -->
							<view class="tenancy">
								广告租期类型:长租、短租、月租、年租
							</view>
						</view>
					</view>
				</view>
				<view class='noCard' v-if="listItem.length===0">
					暂无信息
				</view>
				<view style="width: 100%;height: 100upx;opacity:0;">底部占位盒子</view>
				</scroll-view>
			</swiper-item>
		</swiper>
		<tabBar4 :currentPage="currentPage"></tabBar4>
	</view>
</template>

<script>
const util = require('../../util/util.js');
import refresh from '../../components/refresh.vue';
import navTab from '../../components/navTab.vue';
import tabBar4 from '../../components/tabBar4.vue';
export default {
	components: {refresh,navTab,tabBar4},
	data() {
		return {
			currentPage:'index',
			toView:'',//回到顶部id
			tabTitle:['固定广告位','移动广告位'], //导航栏格式 --导航栏组件
			currentTab: 0, //sweiper所在页
			pages:[1,1], //第几个swiper的第几页
			list: [[1, 2, 3, 4, 5, 6],['a', 'b', 'c', 'd', 'e', 'f']] //数据格式
		};
	},
	onLoad(e) {
		
	},
	onShow() {},
	onHide() {},
	methods: {
		toTop(){
			this.toView = ''
			setTimeout(()=>{
				this.toView = 'top' + this.currentTab
			},10)
		},
		changeTab(index){
			this.currentTab = index
		},
		// 其他请求事件 当然刷新和其他请求可以写一起 多一层判断。
		isRequest(pages) {
			return new Promise((resolve, reject) => {
				this.pages[this.currentTab]++
				var that = this
				setTimeout(() => {
					uni.hideLoading()
					// uni.showToast({
					// 	icon: 'none',
					// 	title: `请求第${that.currentTab + 1 }个导航栏的第${that.pages[that.currentTab]}页数据成功`
					// })
					let newData = ['新数据1','新数据2','新数据3']
					resolve(newData)
				}, 1000)
			})
		},
		// swiper 滑动
		swiperTab: function(e) {
			var index = e.detail.current //获取索引
			if(this.tabTitle.length<=5){
				this.$refs.navTab.navClick(index)
			}else{
				this.$refs.navTab.longClick(index)
			}
		},
		// 加载更多 util.throttle为防抖函数
		lower1: util.throttle(function(e) {
		console.log(`加载${this.currentTab}`)//currentTab表示当前所在页数 根据当前所在页数发起请求并带上page页数
		uni.showLoading({
			title: '加载中',
			mask:true
		})
			this.isRequest().then((res)=>{
				let tempList = this.list
				tempList[this.currentTab] = tempList[this.currentTab].concat(res)
				console.log(tempList)
				this.list = tempList
				this.$forceUpdate() //二维数组，开启强制渲染
			})
		}, 300),
		// 刷新touch监听
		refreshStart(e) {
			this.$refs.refresh.refreshStart(e);
		},
		refreshMove(e){
			this.$refs.refresh.refreshMove(e);
		},
		refreshEnd(e) {
			this.$refs.refresh.refreshEnd(e);
		},
		isRefresh(){
				setTimeout(() => {
					// uni.showToast({
					// 	icon: 'success',
					// 	title: '刷新成功'
					// })
					this.$refs.refresh.endAfter() //刷新结束调用
				}, 1000)
		}
	}
};
</script>

<style lang="scss">
		.container999 {
	  width: 100vw;
	  font-size: 28upx;
	  min-height: 100vh;
	  overflow: hidden;
	  color: #6B8082;
	  position: relative;
	  background-color: #f6f6f6;
	}
	.content {
		width: 100%;
	}
	
	.card {
		width: 90%;
		height: 368upx;
		background-color: white;
		margin: 0 auto 42upx auto;
		background: #FFFFFF;
		box-shadow: 0 0 5px 0 rgba(0, 0, 0, 0.10);
		border-radius: 5px;
		position: relative;
		.adverImage{
			width:50%;
			height:90%;
			position: absolute;
			left:10px;
			top: 8px;
			border-radius: 5px;
			border:1px solid #007AFF;
			image{
				width: 100%;
				height: 100%;
			}
		}
		.info{
			width: 42%;
			height: 90%;
			top:15px;
			right:10px;
			position: absolute;
			// border: 1px solid #007AFF;
			overflow: hidden;
			.address{
				width:97%;
				height: 40px;
				position: relative;
				top:0;
				// border: 1px solid #4CD964;
				border-radius: 5px;
				box-shadow: 1px 2px 2px #808080;
				image{
					width:40upx;
					height: 40upx;
					position: absolute;
					top: 0;
					left: 0;
					border:1px solid #DD524D;
				}
				.addr{
					width:80%;
					position: absolute;
					top: 0;
					left:45upx;
					color: #333333;
					font-size: 13px;
					word-wrap:break-word;
					word-break:normal;
				}
			}
			.price{
				position: relative;
				width:100%;
				top:10px;
				// border: 1px solid #F0AD4E ;
				border-radius: 5px;
				box-shadow: 1px 2px 2px #808080;
			}
			.tenancy{
				position: relative;
				width:100%;
				top: 25px;
				// border: 1px solid #F0AD4E ;
				border-radius: 5px;
				box-shadow: 1px 2px 2px #808080;
			}
		}
	}
	
	.noCard {
		width: 90%;
		height: 200upx;
		margin: auto;
		background-color: white;
		display: flex;
		align-items: center;
		justify-content: center;
		color: #999999;
		box-shadow: 0 0 10upx 0 rgba(0, 0, 0, 0.10);
		border-radius: 10upx;
	}
	
	
	.nav {
		position: fixed;
		left: 0;
		top: 0;
		color: white;
		width: 100%;
		display: flex;
		flex-direction: column;
		align-items: flex-start;
		justify-content: flex-start;
		font-size: 24upx;
		background-color: #50B7EA;
		z-index: 996;
	}
	
	.searchInput999 {
		width: 90%;
		margin: 0 auto;
		background: white;
		border-radius: 30upx;
		display: flex;
		align-items: center;
		justify-content: center;
		height: 56upx;
	}
	
	.search999 {
		width: 32upx;
		height: 32upx;
	}
	
	.searchBox999 {
		width: 56upx;
		height: 56upx;
		display: flex;
		justify-content: center;
		align-items: center;
	}
	
	.input999 {
		color: #999;
		width: 80%;
	}
</style>
