<template>
	<view>
		<view :fixed="true">			
		<!-- 滑块 -->
		<swiper-tab-head 
		:tabBar="tabBar" 
		:tabIndex="tabIndex" 
		@tabtap="tabtap"	
		>
		</swiper-tab-head>
		</view>
		<!-- 滑动切换 -->
		<view class="uni-tab-bar">
			<swiper class="swiper-box" 
			:style="{ height: swiperHeight + 'px' }" 
			:current="tabIndex" 
			@change="tabChange">
				<swiper-item v-for="(items, index) in newList" :key="index">
					
					<scroll-view scroll-y="true" class="list" 
					@scrolltolower="loadmore(index)">
					<!-- 下拉到底部加载。。。 -->
					<template v-if="items.list.length>0">
						<!-- 图文列表 -->
						<block v-for="(item, index1) in items.list" :key="index1">
							<indexList :item="item" :index="index1"></indexList>
							<!-- 通过v-bind绑定将数据向下传递 -->
						</block>
						<!-- 下拉加载-->
						<load-more :loadtext="items.loadtext"></load-more>
					</template>
					<!-- 无内容显示 -->
					<template v-else>
						<nothing></nothing>
					</template>					
					</scroll-view>
				</swiper-item>
			</swiper>
		</view>
	</view>
</template>

<script>
//引入组件
import indexList from '../../components/index/index-list.vue';
import swiperTabHead from '../../components/index/swiper-tab-head.vue';

import loadMore from '../../components/common/load-more.vue';//下拉加载组件
import nothing from '../../components/common/nothing.vue';//无内容组件


export default {
	components: {
		//注册组件
		indexList,
		swiperTabHead,
		loadMore,
		nothing
	},
	data() {
		return {
			swiperHeight:500,
			tabIndex: 0,
			tabBar: [
				{ name: '关注', id: 'guanzhu' },
				{ name: '推荐', id: 'tuijian' },
				{ name: '体育', id: 'tiyu' },
				{ name: '热点', id: 'redian' },
				{ name: '财经', id: 'caijing' },
				{ name: '娱乐', id: 'yule' }
			],
			newList: [
				{
					loadtext:"上拉加载更多...",
					list: [
						{
							userpic: '../../static/demo/userpic/11.jpg',
							username: '王五',
							isguanzhu: false,
							title: '标题',
							type: 'video', //img:图文 video:视频
							titlepic: '../../static/demo/datapic/17.jpg',
							playnum: 200000,
							long: '2:22',
							infonum: {
								index: 2, //0:没有,1:顶,2:踩
								dingnum: 12,
								cainum: 14
							},
							commentnum: 10,
							sharenum: 10
						},
						{
							userpic: '../../static/demo/userpic/1.jpg',
							username: '张三',
							isguanzhu: false,
							title: '标题',
							type: 'video', //img:图文 video:视频
							titlepic: '../../static/demo/datapic/1.jpg',
							playnum: 200000,
							long: '2:22',
							infonum: {
								index: 2, //0:没有,1:顶,2:踩
								dingnum: 12,
								cainum: 14
							},
							commentnum: 10,
							sharenum: 10
						},
						{
							userpic: '../../static/demo/userpic/2.jpg',
							username: '李四',
							isguanzhu: false,
							title: '标题',
							type: 'img', //img:图文 video:视频
							titlepic: '../../static/demo/datapic/2.jpg',
							playnum: 200000,
							long: '2:22',
							infonum: {
								index: 1, //0:没有,1:顶,2:踩
								dingnum: 12,
								cainum: 14
							},
							commentnum: 10,
							sharenum: 10
						}
					]
				},
				{
				   loadtext:"上拉加载更多...",
					list: [
							{
							userpic: '../../static/demo/userpic/3.jpg',
							username: '张三',
							isguanzhu: false,
							title: '标题',
							type: 'video', //img:图文 video:视频
							titlepic: '../../static/demo/datapic/3.jpg',
							playnum: 200000,
							long: '2:22',
							infonum: {
								index: 2, //0:没有,1:顶,2:踩
								dingnum: 12,
								cainum: 14
							},
							commentnum: 10,
							sharenum: 10
						},
						{
							userpic: '../../static/demo/userpic/4.jpg',
							username: '张三',
							isguanzhu: false,
							title: '标题',
							type: 'img', //img:图文 video:视频
							titlepic: '../../static/demo/datapic/4.jpg',
							playnum: 200000,
							long: '2:22',
							infonum: {
								index: 2, //0:没有,1:顶,2:踩
								dingnum: 12,
								cainum: 14
							},
							commentnum: 10,
							sharenum: 10
						},
						{
							userpic: '../../static/demo/userpic/5.jpg',
							username: '张三',
							isguanzhu: false,
							title: '标题',
							type: 'img', //img:图文 video:视频
							titlepic: '../../static/demo/datapic/5.jpg',
							playnum: 200000,
							long: '2:22',
							infonum: {
								index: 2, //0:没有,1:顶,2:踩
								dingnum: 12,
								cainum: 14
							},
							commentnum: 10,
							sharenum: 10
						},
						{
							userpic: '../../static/demo/userpic/6.jpg',
							username: '张三',
							isguanzhu: true,
							title: '标题',
							type: 'img', //img:图文 video:视频
							titlepic: '../../static/demo/datapic/6.jpg',
							playnum: 200000,
							long: '2:22',
							infonum: {
								index: 2, //0:没有,1:顶,2:踩
								dingnum: 12,
								cainum: 14
							},
							commentnum: 10,
							sharenum: 10
						}
					]
				},
				{ 
				   loadtext:"上拉加载更多...",	
					list: [
						{
							userpic: '../../static/demo/userpic/7.jpg',
							username: '张三',
							isguanzhu: true,
							title: '标题',
							type: 'img', //img:图文 video:视频
							titlepic: '../../static/demo/datapic/7.jpg',
							playnum: 200000,
							long: '2:22',
							infonum: {
								index: 2, //0:没有,1:顶,2:踩
								dingnum: 12,
								cainum: 14
							},
							commentnum: 10,
							sharenum: 10
						},
						{
							userpic: '../../static/demo/userpic/8.jpg',
							username: '张三',
							isguanzhu: true,
							title: '标题',
							type: 'img', //img:图文 video:视频
							titlepic: '../../static/demo/datapic/8.jpg',
							playnum: 200000,
							long: '2:22',
							infonum: {
								index: 2, //0:没有,1:顶,2:踩
								dingnum: 12,
								cainum: 14
							},
							commentnum: 10,
							sharenum: 10
						},
						{
							userpic: '../../static/demo/userpic/9.jpg',
							username: '张三',
							isguanzhu: true,
							title: '标题',
							type: 'img', //img:图文 video:视频
							titlepic: '../../static/demo/datapic/9.jpg',
							playnum: 200000,
							long: '2:22',
							infonum: {
								index: 2, //0:没有,1:顶,2:踩
								dingnum: 12,
								cainum: 14
							},
							commentnum: 10,
							sharenum: 10
						},
					] },
				{ 
				   loadtext:"上拉加载更多...",	
					list: [
						{
							userpic: '../../static/demo/userpic/10.jpg',
							username: '张三',
							isguanzhu: true,
							title: '标题',
							type: 'img', //img:图文 video:视频
							titlepic: '../../static/demo/datapic/10.jpg',
							playnum: 200000,
							long: '2:22',
							infonum: {
								index: 2, //0:没有,1:顶,2:踩
								dingnum: 12,
								cainum: 14
							},
							commentnum: 10,
							sharenum: 10
						},
						{
							userpic: '../../static/demo/userpic/11.jpg',
							username: '张三',
							isguanzhu: true,
							title: '标题',
							type: 'img', //img:图文 video:视频
							titlepic: '../../static/demo/datapic/11.jpg',
							playnum: 200000,
							long: '2:22',
							infonum: {
								index: 2, //0:没有,1:顶,2:踩
								dingnum: 12,
								cainum: 14
							},
							commentnum: 10,
							sharenum: 10
						},
						{
							userpic: '../../static/demo/userpic/12.jpg',
							username: '张三',
							isguanzhu: true,
							title: '标题',
							type: 'img', //img:图文 video:视频
							titlepic: '../../static/demo/datapic/12.jpg',
							playnum: 200000,
							long: '2:22',
							infonum: {
								index: 2, //0:没有,1:顶,2:踩
								dingnum: 12,
								cainum: 14
							},
							commentnum: 10,
							sharenum: 10
						}
						
					] },
				{ 
				   loadtext:"上拉加载更多...",	
					list: [] },
				{ 
				   loadtext:"上拉加载更多...",	
					list: [] }
			]
		};
	},
	onLoad() {
		uni.getSystemInfo({
			success: (res)=> {
				let height=res.windowHeight-uni.upx2px(100)
				this.swiperHeight=height
				//console.log(this.swiperHeight)
			}
		});
	},
	//监听搜索框
	onNavigationBarSearchInputClicked() {
		uni.navigateTo({
			url:'../search/search'
		})
		
	},
	//监听  发布按钮
	onNavigationBarButtonTap(e) {
		console.log(e);
		switch (e.index){
			case 1:
			//打开发布页
			uni.navigateTo({
				url:'../add-input/add-input'
			})
				break;
			default:
				break;
		}
		
	},
	methods: {
		//上拉加载
		loadmore(index){
			if(this.newList[index].loadtext!="上拉加载更多..."){return};
			//更改状态
			this.newList[index].loadtext="加载中..."
			setTimeout(()=> {
				let obj={
							userpic: '../../static/demo/userpic/15.jpg',
							username: '张三',
							isguanzhu: false,
							title: '标题',
							type: 'img', //img:图文 video:视频
							titlepic: '../../static/demo/datapic/15.jpg',
							playnum: 200000,
							long: '2:22',
							infonum: {
								index: 2, //0:没有,1:顶,2:踩
								dingnum: 12,
								cainum: 14
							},
							commentnum: 10,
							sharenum: 10
						};				
			this.newList[index].list.push(obj);
			this.newList[index].loadtext="上拉加载更多..."
			}, 1000);
			//this.newList[index].loadtext="已经到底啦..."
		},
		
		//事件接受子组件传过来的index    子组件$emit('tabtap', index)
		tabtap(index) {
			this.tabIndex = index;
		},
		//滑动事件
		tabChange(e) {
			console.log(e.detail);
			this.tabIndex = e.detail.current;
		}
	}
	
	
}
</script>
<style lang="less" scoped>
	
	
	
</style>
