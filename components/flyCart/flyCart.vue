<template>
	<view>
		<image :src="imageUrl" :style="{left:bus_x+'px',top:bus_y+'px',transform:'scale('+scale+')'}" v-if="cartHidden" class="flycart">
		</image>
	</view>
</template>

<script>
	import flyCart from '../../utils/flyCart'
	export default {
		name: "flyCart",
		props: {
			/* 当前 x ,y 值 */
			current: {
				type: Object,
				default: {}
			},
			/* 图片 url  */
			imageUrl: {
				type: String,
				default: 'https://pic.cnblogs.com/avatar/1628917/20201219134424.png'
			}
		},
		data() {
			return {
				cartHidden: true,
				bus_x: 0,
				bus_y: 0,
				scale: 0,
				end: {},
				start: {},
				timer:''
			};
		},
		methods: {
			startCart() {
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
				this.start = {}
				console.log(this.current,'this.current');
				this.start.x= this.current.x
				this.start.y = this.current.y
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
.flycart{
	   width:80rpx;
	   height:80rpx;
	   position:fixed;
	   z-index:1010;
	}
</style>
