<template>
	<view class="body">
		<view class="page-header text-center input-group">			
			<input class="search-input text-left" v-model="search_text" placeholder="搜点什么吧" type="text"/>
			<button  @click="search" class="search-button btn btn-primary">搜索</button>
		</view>
		<br>
		<text v-if="novels == null">加载中</text>
		<view class="container">
			<view class="row">
				<template v-for="novel in novels">
					<view class="col-6" @click="toNovel(novel.id, novel.name)">
						<view class="novel-item" :style="{'background-image': 'url(\'/static/imgs/' + parseInt(Math.random()*30) + '.jpg\')'}">
							<text class="name" >{{novel.name}}</text>
							<text class="info">{{novel.author}}   {{novel.chapterNumbers}}</text>
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
			toNovel: function(id, name){
				uni.navigateTo({
					url: "novel?id=" + id + "&name=" + encodeURIComponent(name),
				})
			},
		}
	}
</script>

<style>
	.body{
		background-color: #f2f5fa;
	}
	.page-header{
		display: flex;
	}
	.search-input{
		border-top-left-radius: 32rpx !important;
		border-bottom-left-radius: 32rpx !important;
		border-top-right-radius: 32rpx !important;
		border-bottom-right-radius: 32rpx !important;
		border: 1px dashed rgba(0,0,0,.5);
		height: 2rem;
		flex: 70%
	}
	.search-button{
		border-top-left-radius: 50rpx !important;
		border-bottom-left-radius: 50rpx !important;
		border-top-right-radius: 50rpx !important;
		border-bottom-right-radius: 50rpx !important;
		border: 0rpx;
		height: 2rem;
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
		padding: 15rpx;
	}
	.card-header{
		padding-right: 15rpx;
		white-space: nowrap;
		overflow-x: hidden;
		text-overflow: ellipsis;
	}
	.novel-item{
		display: flex;
		flex-wrap: wrap;
		position: relative;
		width: auto;
		height: 230rpx;
		background-image: url("../../static/imgs/1.jpg");
		background-position: center center; 
		background-size: cover;
		background-repeat: no-repeat;
		padding: 15rpx;
		border-radius: 15rpx;
		color: #fff;
		box-shadow: 2rpx 2rpx 6rpx rgba(0,0,0,.2), -2rpx -2rpx 6rpx rgba(0,0,0,.2);
	}
	.novel-item::before{
		content: "";
		position: absolute;
		top:0;
		left: 0;
		height: 100%;
		width: 100%;
		border-radius: 15rpx;
		background-color: rgba(0,0,0,.4);
	}
	.name{
		text-align: center;
		height: 4rem;
		text-overflow: ellipsis;
		width: 100%;
		overflow-y: hidden;
		z-index: 1;
	}
	.info{
		white-space: pre;
		text-overflow: ellipsis;
		overflow-x: hidden;
		z-index: 1;
	}
</style>
