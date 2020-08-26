<template>
	<view class="my-plan-style">
		<!-- 3D轮播 -->
		<view class="">
			<swiper class="imageContainer" @change="handleChange" previous-margin="50rpx" next-margin="50rpx" circular  autoplay>
				<block v-for="(item,index) in imgList" :key="index">
					<swiper-item class="swiperitem">
						<image class="itemImg" @click="toNovel(item.novel.id, item.novel.name)" :class="currentIndex == index ? 'swiperactive': ''" :src="item.href" lazy-load mode="scaleToFill"></image>
					</swiper-item>
				</block>
			</swiper>
			<view class="pointbox" v-if="isPoint">
				<block v-for="(item,index) in imgList" :key="index">
					<view class="point" :class="currentIndex == index ? 'pointactive': ''"></view>
				</block>
			</view>
		</view>
	</view>
</template>
<script>
	export default {
		name: 'swiper-bar',
		props: { 
		  /**
		   * 固定到页面顶部
		   */
		  imgList: {
		    type: Array,
		    default: ()=>[]
				
		  },
		  isPoint: {
		    type: Boolean,
		    default: false		
		  },
		},
		data() {
			return {
				currentIndex:0
			};
		},
		computed: {
	
		},
		methods: {
			 handleChange(e){
				 this.currentIndex = e.detail.current;
			 },
			 toNovel(id, name){
			 	uni.navigateTo({
			 		url: "../../pages/index/novel?id=" + id + "&name=" + encodeURIComponent(name),
			 	})
			 }
		}
	}	
</script>
<style lang="scss">
	
	.pointbox{
		height: 40upx;
		line-height: 40upx;
		margin-top: 19upx;
		display: flex;
		flex-direction: row;
		justify-content: center;
	}
	.point{
		width: 8px;
		height: 8px;
		background: #FBB717;
		border-radius: 50%;
		margin-left: 20upx;
		align-self: center;
	}
	.pointactive{
		width:40upx;
		height:16upx;
		background:#FBB717;
		border-radius: 12upx;
		align-self: center;

	}
	// 3D轮播样式
	.imageContainer {
		width: 100%;
		/* height: 500rpx; */
		/* background: #000; */
		height: 300upx;
	}
	
	.swiperitem {
		/* height: 500rpx; */
		height: 255upx;
		padding: 0upx 20upx;
		box-sizing: border-box;
		position: relative;
		.swiperText {
			display: flex;
			flex-direction: column;
			align-items: center;
			position: absolute;
			top: 56upx;
			left: 51upx;
			z-index: 998;
			width:162upx;
			height:163upx;
			background:rgba(255,255,255,1);
			border-radius:8upx;
			padding:10upx;
			.name {
				font-size:26upx;
				font-weight:500;
				color:rgba(253,57,91,1);
				line-height:37upx;
				margin-bottom: 10upx;
			}
			.zq,.cz {
				font-size:20upx;
				color:rgba(253,57,91,1);
				line-height:35upx;
			}
			.addNl {
				width:120upx;
				height:26upx;
				background:rgba(253,57,91,1);
				border-radius:13upx;
				font-size:20upx;
				font-weight:500;
				color:rgba(255,255,255,1);
				text-align: center;
				line-height: 26upx;
				margin-top: 10upx;
			}
			
		}
	}
	
	.itemImg {
		position: absolute;
		width: 95%;
		/* height: 380rpx; */
		height: 255upx;
		border-radius: 15rpx;
		z-index: 5;
		opacity: 0.7;
		top: 5%; 
		box-shadow:0px 4upx 15upx 0px rgba(153,153,153,0.24);
	}
	
	.swiperactive {
		width: 95%;
		opacity: 1;
		z-index: 10;
		//height: 430rpx; 
		height: 300upx;
		top: 0%;
		transition: all .2s ease-in 0s;
	}
	
	.zhankai{
		text-align: center;
		.iconfont{
			margin-left: 10upx;
		}
	}
</style>