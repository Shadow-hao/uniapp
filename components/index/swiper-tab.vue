<template>
		<view class="uni-tab-bar">
			<scroll-view scroll-x="true" class="uni-swiper-tab" >
				<block v-for="(tab,index) in tabBars" :key="tab.id">
					<view class="swiper-tab-list" 
					:class="{'active':tabIndex == index}"
					@tap="tabTap(index)">
					{{tab.name}}
					<view class="swiper-tab-line"></view>
					</view>
				</block>
			</scroll-view>
		</view>
		
</template>

<script>
	export default {
		props:{
			tabBars:Array,
			tabIndex:Number
		},
		methods:{
			tabTap(index){
				this.$emit('tabtap',index);
			},
		}
	}
</script>

<style scoped>
	.uni-swiper-tab{
		border-bottom: 1px solid #EEEEEE;
	}
	.swiper-tab-list{
		color: #969696;
		font-weight: bold;
	}
	.uni-swiper-tab .active{
		color: #343434;
	}
	.active .swiper-tab-line{
		border-bottom: 5upx solid #FEDE33;
		width: 70upx;
		margin: auto;
		border-top: 5upx solid #FEDE33;
		border-radius: 20upx;
	}
</style>
