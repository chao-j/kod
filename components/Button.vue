<template>
	<view :class="classArr" >
		<slot />
	</view>
</template>

<script>
	export default {
		data(){
			return {
				
			}
		},
		props:{
			disable: {
				type: Boolean,
				default: false
			},
			type: {
				type: String,
				default: 'primary'
			}
		},
		methods:{
			onClick(){
				
			}
		},
		computed:{
			classArr() {
				let arr = {}
				console.log(this.type,this.disable)
				if(this.type == 'primary'){
					arr['container'] = true
				}
				if(this.disable){
					arr['disable'] = true
				}
				console.log(arr)
				return arr
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
		background-color: $color-main-light;
	}
</style>
