<template>
	<!-- 滚动条 -->
	<view class="uni-tab-bar">
		<scroll-view scroll-x class="uni-swiper-tab" :style="scrollStyle">
			<block v-for="(tab, index) in tabBar" :key="tab.id">
				<view class="swiper-tab-list" :class="{ active: tabIndex == index }" @tap="tabtap(index)" :style="scrollItemStyle">
					{{ tab.name }} {{tab.num?tab.num:''}}
					<!-- tab下面的小黄条 -->
					<view class="swiper-tab-line"></view>
				</view>
			</block>
		</scroll-view>
	</view>
</template>

<script>
export default {
	data() {
		return {};
	},
	props: {
		tabBar: Array,
		tabIndex: Number,
		scrollStyle: {
			type: String,
			default: ''
		},
		scrollItemStyle: {
			type: String,
			default: ''
		}
	},
	methods: {
		//子组件向父组件传递数据 index
		tabtap(index) {
			this.$emit('tabtap', index);
		}
	}
};
</script>

<style lang="less" scoped>
.uni-swiper-tab {
	border-bottom: 1upx solid #eeeeee;
}
.swiper-tab-list {
	color: #969696;
	font-weight: bold;
}
.uni-tab-bar .active {
	color: #343434;
}
.active .swiper-tab-line {
	border-bottom: solid 6rpx #ffff00;
	border-top: solid 6rpx #ffff00;
	width: 70rpx;
	margin: auto;
	border-radius: 20rpx;
}
</style>
