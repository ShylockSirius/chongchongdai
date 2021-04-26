<template>
	<view class="container">
		<view class="banner">
			<image src="../../static/images/index/fruit.jpg" mode="" class="bg"></image>
			<view class="intro">
				<view class="greet">您好，{{ isLogin ? member.nickname : '游客' }}</view>
				<view class="note">好水果，虫虫带(●'◡'●)</view>
			</view>
		</view>
		<view class="content">
			<view class="entrance">
				<view class="item" @tap="takein">
					<image src="/static/images/index/zq.png" class="icon"></image>
					<view class="title">自取</view>
				</view>
				<view class="item" @tap="takeout">
					<image src="/static/images/index/wm.png" class="icon"></image>
					<view class="title">捎带</view>
				</view>
			</view>
			<view class="info" @tap="integrals">
				 
				 <view class="title" style="color:grey;
				font-weight: 600;">我的订单</view >
				 
			</view>
			<view class="info"  @tap="invite">
				 
				 <view class="title" style="color:grey;
				font-weight: 600;">我要捎带</view >
				 
			</view>
		</view>
		</view>
	</view>
</template>

<script>
	import {mapState, mapGetters} from 'vuex'
	
	export default {
		data() {
			return {
			}
		},
		computed: {
			...mapState(['member']),
			...mapGetters(['isLogin'])
		},
		methods: {
			takein() {
				this.$store.commit('SET_ORDER_TYPE', 'takein')
				uni.switchTab({
					url: '/pages/menu/menu'
				})
			},
			takeout() {
				if(!this.isLogin) {
					uni.navigateTo({url: '/pages/login/login'})
					return
				}
				uni.navigateTo({
					url: "/pages/address/address?is_choose=true"	
				})
			},
			integrals() {
				if(!this.isLogin) {
					uni.navigateTo({url: '/pages/login/login'})
					return
				}
				uni.navigateTo({
					url: '/pages/take-foods/take-foods'
				})
			},
			packages() {
				uni.navigateTo({
					url: '/pages/packages/index'
				})
			},
		
			invite() {
				uni.navigateTo({
					url: '/pages/packages/detail'
				})
			}
		}
	}
</script>

<style lang="scss" scoped>
/* #ifdef H5 */
page {
	height: auto;
	min-height: 100%;
}
/* #endif */

.banner {
	position: relative;
	width: 100%;
	height: 600rpx;
	
	.bg {
		width: 100%;
		height: 600rpx;
	}
	
	.intro {
		position: absolute;
		top: calc(50rpx + var(--status-bar-height));
		left: 40rpx;
		color: green ;
		display: flex;
		flex-direction: column;
		
		.greet {
			font-size: $font-size-lg;
			margin-bottom: 10rpx;
		}
		
		.note {
			font-size: $font-size-sm;
		}
	}
}

.content {
	padding: 0 30rpx;
}

.entrance {
	position: relative;
	margin-top: -80rpx;
	margin-bottom: 30rpx;
	border-radius: 10rpx;
	background-color: #ffffff;
	box-shadow: $box-shadow;
	padding: 30rpx 0;
	display: flex;
	align-items: center;
	justify-content: center;
	
	.item {
		flex: 1;
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		position: relative;
		
		&:nth-child(1):after {
			content: '';
			position: absolute;
			width: 1rpx;
			background-color: #ddd;
			right: 0;
			height: 100%;
			transform: scaleX(0.5) scaleY(0.8);
		}
		
		.icon {
			width: 84rpx;
			height: 84rpx;
			margin: 20rpx;
		}
		
		.title {
			font-size: 30rpx;
			color: $text-color-base;
			font-weight: 600;
		}
	}
}

.info {
	position: relative;
	margin-bottom: 30rpx;
	border-radius: 10rpx;
	background-color: #ffffff;
	box-shadow: $box-shadow;
	padding: 30rpx;
	display: flex;
	align-items: center;
	justify-content: center;
	
	.integral_section {
		flex: 1;
		display: flex;
		flex-direction: column;
		justify-content: center;
		
		.top {
			display: flex;
			align-items: center;
			
			.title {
				font-size: 30rpx;
				color: $text-color-base;
				font-weight: 600;
			}
			.value {
				font-size: 44rpx;
				font-weight: bold;
			}
		}
		
		.bottom {
			font-size: $font-size-sm;
			color: $text-color-assist;
			display: flex;
			align-items: center;
		}
	}
	
	.qrcode_section {
		color: $color-primary;
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
		font-size: $font-size-sm;
		
		image {
			width: 40rpx;
			height: 40rpx;
			margin-bottom: 10rpx;
		}
	}
}

.navigators {
	width: 100%;
	margin-bottom: 20rpx;	
	border-radius: 10rpx;
	background-color: #ffffff;
	box-shadow: $box-shadow;
	padding: 20rpx;
	display: flex;
	align-items: stretch;
	
	.left {
		width: 340rpx;
		margin-right: 20rpx;
		display: flex;
		padding: 0 20rpx;
		flex-direction: column;
		font-size: $font-size-sm;
		color: $text-color-base;
		background-color: #F2F2E6;
		
		.grid {
			height: 50%;
			display: flex;
		}
	}
	
	.right {
		width: 290rpx;
		display: flex;
		flex-direction: column;
		
		.tea-activity, .member-gifts {
			width: 100%;
			display: flex;
			padding: 20rpx;
			font-size: $font-size-sm;
			color: $text-color-base;
			align-items: center;
			position: relative;
		}
		
		.tea-activity {
			background-color: #FDF3F2;
			margin-bottom: 20rpx;
		}
		
		.member-gifts {
			background-color: #FCF6D4;
		}
		
		.right-img {
			flex: 1;
			position: relative;
			margin-left: 20rpx;
			margin-right: -20rpx;
			margin-bottom: -20rpx;
			display: flex;
			align-items: flex-end;
			
			image {
				width: 100%;
			}
		}
	}
	
	.mark-img {
		width: 30rpx;
		height: 30rpx;
		margin-right: 10rpx;
	}
	
	.yzclh-img {
		height: 122.96rpx;
		width: 214.86rpx;
	}
}

.member-news {
	width: 100%;
	margin-bottom: 30rpx;
	.header {
		display: flex;
		align-items: center;
		justify-content: space-between;
		padding: 20rpx 0;
		
		.title {
			font-size: $font-size-lg;
			font-weight: bold;
		}
		
		.iconfont {
			font-size: 52rpx;
			color: $text-color-assist;
		}
	}
	
	.list {
		width: 100%;
		display: flex;
		flex-direction: column;
		
		.item {
			width: 100%;
			height: 240rpx;
			position: relative;
			
			image {
				width: 100%;
				height: 100%;
				border-radius: 8rpx;
			}
			
			.title {
				position: relative;
				font-size: 32rpx;
				font-weight: 500;
				width: 100%;
				top: -70rpx;
				left: 16rpx;
				color: #ffffff;
			}
		}
	}
}
</style>
