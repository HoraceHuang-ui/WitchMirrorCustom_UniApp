<template>	
	<view class="content">
		<view style="height: var(--status-bar-height);"></view>
		<uni-nav-bar left-icon="back" rightText="保存" title="自定义" style="width: 100%;" shadow @clickLeft="top_bar_back"></uni-nav-bar>
		<view style="text-align: right;">
			<image class="main-pic" :src="setMainPic" mode="aspectFill"></image>
			<image @click="back_to_overview" class="back-to-overview" v-show="mainPicMode" src="../../static/back.png" mode="aspectFit"></image>
			<image @click="arm_click" class="circle-button" v-show="!mainPicMode" style="position: absolute; top: 300rpx; left: 230rpx;" src="../../static/circle-button.png"/>
			<image @click="body_click" class="circle-button" v-show="!mainPicMode" style="position: absolute; top: 290rpx; left: 350rpx;" src="../../static/circle-button.png"/>
			<image @click="leg_click" class="circle-button" v-show="!mainPicMode" style="position: absolute; top: 600rpx; left: 300rpx;" src="../../static/circle-button.png"/>
		</view>
		<view class="footer">
			<text style="position: relative;margin-bottom: 20rpx;">{{message}}</text>
			<view class="division-line" style="bottom: 550rpx;"></view>
			<template v-if="!mainPicMode">
				<scroll-view scroll-x="true" scroll-y="false" scroll-left="120">
					<button @click="texture_click" class="bottom-nav-item" :class="{'nav-button-selected': bottomNavSelection == 1}">材质</button>
					<button @click="color_click" class="bottom-nav-item" :class="{'nav-button-selected': bottomNavSelection == 2}">颜色</button>
					<button @click="layer_click" class="bottom-nav-item" :class="{'nav-button-selected': bottomNavSelection == 3}">图层</button>
					<button @click="preset_click" class="bottom-nav-item" :class="{'nav-button-selected': bottomNavSelection == 4}">预设</button>
				</scroll-view>
				<!-- texture -->
				<scroll-view scroll-y="true" v-if="bottomNavSelection == 1" class="bottom-scroller">
					<uni-grid :column="3" :highlight="true">
						<uni-grid-item v-for="texture in textures">
							<view class="grid-item-box" style="background-color: #fff;">
								<text>{{texture}}</text>
								<uni-icons type="image" :size="50" color="#777" />
							</view>
						</uni-grid-item>
					</uni-grid>
				</scroll-view>
				<!-- color -->
				<scroll-view scroll-y="true" v-if="bottomNavSelection == 2" class="bottom-scroller">
					<button @click="open_color_picker" class="full-width-button" :style="{backgroundColor: pickerColor}" :class="{foregroundWhite: !buttonForegroundBlack, foregroundBlack: buttonForegroundBlack}">当前底色：{{pickerColor}}</button>
					<wxy-color-picker ref="colorPicker" :color="color" @confirm="color_picker_confirm"></wxy-color-picker>
				</scroll-view>
				<!-- layer -->
				<scroll-view scroll-y="true" v-if="bottomNavSelection == 3" class="bottom-scroller">
					<uni-grid :column="3" :highlight="true">
						<uni-grid-item v-for="(layer, index) in layers">
							<view class="grid-item-box" style="background-color: #fff;">
								<text>{{layer}}</text>
								<uni-icons :type="index != 2 ? 'image' : 'plus'" :size="50" color="#777" />
							</view>
						</uni-grid-item>
					</uni-grid>
				</scroll-view>
				<!-- preset -->
				<scroll-view scroll-y="true" v-if="bottomNavSelection == 4" class="bottom-scroller">
					<uni-grid :column="3" :highlight="true">
						<uni-grid-item v-for="preset in presets">
							<view class="grid-item-box" style="background-color: #fff;">
								<text>{{preset}}</text>
								<uni-icons type="image" :size="50" color="#777"/>
							</view>
						</uni-grid-item>
					</uni-grid>
				</scroll-view>
			</template>
			<template v-else>
				<scroll-view scroll-x="true" scroll-y="false" scroll-left="120">
					<button @click="texture_click" class="bottom-nav-item" :class="{'nav-button-selected': bottomNavSelection == 1}">材质</button>
					<button @click="color_click" class="bottom-nav-item" :class="{'nav-button-selected': bottomNavSelection == 2}">颜色</button>
					<button @click="layer_click" class="bottom-nav-item" :class="{'nav-button-selected': bottomNavSelection == 3}">图层</button>
					<button @click="size_click" class="bottom-nav-item" :class="{'nav-button-selected': bottomNavSelection == 4}">尺寸</button>
					<button @click="detail_click" class="bottom-nav-item" :class="{'nav-button-selected': bottomNavSelection == 5}">细节</button>
				</scroll-view>
				<!-- texture -->
				<scroll-view scroll-y="true" v-if="bottomNavSelection == 1" class="bottom-scroller">
					<uni-grid :column="3" :highlight="true">
						<uni-grid-item v-for="texture in textures">
							<view class="grid-item-box" style="background-color: #fff;">
								<text>{{texture}}</text>
								<uni-icons type="image" :size="50" color="#777" />
							</view>
						</uni-grid-item>
					</uni-grid>
				</scroll-view>
				<!-- color -->
				<scroll-view scroll-y="true" v-if="bottomNavSelection == 2" class="bottom-scroller">
					<button @click="open_color_picker" class="full-width-button" :style="{backgroundColor: pickerColor}" :class="{foregroundWhite: !buttonForegroundBlack, foregroundBlack: buttonForegroundBlack}">当前底色：{{pickerColor}}</button>
					<wxy-color-picker ref="colorPicker" :color="color" @confirm="color_picker_confirm"></wxy-color-picker>
				</scroll-view>
				<!-- layer -->
				<scroll-view scroll-y="true" v-if="bottomNavSelection == 3" class="bottom-scroller">
					<uni-grid :column="3" :highlight="true">
						<uni-grid-item v-for="(layer, index) in layers">
							<view class="grid-item-box" style="background-color: #fff;">
								<text>{{layer}}</text>
								<uni-icons :type="index != 2 ? 'image' : 'plus'" :size="50" color="#777" />
							</view>
						</uni-grid-item>
					</uni-grid>
				</scroll-view>
				<!-- size -->
				<scroll-view scroll-y="true" v-if="bottomNavSelection == 4" class="bottom-scroller">
					<view class="uni-title slider-title">袖长占臂长比例 / %</view>
					<slider value="20" show-value />
				</scroll-view>
				<!-- details -->
				<scroll-view scroll-y="true" v-if="bottomNavSelection == 5" class="bottom-scroller">
					<checkbox style="position: relative; left: -250rpx;" @click="curve = !curve">袖口褶皱</checkbox>
					<button :disabled="!curve" style="margin: 25rpx;">编辑褶皱</button>
					<checkbox style="position: relative; left: -280rpx;" @click="belt = !belt">飘带</checkbox>
					<button :disabled="!belt" style="margin: 25rpx;">编辑飘带</button>
				</scroll-view>
			</template>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				pickerColor: "#aa0000",
				message: "总体",
				mainPicMode: 0,
				bottomNavSelection: 1,
				textures: ["棉", "毛衣", "丝绸", "懒得", "想", "别的", "材质", "了"],
				layers: ["图层1", "图层2", "添加图层"],
				presets: ["预设1", "预设2", "预设3", "预设4", "预设5", "预设6"],
				curve: false,
				belt: false
			}
		},
		methods: {
			top_bar_back() {
				uni.navigateTo({
					url: "/pages/mainPage/mainPage"
				})
			},
			open_color_picker() {
				this.$refs.colorPicker.open();
			},
			color_picker_confirm(e) {
				this.pickerColor = e.hex
			},
			texture_click() {
				this.bottomNavSelection = 1
			},
			color_click() {
				this.bottomNavSelection = 2
			},
			layer_click() {
				this.bottomNavSelection = 3
			},
			size_click() {
				this.bottomNavSelection = 4
			},
			detail_click() {
				this.bottomNavSelection = 5
			},
			preset_click() {
				this.bottomNavSelection = 4
			},
			arm_click() {
				this.mainPicMode = 1
				this.bottomNavSelection = 1
				this.message = "手臂"
			},
			body_click() {
				this.mainPicMode = 2
				this.bottomNavSelection = 1
				this.message = "上半身"
			},
			leg_click() {
				this.mainPicMode = 3
				this.bottomNavSelection = 1
				this.message = "腿部"
			},
			back_to_overview() {
				this.mainPicMode = 0
				this.bottomNavSelection = 1
				this.message = "总体"
			}
		},
		computed: {
			buttonForegroundBlack() {
				if (this.pickerColor > "#888888") {
					return true
				} else {
					return false
				}
			},
			setMainPic() {
				switch (this.mainPicMode) {
					case 0: return "../../static/whole-body.jpg"
					case 1: return "../../static/arm.jpg"
					case 2: return "../../static/upperFront.jpg"
					case 3: return "../../static/leg.jpg"
				}
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

	.main-pic {
		width: 800rpx;
		height: 800rpx;
		align-self: center;
	}
	
	.back-to-overview {
		width: 150rpx;
		position: relative;
		margin-top: -300rpx;
		margin-right: 30rpx;
	}
	
	.circle-button {
		width: 50rpx;
		height: 50rpx;
	}

	.text-area {
		display: flex;
		justify-content: center;
	}
	
	.footer {
		text-align: center;
		left: 0;
		right: 0;
		bottom: 0;
		position: absolute;
	}
	
	.bottom-nav-item {
		text-align: center;
		display: inline-block;
		background-color: white;
		font-size: 30rpx;
		width: 110rpx;
		margin-left: 10rpx;
		margin-right: 10rpx;
	}
	
	.grid-item-box {
		flex: 1;
		// position: relative;
		/* #ifndef APP-NVUE */
		display: flex;
		/* #endif */
		flex-direction: column;
		align-items: center;
		justify-content: center;
		padding: 15px;
	}
	
	.bottom-scroller {
		height: 450rpx;
		flex-wrap: wrap;
		margin-top: 20rpx;
	}
	
	.nav-button-selected {
		background-color: #4cb6e8;
		color: white;
	}
	
	.slider-title {
		margin-left: 30rpx;
		margin-top: 20rpx;
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
	
	.full-width-button {
		border-radius: 150rpx;
		margin-left: 30rpx;
		margin-right: 30rpx;
		margin-top: 40rpx;
		font-weight: 500rpx;
		font-size: 35rpx;
		border: none;
	}
	
	.foregroundWhite {
		color: white;
	}
	.foregroundBlack {
		color: black;
	}
	
	/* 自定义状态栏 */
	.status_bar {
	          height: var(--status-bar-height);
	          width: 100%;
	}
	 
	/* 自定义导航栏 */
	.status_title {
	    box-sizing: border-box;
	    display: flex;
	    justify-content: space-between;
	    align-items: center;
	    width: 100%;
	    height: 44px;
	    padding: 0 16px;
	    background-color: #FFFFFF;
	}
	.status_left {
	    width: 18px !important;
	}
	.status_center {
	    font-size: 17px;
	    font-weight: 700;
	}
	.status_right {
	    width: 22px;
	}
</style>
