<template>
	<view class="container">
		<view class="position-relative">
			<image src="https://ss0.bdstatic.com/70cFuHSh_Q1YnxGkpoWK1HF6hhy/it/u=4059091273,1134253273&fm=26&gp=0.jpg" class="bg"></image>
		</view>
		
		<view style="padding: 0 30rpx;">
			<!-- user box begin -->
			<view class="d-flex flex-column bg-white user-box">
				
				<view class="d-flex align-items-center">
					<view class="avatar">
						<image :src="isLogin ? member.avatar : '/static/images/mine/default.png'"></image>
						
					</view>
					<view class="d-flex flex-column flex-fill overflow-hidden" style="margin-top: 20rpx;">
						<view v-if="isLogin" class="font-size-lg font-weight-bold d-flex justify-content-start align-items-center"
							@tap="userinfo">
							<view class="text-truncate">{{ member.nickname }}</view>
							<view class="iconfont iconarrow-right line-height-100"></view>
						</view>
						<view v-else class="font-size-lg font-weight-bold" @tap="login">请点击授权登录</view>
						 
						 
					</view>
					 
				</view>
				<!-- user grid begin -->
				<view class="w-100 d-flex align-items-center just-content-center">
					<view class="user-grid" @tap="coupons">
						<view class="value font-size-extra-lg font-weight-bold text-color-base">
							{{  isLogin ? member.couponNum : '***' }}
						</view>
						<view class="font-size-sm text-color-assist">完成捎带</view>
					</view>
					<view class="user-grid" @tap="">
						<view class="value font-size-extra-lg font-weight-bold text-color-base">
							{{  isLogin ? member.pointNum : '***' }}
						</view>
						<view class="font-size-sm text-color-assist">违约次数</view>
					</view>
					<view class="user-grid" @tap="">
						<view class="value font-size-extra-lg font-weight-bold text-color-base">
							{{  isLogin ? member.balance : '***' }}
						</view>
						<view class="font-size-sm text-color-assist">余额</view>
					</view>
					<view class="user-grid" @tap="">
						<view class="value font-size-extra-lg font-weight-bold text-color-base">
							{{  isLogin ? member.giftBalance : '***' }}
						</view>
						<view class="font-size-sm text-color-assist">捎带中</view>
					</view>
				</view>
				<!-- user grid end -->
			</view>
			<!-- user box end -->
		 
			<!-- banner begin -->
			 
			<!-- bennaer end -->
		</view>
		<!-- service box begin -->
		<view class="service-box">
			<view class="font-size-lg text-color-base font-weight-bold" style="margin-bottom: 20rpx;">我的服务</view>
			<view class="row">
				 
				 
				 
				<view class="grid"  @tap="shaodai">
					<view class="image">
						<image src="/static/images/mine/daizi.png"></image>
					</view>
					<view>捎带订单</view>
				</view>
				<view class="grid" @tap="orders">
					<view class="image">
						<image src="/static/images/mine/wddd.png"></image>
					</view>
					<view>我的订单</view>
				</view>
				<view class="grid" @tap="userinfo">
					<view class="image">
						<image src="/static/images/mine/wdzl.png"></image>
					</view>
					<view>我的资料</view>
				</view>
				<view class="grid" @tap="addresses">
					<view class="image">
						<image src="/static/images/mine/shdz.png"></image>
					</view>
					<view>收货地址</view>
				</view>
				 
			</view>
		</view>
		<!-- service box end -->
		<!-- tips begin -->
		<view class="d-flex just-content-center align-items-center text-color-assist" style="padding: 30rpx 0; font-size: 22rpx;">
			 
		</view>
		<!-- tisps end -->
	</view>
</template>

<script>
	import {mapState, mapGetters} from 'vuex'
	export default {
		data() {
			return {
				newIcon: 'https://img-shop.qmimg.cn/s16/images/2020/05/12/ffb0613dded704b6.png'
			}
		},
		computed: {
			...mapState(['member']),
			...mapGetters(['isLogin']),
			growthValue() {
				if(!this.isLogin) return 0
				const {currentValue, needValue} = this.member
				return currentValue / (currentValue + needValue) 
			}
		},
		onLoad() {
		},
		methods: {
			login() {
				uni.navigateTo({
					url: '/pages/login/login'
				})
			},
			
			shaodai() {
				if(!this.isLogin) {
					this.login()
					return
				}
				uni.navigateTo({
					url: '/pages/packages/bringings'
				})
			},
			addresses() {
				if(!this.isLogin) {
					this.login()
					return
				}
				uni.navigateTo({
					url: '/pages/address/address'
				})
			},
	
			
			orders() {
				if(!this.isLogin) {
					this.login()
					return
				}
				uni.navigateTo({
					url: '/pages/orders/orders'
				})
			},
			
			userinfo() {
				if(!this.isLogin) {
					this.login()
					return
				}
				uni.navigateTo({
					url: '/pages/mine/userinfo'
				})
			}
			
		}
	}
</script>

<style lang="scss" scoped>
page {
	height: auto;
	min-height: 100%;
}	

.bg {
	width: 100%;
	height: calc(410 / 594 * 750rpx);
}

.hym-btn {
	position: absolute;
	top: 40rpx;
	right: 40rpx;
	color: $color-primary;
	display: flex;
	align-items: center;
	justify-content: center;
	border-radius: 50rem;
	font-size: $font-size-sm;
	box-shadow: 0 0 20rpx rgba(66,66,66,0.1);
	&::after {
		border: 0;
	}
	
	image {
		width: 30rpx;
		height: 30rpx;
		margin-right: 10rpx;
	}
}

.user-box {
	position: relative;
	border-radius: 8rpx; 
	margin-bottom: 30rpx;
	margin-top: -115rpx;
	box-shadow: $box-shadow;
}

.avatar {
	position: relative;
	margin-top: -35rpx;
	margin-left: 35rpx;
	margin-right: 35rpx;
	width: 160rpx;
	height: 160rpx;
	border-radius: 100%;
	display: flex;
	align-items: center;
	justify-content: center;
	background-color: #FFFFFF;
	box-shadow: 0 0 20rpx rgba($color: #000000, $alpha: 0.2);
	
	image {
		width: 140rpx;
		height: 140rpx;
		border-radius: 100%;
	}
	
	.badge {
		position: absolute;
		right: -10rpx;
		bottom: -10rpx;
		background-color: #FFFFFF;
		border-radius: 50rem;
		display: flex;
		align-items: center;
		justify-content: center;
		color: $color-warning;
		font-size: 24rpx;
		padding: 8rpx 16rpx;
		box-shadow: 0 0 20rpx rgba($color: #000000, $alpha: 0.2);
		
		image {
			width: 30rpx;
			height: 30rpx;
		}
	}
}

.level-benefit {
	margin-left: 35rpx;
	padding: 10rpx 0 10rpx 30rpx;
	border-radius: 50rem 0 0 50rem;
}

.user-grid {
	width: 25%;
	padding: 30rpx;
	display: flex;
	flex-direction: column;
	align-items: center;
	justify-content: center;
	
	.value {
		margin-bottom: 20rpx;
	}
}

.level-benefit-box {
	border-radius: 8rpx; 
	margin-bottom: 30rpx;
	box-shadow: 0 10rpx 8rpx rgba($color: #878889, $alpha: 0.1);
	width: 100%;
	display: flex;
	padding: 30rpx;
	flex-direction: column;
	background-color: #FFFFFF;
	
	.row {
		display: flex;
		padding: 30rpx 0 20rpx;
		justify-content: space-around;
		align-items: center;
		
		.grid {
			width: 20%;
			display: flex;
			flex-direction: column;
			font-size: $font-size-sm;
			color: $text-color-assist;
			align-items: center;

			image {
				width: 80rpx;
				height: 80rpx;
				margin-bottom: 10rpx;
			}
		}
	}
}

.banner {
	width: 100%;
	border-radius: 8rpx;
	margin-bottom: 30rpx;
}

.service-box {
	width: 100%;
	background-color: #FFFFFF;
	padding: 32rpx 30rpx 10rpx;
	box-shadow: $box-shadow;
	
	.row {
		display: flex;
		flex-wrap: wrap;
		color: $text-color-assist;
		font-size: $font-size-sm;
		padding-bottom: -40rpx;
		
		.grid {
			display: flex;
			flex-direction: column;
			justify-content: center;
			align-items: center;
			margin-bottom: 40rpx;
			width: 25%;
			position: relative;
			
			.image {
				image {
					width: 80rpx;
					height: 80rpx;
					margin-bottom: 20rpx;
				}
			}
			
			.new-badage {
				width: 40rpx;
				height: 40rpx;
				position: absolute;
				top: 0;
				right: 30rpx;
			}
		}
	}
}
</style>
