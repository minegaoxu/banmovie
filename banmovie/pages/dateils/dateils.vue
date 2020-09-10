<template>
	<view class="big_view">
		<!-- 顶部固定 -->
		<view class="disBox" :style="{height:top + hei + 'px'}">
			<text @click="backbtn" style="font-size: 20px; position: absolute;bottom: 2px;" decode> ⬅ </text>
		</view>
		<view>

		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				moveList: [],
				top: 0,
				hei: 0,
			}.
		},
		onLoad(id) {
			// 获取顶部距离
			let lisobj = uni.getMenuButtonBoundingClientRect();
			this.top = lisobj.top;
			this.hei = lisobj.height;
			// 发送请求
			uni.request({
				url: "http://t.yushu.im/v2/movie/subject/" + id,
				data: {
					apikey: "0df993c66c0c636e29ecbb5344252a4a"
				},
				success: (res) => {
					console.log(res);
					this.moveList = res.data
				}
			});
		},
		methods: {

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
</style>
