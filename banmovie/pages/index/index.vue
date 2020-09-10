<template>
	<view class="content">
		<!-- 顶部搜索栏 -->
		<view class="scerch" :style="{marginTop:top + 'px',height: hei + 2 + 'px'}">
			<text class="txt_top" :style="{lineHeight: hei + 'px'}">豆瓣</text>
			<view>
				<!-- <icon :type="search" size="22" /> -->
				<input placeholder="搜索" class="inpi" type="text" :style="{height: hei + 2 + 'px'}" />
			</view>
		</view>
		<!-- 主要内容 -->
		<view class="">
			<!-- 轮播图 -->
			<view class="uni-padding-wrap">
				<view class="page-section swiper">
					<view class="page-section-spacing">
						<swiper class="swiper" :indicator-dots="indicatorDots" :autoplay="autoplay" :interval="interval" :duration="duration">
							<swiper-item v-for="data in background" :key="data">
								<image :src=" data " style="width: 100%;height: 100%;"></image>
							</swiper-item>

						</swiper>
					</view>
				</view>
			</view>
			<!-- 主要内容 -->
			<view>
				<text class="txt_db">豆瓣电影</text>
			</view>
			<view v-for="item in conlist" :key="item.id" class="contant" @click="cliBtn(item.name)">
				<text> {{ item.name }} </text>
				<text> > </text>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				background: [
					'http://liangcang-material.alicdn.com/prod/upload/a40129d2a64d48a9800941e8196c8794.jpg?x-oss-process=image/resize,w_490/crop,x_0,y_0,w_490,h_276',
					'http://liangcang-material.alicdn.com/prod/upload/2f38dbef110b4b91a55b88213dbaec2e.jpg?x-oss-process=image/resize,w_290/interlace,1/quality,Q_80/sharpen,100',
					'https://vthumb.ykimg.com/054101015F4878BF04CD82AD28CCA819'
				],
				autoplay: true,
				interval: 2000,
				duration: 600,
				top: 0, //顶部距离
				hei: 0, //高度
				conlist: [{
					id: 0,
					name: "正在热映"
				}, {
					id: 1,
					name: "即将上映"
				}, {
					id: 2,
					name: "top100"
				}]
			}
		},
		onLoad() {
			let obj = uni.getMenuButtonBoundingClientRect()
			this.top = obj.top
			this.hei = obj.height
		},
		methods: {
			cliBtn( name ) {
				uni.navigateTo({
					url:`../lists/lists?name=${name}`
				})
			}
		}
	}
</script>

<style>
	.scerch {
		width: 96%;
		display: flex;
		justify-content: flex-start;
		width: 100%;
		margin-bottom: 10px;
	}

	.inpi {
		padding-left: 30px;
		background-color: #f7f7f7;
		border-radius: 20px;
	}

	.txt_top {
		margin: 0 6px;
		font-size: 20px;
		color: #06B806;
	}

	.txt_db {
		font-size: 24px;
		color: #555;
		margin: 16px 20px 0;
	}

	.contant {
		height: 40px;
		display: flex;
		justify-content: space-between;
		padding: 10px;
		margin: 10px;
		align-items: center;
		background: linear-gradient(to right bottom, rgba(114, 94, 67, 0.9), rgba(76, 62, 45, 0.9));
		color: #fff;
		border-radius: 3px;
		box-shadow: 0px 0px 3px #808080;
	}
</style>
