<template>
	<view>
		<view class="index-list animated fadeInLeft fast">
			<view class="index-list1 u-f-a-c">
				<view class="u-f-a-c">
					<image :src="item.userpic" mode="widthFix" lazy-load></image>
					{{item.username}}
				</view>
				<view class="u-f-a-c" v-if="!isguanzhu" @tap="guanzhu">
					<view class="icon iconfont icon-zengjia"></view>关注
				</view>
				<view class="u-f-a-c" v-if="isguanzhu" @tap="guanzhu">
					已关注
				</view>
			</view>
			<view class="index-list2" @tap="opendetail">
				{{item.title}}
			</view>
			<view class="index-list3 u-f-j-c" @tap="opendetail">
				<!-- 图片 -->
				<image :src="item.titlepic" mode="widthFix" lazy-load></image>
				<template v-if="item.type =='video'">
					<!-- 视频 -->
					<!-- 播放按钮 -->
					<view class="icon iconfont icon-bofang index-list3-play u-f-j-c"></view>
					<!-- 播放量 -->
					<view class="index-list3-play-info">
						{{item.playcount}} {{item.long}}
					</view>
				</template>
			</view>
			<view class="index-list4 u-f-a-c">
				<view class="u-f-a-c">
		<view class="u-f-a-c"  @tap="caozuo('ding')">
			<view class="icon iconfont icon-icon_xiaolian-mian " :class="{'active':infonum.index==1}"></view>
			<view>{{infonum.ding}}</view>
		</view>	
				<view class="u-f-a-c" @tap="caozuo('cai')">
					<view class="icon iconfont icon-kulian" :class="{'active':infonum.index==2}"></view>
						<view>{{infonum.cai}}</view>
					</view>
				</view>
				<view class="u-f-a-c">
					<view class="icon iconfont icon-pinglun1 u-f-a-c"></view>
					<view class="u-f-a-c">{{item.comment}}</view>
					<view class="icon iconfont icon-zhuanfa u-f-a-c"></view>
					<view class="u-f-a-c">{{item.share}}</view>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		props:{
			item:Object,
			index:Number
		},
		data() {
			return {
				isguanzhu: this.item.isguanzhu,
				infonum: this.item.infonum,
			}
		},
		methods:{
			//关注的处理
			guanzhu(){
				  
					if(!this.isguanzhu){
						uni.showToast({
							title:'关注成功',
						});
					}else{
						uni.showToast({
							title:'取消关注成功',
						});
					}
			this.isguanzhu= !this.isguanzhu;	
			},
			//顶踩
						caozuo(type){
							switch (type){
								case "ding":
								if(this.infonum.index==1){ return; }
								this.infonum.ding++;
								if(this.infonum.index==2){
									this.infonum.cai--;
								}
								this.infonum.index=1;
									break;
								case "cai":
								if(this.infonum.index==2){ return; }
								this.infonum.cai++;
								if(this.infonum.index==1){
									this.infonum.ding--;
								}
								this.infonum.index=2;
									break;
							}
							
			},
			//进入详情页
				opendetail(){
			uni.showModal({
				content: '进入详情页',
				showCancel: false
			});
				}
		},
	
		
	}
</script>

<style scoped>
.index-list{
		padding: 20upx;
		border-bottom: 1upx solid #F0F0F0;
	}
	.index-list1{
		justify-content: space-between;
	}
	.index-list1>view:first-child{
		color: #989898;
	}
	.index-list1>view:first-child image{
		width: 80upx;
		height: 80upx;
		border-radius: 100%;
		margin-right: 10upx;
	}
	.index-list1>view:last-child{
		background: #F4F4F4;
		border-radius: 5upx;
		padding: 0 10upx;
	}
	.index-list2{
		padding-top: 15upx;
		font-size: 32upx;
	}
	.index-list3{
		position: relative;
		padding: 15upx 0;
	}
	.index-list3-play{
		position: absolute;
		color: #FFFFFF;
		font-size: 100upx;
	}
	.index-list3-play-info{
		position: absolute;
		color: #FCFDFC;
		background: rgb(78,86,57);
		bottom: 28upx;
		right: 28upx;
		border-radius: 40upx;
		font-size: 22upx;
		padding: 0 15upx;
	}
	.index-list3>image{
		width: 100%;
		border-radius: 20upx;
	}
	.index-list4{
		justify-content: space-between;
		padding: 15upx 0;
	}
	.index-list4>view>view{
		color: #D5D5D5;
		margin-right: 10upx;
	}
	.index-list4>view>view view{
		margin-right: 10upx;
	}
	.index-list4 .active,.index-list4 .active>view{
		color: #FEE42A;
	}

</style>
