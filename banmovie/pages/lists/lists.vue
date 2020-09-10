<template>
	<scroll-view scroll-y="true">
		<!-- 顶部固定 -->
		<view class="disBox" :style="{height:top + hei + 'px'}">
			<text @click="backbtn" style="font-size: 20px; position: absolute;bottom: 2px;" decode> ⬅ </text>
		</view>
		<view class="contant" :style="{marginTop:top + hei + 10 + 'px'}">
			<view class="toptxt">
				<text>{{ title }}</text>
			</view>
			<!-- 电影列表 -->


			<view class="listbox" v-for="(item,index) in dataList" :key="index" @click="getmove(item.id)">
				<image class="listimage" :src="item.images.large"></image>
				<view class="rigbox">
					<view class="topbox">
						<text style="font-size: 20px;font-weight: bold;">{{ item.title }}</text>
						<text style="color: #DD524D;font-size: 18px;"> {{ item.rating.average }} </text>
					</view>
					<text style="color: #C0C0C0;margin-right: 8px;" v-for=" val in item.casts " :key="val.name">主演:{{ val.name }}</text>
					<view>
						<text style="color: #C0C0C0;">导演:{{ item.directors[0].name }}</text>
					</view>
				</view>
			</view>
		</view>
	</scroll-view>
</template>

<script>
	export default {
		data() {
			return {
				title: "",
				top: 0,
				hei: 0,
				dataList: []
			}
		},
		onLoad(obj) {
			// 传过来的值
			this.title = obj.name;
			// 顶部距离
			let lisobj = uni.getMenuButtonBoundingClientRect()
			this.top = lisobj.top
			this.hei = lisobj.height
			// 发送请求
			switch (this.title) {
				case "top100":
					uni.request({
						url: "http://t.yushu.im/v2/movie/top250",
						data: {
							apikey: "0df993c66c0c636e29ecbb5344252a4a",
							start: 0,
							count: 3
						},
						success: (res) => {
							this.dataList = res.data.subjects

						}
					})
					break;
				case "正在热映":
					uni.request({
						url: "http://t.yushu.im/v2/movie/in_theaters",
						data: {},
						success: (res) => {
							this.dataList = res.data.subjects
							console.log(res);
						}
					})
					break;
				case "即将上映":
					uni.request({
						url: "http://t.yushu.im/v2/movie/coming_soon",
						data: {
							apikey: "0df993c66c0c636e29ecbb5344252a4a"
						},
						success: (res) => {

							this.dataList = res.data.subjects
						}
					})
					break;
			}

		},
		methods: {
			backbtn(){
				uni.navigateBack({
					delta: 1
				})
			}
			getmove(id){
				uni.navigateTo({
					url:`../lists/lists?name=${id}`
				})
			}
		}
	}
</script>

<style>
	.disBox {
		width: 100%;
		background-color: #c0c0c0;
		position: fixed;
		top: 0;
	}

	.contant {
		width: 96%;
		margin: 0 auto;
		height: 100%;
	}

	.toptxt {
		font-size: 24px;
		font-weight: bold;
		color: #C0C0C0;
	}

	.listbox {
		padding: 10px;
		display: flex;
	}

	 .listimage {
		width: 120px;
		height: 140px;
	}

	.rigbox {
		width: 100%;
		padding: 0 10px;
	}

	.topbox {
		display: flex;
		justify-content: space-between;
		align-items: center;
	}
</style>
