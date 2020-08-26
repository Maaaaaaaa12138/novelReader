<template>
	<view class="container">
		<view class="tools">
			<template v-for="tool in tools">
				<view @click="toTool(tool.url)" class="tool" :style="{'background-image': 'url(\'/static/toolImgs/' + tool.url + '.jpg\')'}">
					<text class="tool-text">{{tool.name}}</text>
				</view>
			</template>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				tools:[
					{
						url: "timeCalc",
						name: "相差时间计算器"
					},
					{
						url: "qrcode",
						name: "二维码生成"
					},
					{
						url: "music",
						name: "音乐播放器"
					},
					{
						url: "translate",
						name: "翻译"
					}
				]
			}
		},
		methods: {
			toTool(url){
				uni.navigateTo({
					url: url,
					animationType: "zoom-out",
					animationDuration: 300
				})
			}
		}
	}
</script>

<style>
	@import url("css/timeCalc.css");
</style>
