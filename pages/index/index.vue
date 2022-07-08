<template>
	<view class="gender-select">
		<text class="gender-title">请选择性别</text>
		<radio-group class="radios">
			<radio style="padding: 20rpx;">男</radio>
			<radio style="padding: 20rpx;">女</radio>
		</radio-group>
		<button class="next-button">下一步</button>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				
			}
		},
		methods: {
			
		}
	}
</script>

<style>
	view {
		display: flex;
	}
	
	.gender-select {
		flex-direction: column;
	}
	
	.gender-title {
		margin-top: 200rpx;
		text-align: center;
		font-size: 40rpx;
		font-weight: 700;
	}
	
	.radios {
		align-self: center;
		justify-items: center;
	}
	
	.next-button {
		margin-top: 20rpx;
		font-size: 10rpx;
		background-color: #4cb6e8;
		border: none;
		color: #eff1fe;
	}
</style>