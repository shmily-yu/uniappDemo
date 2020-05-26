<template>
	<view>
		<!-- 关注/话题 -->
		<news-nav-bar :tabBars="tabBars" :tabIndex="tabIndex" @changeTab="changeTab"></news-nav-bar>

		<view class="uni-tab-bar">
			<swiper class="swiper-box" :style="{ height: swiperHeight + 'px' }" :current="tabIndex" @change="tabChange">
				<!-- 关注 -->
				<swiper-item>
					<scroll-view scroll-y class="list" @scrolltolower="loadmore">
						<!-- 列表 -->
						<block v-for="(item, index) in guanzhu.list" :key="index"><common-list :item="item" :index="index"></common-list></block>
						<!-- 上拉加载 -->
						<load-more :loadtext="guanzhu.loadtext"></load-more>
					</scroll-view>
				</swiper-item>
				<!-- 话题 -->
				<swiper-item>
					<scroll-view scroll-y class="list">
						<!-- 搜索框 -->
						<view class="search-input"><input class="uni-input" placeholder-class="icon iconfont icon-sousuo topic-search" placeholder="搜索内容" /></view>
						<!-- 轮播图 -->
						<swiper class="topic-swiper" :indicator-dots="true" :autoplay="true" :interval="3000" :duration="1000">
							<block v-for="(item, index) in topic.swiper" :key="index">
								<swiper-item><image :src="item.src" mode="scaleToFill" lazy-load></image></swiper-item>
							</block>
						</swiper>
						<!-- 热门分类 -->
						<topic-nav :nav="topic.nav"></topic-nav>
						<!-- 最近更新 -->
						<view class="topic-new">
							<view>最近更新</view>
							<block v-for="(item, index) in topic.list" :key="index">
								<topic-list :item="item" :index="index"></topic-list>
							</block>
						</view>
										
					</scroll-view>
				</swiper-item>
			</swiper>
		</view>
	</view>
</template>

<script>
import loadMore from '../../components/common/load-more.vue'; //下拉加载组件
import topicNav from '../../components/news/topic-nav.vue'; //热门分类
import topicList from '../../components/news/topic-list.vue'//列表

import commonList from '../../components/common/common-list.vue';
import newsNavBar from '../../components/news/news-nav-bar.vue';
export default {
	components: {
		commonList,
		newsNavBar,
		loadMore,
		topicNav,
		topicList
	},
	data() {
		return {
			tabIndex: 0,
			swiperHeight: 500,

			tabBars: [{ name: '关注', id: 'guanzhu' }, { name: '话题', id: 'topic' }],
			topic: {
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
				],
				swiper: [{ src: '../../static/demo/banner1.jpg' }, { src: '../../static/demo/banner2.jpg' }, { src: '../../static/demo/banner3.jpg' }],
				nav: [{ name: '最新' }, { name: '游戏' }, { name: '打卡' }, { name: '情感' }, { name: '故事' }, { name: '喜爱' }]
			},
			guanzhu: {
				loadtext: '上拉加载更多...',
				list: [
					// 文字
					{
						userpic: '../../static/demo/userpic/1.jpg',
						username: '户侯',
						sex: 1, //0 男 1 女
						age: 25,
						isguanzhu: false,
						title:
							'比如，都说我们有全产业链优势，但这是按照正常时期的状态安排的产能。那么应急状态下产能够不够，怎么调配规划，都是不知道的。再比如，都说经济稳定性增强，发展后劲很足。那么到底有多稳定，能够经历多大的考验，多大规模的事情会影响到经济的持续稳定，也是不知道的。',
						titlepic: '',
						video: false,
						share: false,
						path: '深圳 龙岗',
						sharenum: 20,
						commentnum: 30,
						goodnum: 20
					},
					// 图文
					{
						userpic: '../../static/demo/userpic/12.jpg',
						username: '扣扣',
						sex: 0, //0 男 1 女
						age: 25,
						isguanzhu: false,
						title: '我是标题',
						titlepic: '../../static/demo/datapic/12.jpg',
						video: false,
						share: false,
						path: '深圳 龙岗',
						sharenum: 20,
						commentnum: 30,
						goodnum: 20
					},
					// 视频
					{
						userpic: '../../static/demo/userpic/13.jpg',
						username: '动端',
						sex: 0, //0 男 1 女
						age: 25,
						isguanzhu: false,
						title: '我是标题',
						titlepic: '../../static/demo/datapic/13.jpg',
						video: {
							looknum: '20w',
							long: '2:47'
						},
						share: false,
						path: '深圳 龙岗',
						sharenum: 20,
						commentnum: 30,
						goodnum: 20
					},
					// 分享
					{
						userpic: '../../static/demo/userpic/14.jpg',
						username: '威威',
						sex: 0, //0 男 1 女
						age: 25,
						isguanzhu: false,
						title: '我是标题',
						titlepic: '',
						video: false,
						share: {
							title: '我是分享的标题',
							titlepic: '../../static/demo/datapic/14.jpg'
						},
						path: '深圳 龙岗',
						sharenum: 20,
						commentnum: 30,
						goodnum: 20
					}
				]
			}
		};
	},
	methods: {
		//关注话题切换
		changeTab(index) {
			this.tabIndex = index;
		},
		tabChange(e) {
			console.log(e.detail);
			this.tabIndex = e.detail.current;
		},
		//监听滑动触底事件
		loadmore() {
			if (this.guanzhu.loadtext != '上拉加载更多...') {
				return;
			}
			//更改状态
			this.guanzhu.loadtext = '加载中...';
			setTimeout(() => {
				let obj = {
					userpic: '../../static/demo/userpic/22.jpg',
					username: '动端',
					sex: 1, //0 男 1 女
					age: 25,
					isguanzhu: false,
					title: '我是标题',
					titlepic: '../../static/demo/datapic/22.jpg',
					video: false,
					share: false,
					path: '深圳 龙岗',
					sharenum: 20,
					commentnum: 30,
					goodnum: 20
				};
				this.guanzhu.list.push(obj);
				this.guanzhu.loadtext = '上拉加载更多...';
			}, 1000);
			//this.guanzhu.loadtext="已经到底啦..."
		},
		onLoad() {
			uni.getSystemInfo({
				success: res => {
					let height = res.windowHeight - uni.upx2px(100);
					this.swiperHeight = height;
					//console.log(this.swiperHeight)
				}
			});
		}
	}
};
</script>

<style scoped>
.search-input {
	padding: 20rpx;
}
.search-input > input {
	background: #f4f4f4;
	border-radius: 10rpx;
}
.topic-search {
	display: flex;
	justify-content: center;
	font-size: 27rpx;
}

.topic-swiper {
	padding: 0 20rpx 20rpx 20rpx;
}
.topic-swiper image {
	/* height: 100%; */
	width: 100%;
	border-radius: 10rpx;
}

.topic-new {
	padding: 20rpx;
}
.topic-new > view:first-child {
	padding-bottom: 5rpx;
	font-size: 32rpx;
}

</style>
