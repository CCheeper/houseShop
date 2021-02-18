<template>
	<view>
		<view class="uni-padding-wrap uni-common-mt">
			<view class="" v-for="(num,index) in data" :key="index" @click="_request()" style="height: 150px;">
				<view @click="tapBlock(index)">
					<image src="../../../static/60x60.png" style="margin: 14px 5px;float: left;height: 120px;width: 120px;"></image>
					<div style='display: inline-block;align=left;margin: 14px;'>
						<div style="font-size: 20px;height: 30px;">东方曼哈顿 3室2厅 西南</div>
						<div style="font-size: 17px;height: 25px;">3宝2厅|83.7m|西南东方曼</div>
						<div style="font-size: 17px;height: 25px;">利州区·万源</div>
						<div style="display: flex;">
							<div style="font-size: 25px;height: 25px;color: #EE0A24;">25万</div>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
							<div style="font-size: 15px;font-weight: 100;position:fixed; bottom:0px;right: 30px;">10000/平</div>
						</div>
					</div>
				</view>
			</view>
			<view class="uni-loadmore" v-if="showLoadMore">{{loadMoreText}}</view>
		</view>
	</view>
</template>
<script>
	export default {
		data() {
			return {
				title: '下拉刷新 + 加载更多',
				data: [],
				loadMoreText: "加载中...",
				showLoadMore: false,
				max: 0
			}
		}
		,
		onLoad() {
			this.initData();
		},
		onUnload() {
			this.max = 0,
				this.data = [],
				this.loadMoreText = "加载更多",
				this.showLoadMore = false;
		},
		onReachBottom() {
			console.log("onReachBottom");
			if (this.max > 40) {
				this.loadMoreText = "没有更多数据了!"
				return;
			}
			this.showLoadMore = true;
			setTimeout(() => {
				this.setListData();
			}, 300);
		},
		onPullDownRefresh() {
			console.log('onPullDownRefresh');
			this.initData();
		},
		methods: {
			_request() {
				// uni.request({
				// 	url: 'localhost:8080',
				// 	dataType: 'text',
				// 	data: {
				// 		noncestr: Date.now()
				// 	},
				// 	success: (res) => {
				// 		console.log('request success', res)
				// 		uni.showToast({
				// 			title: '请求成功',
				// 			icon: 'success',
				// 			mask: true,
				// 			duration: duration
				// 		});
				// 		this.res = '请求结果 : ' + JSON.stringify(res);
				// 	},
				// 	fail: (err) => {
				// 		console.log('request fail', err);
				// 		uni.showModal({
				// 			content: err.errMsg,
				// 			showCancel: false
				// 		});
				// 	},
				// 	complete: () => {
				// 		this.loading = false;
				// 	}
				// });
			},
			initData() {
				setTimeout(() => {

					this.max = 0;
					this.data = [];
					let data = [];
					this.max += 20;
					for (var i = this.max - 19; i < this.max + 1; i++) {
						data.push(i)
					}
					this.data = this.data.concat(data);
					uni.stopPullDownRefresh();
				}, 300);
			},
			setListData() {
				let data = [];
				this.max += 10;
				for (var i = this.max - 9; i < this.max + 1; i++) {
					data.push(i)
				}
				this.data = this.data.concat(data);
			},
			tapBlock(index){
				uni.navigateTo({
				    url: '/pages/houseDetail/detail?id='+index
				});
			}
		}
	}
</script>

<style>
	.text {
		margin: 16rpx 0;
		width: 100%;
		background-color: #fff;
		height: 120rpx;
		line-height: 120rpx;
		text-align: center;
		color: #555;
		border-radius: 8rpx;
	}
</style>
