<template>
	<view>
		<view style="height: var(--status-bar-height);"></view>
		<uni-nav-bar left-icon="back" title="模型微调" style="width: 100%;" shadow @clickLeft="top_bar_back"></uni-nav-bar>
		
		<image class="body-image" src="../../static/whole-body.jpg"></image>
		
		<view class="uni-title slider-title">身高 / cm</view>
		<slider value="180" min="120" max="220" show-value />
		<view class="uni-title slider-title">腿长占身高比例 / %</view>
		<slider value="50" min="30" max="70" show-value />
		<view class="uni-title slider-title">臂长 / cm</view>
		<slider value="85" min="50" max="120" show-value />
					
		<navigator url="/pages/editParts/editParts" hover-class="navigator-hover">
			<button type="default" class="next-button">下一步</button>
		</navigator>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				
			}
		},
		methods: {
			top_bar_back() {
				uni.navigateTo({
					url: "/pages/index/index"
				})
			}
		}
	}
</script>

<style>
	page {
		background-color: #f2f2f2;
	}
	
	.body-image {
		width: 800rpx;
		height: 800rpx;
		align-self: center;
	}
	
	.slider-title {
		margin-left: 30rpx;
		margin-top: 20rpx;
	}
	
	.next-button {
		border-radius: 150rpx;
		margin-left: 30rpx;
		margin-right: 30rpx;
		margin-top: 40rpx;
		font-weight: 500rpx;
		font-size: 35rpx;
		background-color: #4cb6e8;
		border: none;
		color: #eff1fe;
	}
</style>