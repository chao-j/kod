<template>
	<view :class="classArr" @click="onClick()">
		<template v-if="!loading">
			<slot />
		</template>
		<view :animation="animationData" v-else class="loading">
			<view class="dot" :animation="animationData[0]"></view>
			<view class="dot" :animation="animationData[1]"></view>
			<view class="dot" :animation="animationData[2]"></view>
		</view>
		
		<!-- <view  style="width: 100rpx;height: 100rpx;background-color: #007AFF;"></view> -->
	</view>
</template>

<script>
	export default {
		data(){
			return {
				animationData:[]
			}
		},
		props:{
			disable: {
				type: Boolean,
				default: false
			},
			loading: {
				type: Boolean,
				default: false
			},
			type: {
				type: String,
				default: 'primary'
			}
		},
		// 这是组件 没有onShow等事件！
		created:function(){
			this.animIndex = true
		},
		mounted:function(){
			this.animTimer && clearTimeout(this.animTimer)
		},
		methods:{
			onClick:function(){
				this.$emit('click')
			},
			startAnim:function(){
				this.animationData = new Array()
				for(let i = 0; i < 3; i++){
					let anim = this.createAnim(i)
					anim.opacity(this.animIndex ? 0 : 1).step()
					this.animationData.push(anim.export())
				}
				this.animIndex = !this.animIndex
			},
			repeatAnim:function(){
				this.animTimer && clearTimeout(this.animTimer)
				this.startAnim()
				this.animTimer = setTimeout(()=>{
					this.repeatAnim()
				},610)
			},
			createAnim:function(i){
				return uni.createAnimation({
					duration: 200,
					delay: i * 200
				})
			}
		},
		computed:{
			classArr() {
				let arr = {}
				if(this.type == 'primary'){
					arr['container'] = true
				}
				if(this.disable){
					arr['disable'] = true
				}
				return arr
			}
		},
		watch:{
			loading(val){
				// loading动画
				if(val){
					// 如果this是在created里初始化的，这些this调用前都要reload一下
					// 如果只是保存刷新，可能没有this
					this.repeatAnim()
				}
			}
		}
	}
</script>

<style scoped lang="scss">
	.container {
		display: flex;
		justify-content: center;
		align-items: center;
		background-color: $color-main;
		color: $color-text-mian;
	}
	.disable {
		background-color: $color-main-light-pain;
	}
	.loading{
		// width: 22rpx;
		height: 30rpx;
		// border: $debug-border;
		display: flex;
		justify-content: center;
		align-items: center;
		.dot{
			width: 10rpx;
			height: 10rpx;
			border-radius: 5rpx;
			background-color: #fff;
			margin: 0 5rpx;
		}
	}
</style>
