<script setup>
	import { ref } from "vue"
	// tab 选项卡列表
	const tabbarList = ref(["Tab1", "Tab2", "Tab3", "Tab4", "Tab5", "Tab6", "Tab7", "无产阶级"])

	// 滑块视图容器，当前所在滑块的 index
	const activeIndex = ref(0)

	// 可滚动视图区域里的 tab 选项卡点击事件
	const changeTabbar = (index) => {
		activeIndex.value = index
	}

	// 滑块视图容器，当前所在滑块的 index 改变事件
	const swiperChange = (e) => {
		activeIndex.value = e.detail.current
	}

	// 返回一个在该范围内的随机整数
	const randomInt = (min, max) => Math.floor(Math.random() * (max - min + 1) + min)
</script>

<template>
	<view class="wrap">
		<!-- tab 选项卡列表 -->
		<view class="tabbar">
			<scroll-view class="tabbar-scroll" :scroll-left="activeIndex * 4 * 16" scroll-x :scroll-with-animation="true">
				<view class="tabbar-item" v-for="(item, index) in tabbarList" :key="index" :class="{ active: activeIndex === index }" @tap="changeTabbar(index)">
					<text class="tabbar-item-word">{{ item }}</text>
				</view>
			</scroll-view>
		</view>

		<!-- 可滚动视图区域 长列表 -->
		<swiper class="swiper" :current="activeIndex" @change="swiperChange" :duration="300" :circular="true">
			<swiper-item v-for="(item, index) in tabbarList" :key="index">
				<scroll-view style="background: #ff000021" class="swiper-scroll" scroll-y>
					<view class="list-item" v-for="n in randomInt(3, 60)" :key="n">
						<text
							>{{ item }} -
							{{ n }}
							【这里填写自己的长列表子项】洪都拉斯驻华使馆在北京举行开馆仪式。秦刚代表中国政府致以热烈祝贺：自中洪建交以来，双方坚定履行建交承诺，推动双边关系强劲起步</text
						>
					</view>
				</scroll-view>
			</swiper-item>
		</swiper>
	</view>
</template>

<style scoped lang="scss">
	/* #ifdef H5||APP */
	body {
		overflow: hidden;
	}
	/* #endif */

	.wrap {
		.tabbar {
			// position: sticky;
			// top: 0;
			height: 80rpx;

			background-color: #fff;
			box-sizing: border-box;
			z-index: 999;

			.tabbar-scroll {
				white-space: nowrap;
				// 谷歌隐藏滚动条
				::-webkit-scrollbar {
					display: none;
				}
				// Firefox 隐藏滚动条
				overflow: -moz-scrollbars-none;
				// IE11 隐藏滚动条
				-ms-overflow-style: none;

				.tabbar-item {
					display: inline-block;
					height: 80rpx;
					padding: 0 20rpx;
					line-height: 80rpx;
					text-align: center;
					font-size: 30rpx;
					color: #999;
					transition: all 0.3s;

					.tabbar-item-word {
						padding: 0 10rpx 4rpx;
						border-bottom: 4rpx solid transparent;
						white-space: nowrap;
						box-sizing: border-box;
						transition: all 0.3s;
					}

					&.active {
						color: #07c160;

						.tabbar-item-word {
							padding-bottom: 4rpx;
							border-bottom-color: #07c160;
						}
					}
				}
			}
		}
		.swiper {
			height: calc(100vh - 80rpx);

			.swiper-scroll {
				height: calc(100vh - 80rpx);
				overflow-y: scroll;
				// 谷歌隐藏滚动条
				::-webkit-scrollbar {
					display: none;
				}
				// Firefox 隐藏滚动条
				overflow: -moz-scrollbars-none;
				// IE11 隐藏滚动条
				-ms-overflow-style: none;

				.list-item {
					// border-bottom: 1rpx solid #eee;
				}
			}
		}
	}
</style>
