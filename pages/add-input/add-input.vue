<template>
	<view>
		<!-- 自定义导航栏 -->
		<uni-nav-bar :statusBar="true" rightText="发布" leftText="左" leftIcon="arrowleft" @click-left="back"> 
		<view class="u-f-j-c s-title" >
		所有人可见
		<view class="icon iconfont icon-xialazhankai"></view>
		</view>
		</uni-nav-bar>
	</view>
</template>

<script>
	import uniNavBar from '../../components/uni-nav-bar/uni-nav-bar.vue';
	export default {
		components:{
			uniNavBar
		},
		data() {
			return {
				
			}
		},
		methods:{
			back(){
				console.log(123);
				uni.navigateBack({ delta: 1 });
			}
		},
	}
</script>

<style scoped>
	.s-title{
		position: absolute;
		left: 0;
		right: 0;
	}
</style>
