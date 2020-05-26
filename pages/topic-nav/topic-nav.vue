<template>
	<view>
		<view :fixed="true">
			<!-- 滑块 -->
			<swiper-tab-head :tabBar="tabBar" :tabIndex="tabIndex" @tabtap="tabtap"></swiper-tab-head>
		</view>
		<!-- 滑动切换 -->
		<view class="uni-tab-bar">
			<swiper class="swiper-box" :style="{ height: swiperHeight + 'px' }" :current="tabIndex" @change="tabChange">
				<swiper-item v-for="(items, index) in newList" :key="index">
					<scroll-view scroll-y="true" class="list" @scrolltolower="loadmore(index)">
						<!-- 下拉到底部加载。。。 -->
						<template v-if="items.list.length > 0">
							<!-- 话题列表 -->
							<view class="topic-view">
								<block v-for="(item, index1) in items.list" :key="index1">
									<topic-list :item="item" :index="index1"></topic-list>
									<!-- 通过v-bind绑定将数据向下传递 -->
								</block>
							</view>
							
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
import swiperTabHead from '../../components/index/swiper-tab-head.vue';
import nothing from '../../components/common/nothing.vue'; //无内容组件
import loadMore from '../../components/common/load-more.vue'; //下拉加载组件
import topicList from '../../components/news/topic-list.vue'; //列表

export default {
	components: {
		swiperTabHead,
		nothing,
		loadMore,
		topicList
	},
	data() {
		return {
			swiperHeight: 500,
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
					loadtext: '上拉加载更多...',
					list: [
						{
							titlepic: '../../static/demo/topicpic/1.jpeg',
							title: '话题名称',
							desc: '我是话题描述',
							totalnum: 50,
							todaynum: 10
						},
						{
							titlepic: '../../static/demo/topicpic/2.jpeg',
							title: '话题名称',
							desc: '我是话题描述',
							totalnum: 50,
							todaynum: 10
						},
						{
							titlepic: '../../static/demo/topicpic/3.jpeg',
							title: '话题名称',
							desc: '我是话题描述',
							totalnum: 50,
							todaynum: 10
						},
						{
							titlepic: '../../static/demo/topicpic/4.jpeg',
							title: '话题名称',
							desc: '我是话题描述',
							totalnum: 50,
							todaynum: 10
						},
						{
							titlepic: '../../static/demo/topicpic/5.jpeg',
							title: '话题名称',
							desc: '我是话题描述',
							totalnum: 50,
							todaynum: 10
						},
						{
							titlepic: '../../static/demo/topicpic/6.jpeg',
							title: '话题名称',
							desc: '我是话题描述',
							totalnum: 50,
							todaynum: 10
						}
					]
				},
				{
					loadtext: '上拉加载更多...',
					list: [
						{
							titlepic: '../../static/demo/topicpic/1.jpeg',
							title: '话题名称',
							desc: '我是话题描述',
							totalnum: 50,
							todaynum: 10
						},
						{
							titlepic: '../../static/demo/topicpic/2.jpeg',
							title: '话题名称',
							desc: '我是话题描述',
							totalnum: 50,
							todaynum: 10
						},
						{
							titlepic: '../../static/demo/topicpic/3.jpeg',
							title: '话题名称',
							desc: '我是话题描述',
							totalnum: 50,
							todaynum: 10
						},
						{
							titlepic: '../../static/demo/topicpic/4.jpeg',
							title: '话题名称',
							desc: '我是话题描述',
							totalnum: 50,
							todaynum: 10
						},
						{
							titlepic: '../../static/demo/topicpic/5.jpeg',
							title: '话题名称',
							desc: '我是话题描述',
							totalnum: 50,
							todaynum: 10
						},
						{
							titlepic: '../../static/demo/topicpic/6.jpeg',
							title: '话题名称',
							desc: '我是话题描述',
							totalnum: 50,
							todaynum: 10
						}
					]
				},
				{
					loadtext: '上拉加载更多...',
					list: [
					{
						titlepic: '../../static/demo/topicpic/1.jpeg',
						title: '话题名称',
						desc: '我是话题描述',
						totalnum: 50,
						todaynum: 10
					},
					{
						titlepic: '../../static/demo/topicpic/2.jpeg',
						title: '话题名称',
						desc: '我是话题描述',
						totalnum: 50,
						todaynum: 10
					},
					{
						titlepic: '../../static/demo/topicpic/3.jpeg',
						title: '话题名称',
						desc: '我是话题描述',
						totalnum: 50,
						todaynum: 10
					},
					{
						titlepic: '../../static/demo/topicpic/4.jpeg',
						title: '话题名称',
						desc: '我是话题描述',
						totalnum: 50,
						todaynum: 10
					},
					{
						titlepic: '../../static/demo/topicpic/5.jpeg',
						title: '话题名称',
						desc: '我是话题描述',
						totalnum: 50,
						todaynum: 10
					},
					{
						titlepic: '../../static/demo/topicpic/6.jpeg',
						title: '话题名称',
						desc: '我是话题描述',
						totalnum: 50,
						todaynum: 10
					}
				]
				},
				{
					loadtext: '上拉加载更多...',
					list: []
				},
				{
					loadtext: '上拉加载更多...',
					list: []
				},
				{
					loadtext: '上拉加载更多...',
					list: []
				}
			]
		};
	},
	onLoad() {
		uni.getSystemInfo({
			success: res => {
				let height = res.windowHeight - uni.upx2px(100);
				this.swiperHeight = height;
				//console.log(this.swiperHeight)
			}
		});
	},
	methods: {
		loadmore(index) {
			if (this.newList[index].loadtext != '上拉加载更多...') {
				return;
			}
			//更改状态
			this.newList[index].loadtext = '加载中...';
			setTimeout(() => {
				let obj = {
						titlepic: '../../static/demo/topicpic/7.jpeg',
						title: '话题名称',
						desc: '我是话题描述',
						totalnum: 50,
						todaynum: 10
					};
				this.newList[index].list.push(obj);
				this.newList[index].loadtext = '上拉加载更多...';
			}, 1000);
			//this.newList[index].loadtext="已经到底啦..."
		},
		tabtap(index) {
			this.tabIndex = index;
		},
		tabChange(e) {
			console.log(e.detail);
			this.tabIndex = e.detail.current;
		}
	}
};
</script>

<style>
	.topic-view{
		padding: 0 20rpx;
	}
</style>
