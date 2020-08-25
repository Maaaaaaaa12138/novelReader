<template>
	<view>
		<view class="list">
			<view class="list-group">
				<template v-for="chapter in chapters">
					<view class="list-group-item" :id="chapter.id" @click="gotoChapter">
						{{chapter.title}}
					</view>
				</template>
			</view>
		</view>
		<h1>{{title}}</h1>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				id: "",
				name: "",
				title: "",
				chapters: []
			}
		},
		onLoad: function(option){
			uni.setNavigationBarTitle({
				title: option.name
			})
			let self = this;
			uni.request({
				url:getApp().globalData.doamin+"/getChapterList/"+option.id,
				success: (res) => {
					self.chapters = res.data.data;
				}
			})
		},
		methods: {
			gotoChapter: function(event){
				let id = event.target.id;
				uni.navigateTo({
					url: "chapter?id="+id,
				})
			}
		}
	}
</script>

<style>

</style>
