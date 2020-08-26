<template>
	<view class="body">
		<view class="page-header text-center input-group">			
			<input class="search-input text-left" v-model="search_text" placeholder="搜点什么吧" type="text"/>
			<button  @click="search" class="search-button">
				<text class="iconfont icon-search"></text>
			</button>
		</view>
		<br>
		<swiper-bar :imgList="swiperList" class="novelItem"  @click="toNovel('8704', '补天者')"></swiper-bar>
		<br>
		<text v-if="novels == null">加载中</text>
		<view class="container">
			<view class="row">
				<template v-for="novel in novels">
					<view class="col-6" @click="toNovel(novel.id, novel.name)">
						<view class="novel-item" :style="{'background-image': 'url(\'/static/imgs/' + parseInt(Math.random()*30) + '.jpg\')'}">
							<text class="name">{{novel.name}}</text>
							<text class="author">
								<text class="iconfont icon-author"></text>
								{{novel.author}}
							</text>
							<text class="cn">
								<text class="iconfont icon-static"></text>
								{{novel.chapterNumbers}}
							</text>
						</view>
					</view>
				</template>
			</view>
		</view>
	</view>
</template>

<script>
	import swiperBar from "@/components/lps-swiper/lps-swiper.vue"
	export default {
		components:{
			swiperBar
		},
		data() {
			return {
				title: 'Hello',
				search_text: "",
				novels:null,
				data: [1,2,3,4,5,6,7,78,9],
				swiperList:[]
			}
		},
		onLoad() {
			this.refresh()
		},
		methods: {
			search: function(){
				console.log(this.search_text)
			},
			toNovel: function(id, name){
				uni.navigateTo({
					url: "novel?id=" + id + "&name=" + encodeURIComponent(name),
				})
			},
			refresh(){
				this.novels = null;
				let self = this;
				self.swiperList = []
				uni.request({
					url: getApp().globalData.doamin+"/getNovelList/",
					success: (res) => {
						self.novels = res.data.data;
						// 随机开始节点
						var start = parseInt(Math.random()*100)
						// 设置5个轮播项目
						for (let i = start; i < start+5; i++){
							self.swiperList.push({
								href: '/static/imgs/' + parseInt(Math.random()*25) + '.jpg',
								novel:self.novels[i]
							})
						}
						uni.showToast({
							title: "下拉可刷新",
							icon: "none"
						})
						setTimeout(uni.stopPullDownRefresh, 200)
					},
					setTimeout: 5000,
					fail: (res) => {
						uni.showToast({
							title: "加载失败，请检查网络",
							duration: 3000,
							icon: "none",
							success: () => {
								uni.stopPullDownRefresh()
							}
						})
					}
				})
			},
		},
		onPullDownRefresh(){
			this.refresh()
		}
	}
</script>

<style>
	@import url("css/index.css");
	@import url("css/iconfont.css");
</style>
