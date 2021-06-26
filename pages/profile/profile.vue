<template>
	<view class="content">

		<fly-cart :current="currentXY" ref="flyCart"/>
		<view class="box">
			<view class="boxli">
				<image class="boximg" src="https://pic.cnblogs.com/avatar/1628917/20201219134424.png"></image>
				<view class="add" @click="startCart" ref="flyCart">
					+
				</view>
			</view>
			<view class="boxli">
				<image class="boximg" src="https://pic.cnblogs.com/avatar/1628917/20201219134424.png"></image>
				<view class="add" @click="startCart">
					+
				</view>
			</view>
			<view class="boxli">
				<image class="boximg" src="https://pic.cnblogs.com/avatar/1628917/20201219134424.png"></image>
				<view class="add" @click="startCart">
					+
				</view>
			</view>
			<view class="boxli">
				<image class="boximg" src="https://pic.cnblogs.com/avatar/1628917/20201219134424.png"></image>
				<view class="add" @click="startCart">
					+
				</view>
			</view>
			<view class="boxli">
				<image class="boximg" src="https://pic.cnblogs.com/avatar/1628917/20201219134424.png"></image>
				<view class="add" @click="startCart">
					+
				</view>
			</view>
			<view class="boxli">
				<image class="boximg" src="https://pic.cnblogs.com/avatar/1628917/20201219134424.png"></image>
				<view class="add" @click="startCart">
					+
				</view>
			</view>
			<view class="boxli">
				<image class="boximg" src="https://pic.cnblogs.com/avatar/1628917/20201219134424.png"></image>
				<view class="add" @click="startCart">
					+
				</view>
			</view>
		</view>
		<view class="cart">
			购物车
		</view>
	</view>
</template>
<!--  -->
<script>
	import fly from '../../utils/flyCart'
	import flyCart from '../../components/flyCart/flyCart'
	export default {
		components:{
			flyCart
		},
		data() {
			return {
				currentXY:{}
			}
		},
		methods: {
			startCart(e) {
				this.currentXY = {x:e.touches[0].clientX,y:e.touches[0].clientY} 
				this.$nextTick(()=>{
					this.$refs.flyCart.startCart()
				})
			}
		}
	}
</script>

<style>
	/* pages/index/index.wxss */
	page {
		padding: 24rpx;
		box-sizing: border-box;
	}

	.boxli {
		height: 200rpx;
		border: 1px solid #eee;
		position: relative;
	}

	.add {
		width: 50rpx;
		height: 50rpx;
		background-color: #DB7093;
		border-radius: 50%;
		display: flex;
		align-items: center;
		justify-content: center;
		color: #fff;
		position: absolute;
		right: 24rpx;
		bottom: 24rpx;
	}

	.boximg {
		width: 180rpx;
		height: 180rpx;
		margin: 10rpx;
	}

	.cart {
		position: fixed;
		bottom: 0;
		left: 0;
		background-color: #DB7093;
		color: #fff;
		width: 120rpx;
		height: 60rpx;
		border-radius: 10rpx;
		text-align: center;
		color: #fff;
		line-height: 60rpx;
		margin: 24rpx;
	}
	.flycart{
	   width:80rpx;
	   height:80rpx;
	   position:fixed;
	   z-index:1010;
	}
</style>
