<template>
	<view class="container">
		<view class="form-container">
			<input type="text" placeholder="请输入邮箱"/>
			<input type="text" password="" placeholder="请输入密码"/>
			<!-- <button form-type="submit">登录</button> -->
			<Button class="button" type="primary" :disable="true">登录</Button>
			
		</view>
	</view>
</template>

<script>
	import Button from '../../components/Button.vue'
	export default {
		data() {
			return {
				type: 'logins'
			};
		},
		components:{
			Button
		}
	}
</script>

<style lang="scss">
	.form-container {
		display: flex;
		flex-direction: column;
		align-items: center;
		// border: $debug-border;
		input {
			border: 1rpx solid $color-main-light;
			padding: $space-normal;
			margin: $space-normal;
			border-radius: $space-normal;
			width: 60%;
			font-size: $text-small;
		}
		
		.button {
			
			padding: $space-normal;
			border-radius: $space-normal;
			font-size: $text-small;
			margin-top: 60rpx;
			height: 60rpx;
			width: 60%;
		}
	}
</style>
