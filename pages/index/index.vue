<template>
	<view>
		<!-- 滑动tab -->
		<swiper-tab :tabBars="tabBars" :tabIndex="tabIndex" @tabtap="tabtap">
		</swiper-tab>
		<view class="uni-tab-bar" >
			<swiper class="swiper-box" :style="{height:swiperheight+'px'}" :current="tabIndex" @change="tabchange">
				<!-- 图文列表 -->
				<swiper-item   v-for="(items,index) in newList" :key="index">
					<scroll-view scroll-y="true"  class="list" @scrolltolower="loadmore(index)">
							<template v-if="items.list.length>0">
								<block v-for="(item,index1) in items.list" :key="index1">
										<index-list :item="item" :index="index1"></index-list>	
									</block>
									<!-- 下拉加载更多 -->
								<load-more :loadtext="items.loadtext"></load-more>
							</template>
							<template v-else>
								 <no-thing></no-thing>
							</template>
					</scroll-view>
				</swiper-item>
			</swiper>
		</view>
	</view>	
</template>

<script>
	import indexList from '../../components/index/index-list.vue';
	import swiperTab from '../../components/index/swiper-tab.vue';
	import loadMore from '../../components/common/load-more.vue';
	import noThing from '../../components/common/no-thing.vue';
	export default {
		components:{
			indexList,
			swiperTab,
			loadMore,
			noThing
		
		},
		data() {
			return {
				swiperheight:500,
				tabIndex:0,
				tabBars: [{
				    name: '关注',
				    id: 'guanzhu'
				}, {
				    name: '推荐',
				    id: 'tuijian'
				}, {
				    name: '体育',
				    id: 'tiyu'
				}, {
				    name: '热点',
				    id: 'redian'
				}, {
				    name: '财经',
				    id: 'caijing'
				}, {
				    name: '娱乐',
				    id: 'yule'
				},
				],
				newList:[
					{	loadtext:'上拉加载更多',
						list:[
							{
								userpic:'../../static/demo/userpic/6.jpg',
								username:'星火',
								isguanzhu:true,
								title:'文章标题',
								type:'img',//话题类型 img or video
								titlepic:'../../static/demo/datapic/1.jpg',//封面图
								infonum:{
									index:1 ,//0没有操作,1顶2踩
									ding:11,
									cai:11
								},
								comment:'10',
								share:'10'
							},
							{
								userpic:'../../static/demo/userpic/6.jpg',
								username:'星火',
								isguanzhu:false,
								title:'文章标题',
								type:'video',//话题类型 img or video
								playcount:'10w',
								long:'2:47',
								titlepic:'../../static/demo/datapic/1.jpg',//封面图
								infonum:{
									index:2,//0没有操作,1顶2踩
									ding:11,
									cai:11
								},
								comment:'10',
								share:'10'
							}
						],
						
					},
					{
						loadtext:'上拉加载更多',
						list:[
							{
								userpic:'../../static/demo/userpic/6.jpg',
								username:'星火1',
								isguanzhu:true,
								title:'文章标题',
								type:'img',//话题类型 img or video
								titlepic:'../../static/demo/datapic/1.jpg',//封面图
								infonum:{
									index:1 ,//0没有操作,1顶2踩
									ding:11,
									cai:11
								},
								comment:'10',
								share:'10'
							},
							{
								userpic:'../../static/demo/userpic/6.jpg',
								username:'星火1',
								isguanzhu:false,
								title:'文章标题',
								type:'video',//话题类型 img or video
								playcount:'10w',
								long:'2:47',
								titlepic:'../../static/demo/datapic/1.jpg',//封面图
								infonum:{
									index:2,//0没有操作,1顶2踩
									ding:11,
									cai:11
								},
								comment:'10',
								share:'10'
							}
						],
						
					},
					{
						loadtext:'上拉加载更多',
						list:[
						
						],	
					},
					{
						loadtext:'上拉加载更多',
						list:[
						
						],	
					},
					{
						loadtext:'上拉加载更多',
						list:[
						
						],	
					},
					
				],
				
			}
		},
		
		onLoad() {
			uni.getSystemInfo({
				success:(res)=>{
					let height = res.windowHeight-uni.upx2px(100)
					this.swiperheight = height;
				}
			})
		},
		//监听导航搜索
		onNavigationBarSearchInputClicked(e){
			uni.navigateTo({
				url:"../search/search",
			})
		},
	//监听原生标题栏搜索按钮点击事件
		onNavigationBarButtonTap(e){
			switch (e.index){
				case 1:
				//打开发布页面
				uni.navigateTo({
					url:'../add-input/add-input',
				})
					break;
				
			}
			
		},
		methods: {
			// 点击tab切换
			tabtap(index){
				this.tabIndex = index;
			},
			//滑动切换
			tabchange(e){
				this.tabIndex = e.detail.current;
			},
			//上拉加载更多
			loadmore(index){
				if(this.newList[index].loadtext !='上拉加载更多'){ return; }
				this.newList[index].loadtext = '加载中';
				setTimeout(()=>{
					let obj ={
						userpic:'../../static/demo/userpic/6.jpg',
						username:'星火x',
						isguanzhu:true,
						title:'文章标题',
						type:'img',//话题类型 img or video
						titlepic:'../../static/demo/datapic/1.jpg',//封面图
						infonum:{
							index:1 ,//0没有操作,1顶2踩
							ding:11,
							cai:11
						},
						comment:'10',
						share:'10',
						
					}
					this.newList[index].list.push(obj);
					this.newList[index].loadtext = '上拉加载更多';
				},2000)
			}
		}
	}
</script>

<style>

</style>
