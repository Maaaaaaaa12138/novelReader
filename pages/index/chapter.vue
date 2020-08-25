<template>
	<view class="container">
		<view class="content">
			{{content}}
		</view>
		<br>
		<view class="row text-center" v-if="content != null">
			<view class="col-4">
				<button class="btn btn-primary" @click="privious">上一章</button>
			</view>
			<view class="col-4">
				<button class="btn btn-primary" @click="menu">目录</button>
			</view>
			<view class="col-4">
				<button class="btn btn-primary" @click="next">下一章</button>
			</view>
		</view>
		<br>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				id: "",
				title: "",
				content: null,
			}
		},
		onLoad: function(option){
			this.id = option.id;			
			this.getChapter();
		},
		methods: {
			getChapter: function(){
				let self = this;
				uni.request({
					url: getApp().globalData.doamin+"/getChapter/"+this.id,
					success: (res) => {
						uni.setNavigationBarTitle({
								title: res.data.data.title
							})
						self.content = res.data.data.content
						uni.pageScrollTo({
							duration:400,
							scrollTop:0
						})
					}
				})
			},
			menu: function(){
				uni.navigateBack()
			},
			privious: function(){
				let self = this;
				uni.request({
					url: getApp().globalData.doamin + "/previous/" + this.id,
					success: (res) => {
						if (res.data.mes){
							uni.showToast({
								icon: "none",
								title: res.data.mes,
							})
						}
						else{
							self.id = res.data.data;
							self.getChapter();
						}
					}
				})
			},
			next: function(){
				let self = this;
				uni.request({
					url: getApp().globalData.doamin + "/next/" + this.id,
					success: (res) => {
						if (res.data.mes){
							uni.showToast({
								icon: "none",
								title: res.data.mes
							})
						}
						else{
							self.id = res.data.data;
							self.getChapter();
						}
					}
				})
			}
		}
	}
</script>

<style>
	.content{
		white-space:pre-wrap;
		font-size: smaller;
	}
</style>
