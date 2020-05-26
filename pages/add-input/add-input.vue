<template>
	<view>
		<!-- 自定义导航栏 -->
		<uni-nav-bar :status-bar="true" color="#ffffff" background-color="#007AFF" @clickLeft="back" @clickRight="submit">
			<!-- 中间 -->
			<view class="u-f-ajc" style="margin-left: 90rpx; text-align: center;" @tap="changelook">
				<text>{{ secret }}</text>
				<uni-icons type="arrowdown" color="#ffffff" size="18" />
			</view>
			<!-- 左右 -->
			<view slot="left" left-icon="arrowleft">返回</view>
			<view slot="right">发布</view>
		</uni-nav-bar>
		<!-- 文本框 -->
		<view class="uni-textarea"><textarea placeholder="说一句话吧" v-model="text" /></view>

		<!-- 上传图片 -->
		<up-load-img @uplaod="upload"></up-load-img>
		<!-- 弹出公告 -->
		<uni-popup ref="popup" type="center">
			<view class="gonggao">
				<view class="u-f-ajc"><image src="../../static/common/addinput.png" mode="widthFix"></image></view>
				<view class="u-f-ajc">1.涉及黄色，政治，广告及骚扰信息</view>
				<view class="u-f-ajc">2.涉及黄色，政治，广告及骚扰信息</view>
				<view class="u-f-ajc">3.涉及黄色，政治，广告及骚扰信息</view>
				<view class="u-f-ajc">4.涉及黄色，政治，广告及骚扰信息</view>
				<view class="u-f-ajc">5.涉及黄色，政治，广告及骚扰信息</view>
				<button type="default" @tap="close">朕知道了</button>
			</view>
		</uni-popup>
	</view>
</template>

<script>
import uniIcons from '@/components/uni-icons/uni-icons.vue';
import uniNavBar from '@/components/uni-nav-bar/uni-nav-bar.vue';
import upLoadImg from '../../components/common/up-load-img.vue';
import uniPopup from '../../components/uni-popup/uni-popup.vue';
let changelook = ['所有人可见', '仅自己可见', '选中的朋友可见'];

export default {
	components: {
		uniIcons,
		uniNavBar,
		upLoadImg,
		uniPopup
	},
	data() {
		return {
			secret: '所有人可见',
			text: '',
			imageList: [],
			isget: false //标识符
		};
	},
	//监听页面返回
	onBackPress() {
		//如果页面没有值则不提示保存
		if (!this.text && this.imageList.length < 1) {
			return;
		} else {
			if (!this.isget) {
				this.save();
				return true; //使页面不反回
			}
		}
	},

	methods: {
		//保存草稿
		save() {
			uni.showModal({
				content: '是否要保存为草稿?',
				cancelText: '不保存',
				confirmText: '保存',
				success: res => {
					if (res.confirm) {
						console.log('save');
					} else {
						console.log('no');
					}
					this.isget = true; //修改标识符
					//返回
					uni.navigateBack({
						delta: 1
					});
				}
			});
		},
		//返回
		back() {
			uni.navigateBack({
				delta: 1
			});
		},
		//发布
		submit() {
			console.log('发布');
		},
		//所有人可见
		changelook() {
			uni.showActionSheet({
				itemList: changelook,
				success: res => {
					this.secret = changelook[res.tapIndex];
					//选中项等于数组索引
				}
			});
		},
		//事件接受子组件传过来的参数
		upload(arr) {
			this.imageList = arr;
		},
		//关弹窗
		close() {
			this.$refs.popup.close();
		}
	}
};
</script>

<style lang="less">
.uni-textarea {
	border: 0.5rpx solid #c8c7cc;
}
.gonggao {
	width: 500rpx;
	background: #ffffff;
	padding: 10rpx 16rpx 20rpx;
	border-radius: 20rpx;
}
.gonggao image {
	width: 75%;
	margin-bottom: 20rpx;
}
.gonggao button {
	margin-top: 20rpx;
	background: #ffe934;
	color: #171606;
}
</style>
