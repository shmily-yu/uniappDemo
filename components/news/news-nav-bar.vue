<template>
	<view>
		<uni-nav-bar :status-bar="true" @clickRight="openAdd" :fixed="true" >
			<!-- 中间 -->
			<view class="nav-tab-bar u-f-ajc ">
				<block v-for="(item, index) in tabBars" :key="item.id">
					<view class=" u-f-ajc" :class="{ active: tabIndex == index }" 
					@tap="changeTab(index)">
						{{ item.name }}
						<view v-if="tabIndex == index" class="nav-tab-bar-line"></view>
					</view>
				</block>
			</view>
			<!-- 左 -->
			<block slot="left">
				<view class="nav-left"><view class="icon iconfont icon-qiandao"></view></view>
			</block>
			<!-- 右 -->
			<block slot="right">
				<view class="nav-right u-f-ajc"><view class="icon iconfont icon-bianji"></view></view>
			</block>
		</uni-nav-bar>
	</view>
</template>

<script>
import uniNavBar from '@/components/uni-nav-bar/uni-nav-bar.vue';
export default {
	components: {
		uniNavBar
	},
	props: {
		tabBars: Array,
		tabIndex: Number
	},
	methods: {
		changeTab(index) {
			this.$emit('changeTab',index);
		},
		//跳转发布页
		openAdd() {
			uni.navigateTo({
				url: '../add-input/add-input'
			});
		}
	}
};
</script>

<style scoped>
.nav-left > view,
.nav-right > view {
	font-size: 40rpx;
}
.nav-left {
	margin-left: 16rpx;
}
.nav-left > view {
	color: #ff9619;
}
.nav-right {
	width: 100%;
}
.nav-tab-bar {
	margin-left: -20rpx;
	width: 100%;
	position: relative;
}
.nav-tab-bar > view {
	font-size: 32rpx;
	padding: 0 15rpx;
	font-weight: bold;
	color: #ff9619;
}
.active {
	color: #333333 !important;
}
.nav-tab-bar-line {
	border-bottom: 5rpx solid #fede33;
	border-top: 5rpx solid #fede33;
	width: 60rpx;
	top: 56rpx;
	border-radius: 20rpx;
	position: absolute;
}
</style>
