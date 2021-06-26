<template>
	<view class="content">

		<image class="flycart" v-if="cartHidden" :src="imageUrl"
			:style="{left:bus_x+'px',top:bus_y+'px',transform:'scale('+scale+')'}"></image>

		<view class="box">
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
	import flyCart from '../../utils/flyCart'
	export default {
		data() {
			return {
				title: 'Hello',
				cartHidden: true,
				imageUrl: 'https://pic.cnblogs.com/avatar/1628917/20201219134424.png',
				bus_x: 0,
				bus_y: 0,
				scale: 0,
				end: {},
				start: {},
				timer:''
			}
		},
		methods: {
			startCart(e) {
				clearInterval(this.timer)
				this.cartHidden = true
				this.end = {
					x: 375 * 1 / 5,
					y: 600
				}
				/* 获取屏幕宽高 */
				const windowWidth = uni.getSystemInfoSync().windowWidth
				const windowHeight = uni.getSystemInfoSync().windowHeight
				/* 购物车所在的位置 */
				this.end.y = windowHeight - 20
				this.end.x = windowWidth * 1 / 5 - 50
				/* 开启购物车 */
				/* this.start 储存起始点 clientY clientY  ,this.end储存最终点 clientX clientY */
				console.log(e);
				this.start = {}
				this.start.x= e.touches[0].clientX
				this.start.y = e.touches[0].clientY
				console.log(this.start,this.end);
				
				const travelList = flyCart([this.start.x, this.start.y], [this.end.x, this.end.y], 25, 50)
				console.log(travelList);
				this.startAnimation(travelList)
				
			},
			startAnimation(travelList) {
				let index = 0
				this.bus_x = this.start['x']
				this.bus_y = this.start['y']
				if (travelList.length === 0) return
				this.timer = setInterval(() => {
					index++
					const currentPoint = travelList.shift()
					this.bus_x = currentPoint[0] /* left 值 */
					this.bus_y = currentPoint[1]/* top值 */
					this.scale = 1 - index / 25 /* 缩放比 */
					if (travelList.length === 0) {
						clearInterval(this.timer)
						this.cartHidden = false
					}
				}, 33)
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
