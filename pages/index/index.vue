<template>
	<view class="gender-select" style="margin-top: 200rpx;">
		<text class="desc-title">请选择性别</text>
		<radio-group class="radios">
			<radio style="padding: 20rpx;" checked="true">男</radio>
			<radio style="padding: 20rpx;">女</radio>
		</radio-group>
		
		<text class="desc-title">请选择上装</text>
		<view class="division-line"></view>
		<view class="picker-container">
			<view class="uni-list">
				<view class="uni-list-cell">
					<view class="uni-list-cell-db">
						<picker @change="upperChange" :value="upperIndex" :range="upperData">
							<view class="uni-input">{{upperData[upperIndex]}}</view>
						</picker>
					</view>
				</view>
			</view>
		</view>
		<view class="division-line"></view>
		<text class="desc-title">请选择下装</text>
		<view class="division-line"></view>
		<view class="picker-container">
			<view class="uni-list">
				<view class="uni-list-cell">
					<view class="uni-list-cell-db">
						<picker @change="lowerChange" :value="lowerIndex" :range="lowerData">
							<view class="uni-input">{{lowerData[lowerIndex]}}</view>
						</picker>
					</view>
				</view>
			</view>
		</view>
		<view class="division-line"></view>
		
		<navigator url="/pages/mainPage/mainPage" hover-class="navigator-hover">
			<button type="default" class="next-button">下一步</button>
		</navigator>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				upperData: ["T恤", "卫衣", "衬衫", "懒得", "想", "别的", "上装", "了"],
				lowerData: ["牛仔裤", "运动裤", "短裙"],
				upperIndex: 0,
				lowerIndex: 0
			}
		},
		methods: {
			upperChange(e) {
				this.upperIndex = e.detail.value
			},
			lowerChange(e) {
				this.lowerIndex = e.detail.value
			},
			error(e) {
				console.log(e.detail)
			}
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
	
	.desc-title {
		margin-top: 50rpx;
		text-align: center;
		font-size: 40rpx;
		font-weight: 700;
	}
	
	.radios {
		align-self: center;
		justify-items: center;
	}
	
	.division-line {
		margin-top: 20rpx;
		margin-bottom: 20rpx;
		margin-left: 25rpx;
		margin-right: 25rpx;
	    height: 1px;
	    content: '';
	    -webkit-transform: scaleY(.5);
	    transform: scaleY(.5);
	    background-color: #666666;
	}
	
	.picker-container {
		font-size: 40rpx;
		align-self: center;
		text-align: center;
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