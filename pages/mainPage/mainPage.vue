<template>
	<view class="content">
		<image class="logo" src="/static/human-man-scan-190m-01.jpg">
			<image @click="arm_click" class="circle-button" style="position: absolute; top: 200rpx; left: 230rpx;" src="../../static/circle-button.png"/>
			<image @click="body_click" class="circle-button" style="position: absolute; top: 240rpx; left: 350rpx;" src="../../static/circle-button.png"/>
			<image @click="leg_click" class="circle-button" style="position: absolute; top: 550rpx; left: 300rpx;" src="../../static/circle-button.png"/>
		</image>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				
			}
		},
		onLoad() {
			
		},
		methods: {
			arm_click() {
				
			},
			body_click() {
				
			},
			leg_click() {
				
			}
		}
	}
</script>

<style>
	page {
		background-color: #f2f2f2;
	}
	
	.content {
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
	}

	.logo {
		width: 800rpx;
		height: 800rpx;
		align-self: center;
	}
	
	.circle-button {
		width: 50rpx;
		height: 50rpx;
	}

	.text-area {
		display: flex;
		justify-content: center;
	}
</style>
