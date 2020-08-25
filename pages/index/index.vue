<template>
	<view>
		<view class="page-header text-center input-group">			
			<input class="form-control search-input text-left" v-model="search_text" placeholder="搜点什么吧" type="text"/>
			<button @click="search" class="form-control search-button btn btn-primary">搜索</button>
		</view>
		<br>
		<text v-if="novels == null">加载中</text>
		<view class="container">
			<view class="row">
				<template v-for="novel in novels">
					<view class="col-6">
						<view class="card">
							<view class="card-header text-center" :id="novel.id" :data-name="novel.name" @click="toNovel">{{novel.name}}</view>
							<view class="card-body">
								<view >作者：{{novel.author}}</view>
								<view>章节数量：{{novel.chapterNumbers}}</view>
							</view>
						</view>
					</view>
				</template>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				title: 'Hello',
				search_text: "",
				novels:null,
				data: [1,2,3,4,5,6,7,78,9]
			}
		},
		onLoad() {
			let self = this;
			uni.request({
				url: getApp().globalData.doamin+"/getNovelList/",
				success: (res) => {
					self.novels = res.data.data;
				}
			})
		},
		methods: {
			search: function(){
				console.log(this.search_text)
			},
			toNovel: function(event){
				let id = event.target.id;
				let name = event.target.dataset.name;
				uni.navigateTo({
					url: "novel?id=" + id + "&name=" + encodeURIComponent(name),
				})
			},
		}
	}
</script>

<style>
	.search-input{
		border-top-left-radius: 32rpx !important;
		border-bottom-left-radius: 32rpx !important;
		border-top-right-radius: 32rpx !important;
		border-bottom-right-radius: 32rpx !important;
		width: 70%;
	}
	.search-button{
		border-top-left-radius: 50rpx !important;
		border-bottom-left-radius: 50rpx !important;
		border-top-right-radius: 50rpx !important;
		border-bottom-right-radius: 50rpx !important;
		border: 0rpx;
	}
	.search-button::after{
		border: 0;
	}
	.page-header{
		padding-left: 10%;
		padding-right: 10%;
	}
	.row{
		padding-left: 15px;
		padding-right: 15px;
	}
	.col-6{
		padding-left: 5px;
		padding-right: 5px;
	}
	.card-header{
		padding-right: 15rpx;
		white-space: nowrap;
		overflow-x: hidden;
		text-overflow: ellipsis;
	}
</style>
