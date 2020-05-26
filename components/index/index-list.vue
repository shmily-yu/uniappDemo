<template>
	<view class="index-list animated fadeInLeft fast">
			<!-- 第一行 -->
			<view class="index-list1 u-f-ajc u-f-jsb">
				<view class="u-f-ac">
					<image :src="item.userpic" mode="widthFix" lazy-load></image>
					{{ item.username }}
				</view>
				<view class="u-f-ac" v-show="!isguanzhu" @tap="guanzhu">
					<view class="icon iconfont icon-zengjia"></view>关注
				</view>
			</view>
			<!-- 第二行 -->
			<view class="index-list2" @tap="opendetail">{{ item.title }}</view>
			<!-- 第三行 -->
			<view class="index-list3 u-f-ajc" @tap="opendetail">
				
				<!-- 图片 -->
				<image :src="item.titlepic" mode="widthFix" lazy-load></image>
				<template v-if="type === 'video'">
					<view>
						<!-- 视频 -->
						<view class="index-list-play icon iconfont icon-bofang"></view>
						<!-- 视频信息 -->
						<view class="index-list-playinfo">{{ item.playnum }}次播放 {{ item.long }}</view>
					</view>
				</template>
			</view>
			<!-- 第四行 -->
			<view class="index-list4 u-f-ajc u-f-jsb">
				<view class="u-f-ac ">
					<!-- 顶 -->
					<view class="u-f-ac" :class="{'active':(infonum.index===1)}"
					@tap="caozuo('ding')"
					>
						<view class="icon iconfont icon-icon_xiaolian-mian"></view>
						<view class="">{{ infonum.dingnum }}</view>
					</view>
					<!-- 踩 -->
					<view class="u-f-ac" :class="{'active':(infonum.index===2)}"
					@tap="caozuo('cai')"
					>
						<view class="icon iconfont icon-kulian"></view>
						<view class="">{{ infonum.cainum }}</view>
					</view>
				</view>
				<view class="u-f-ac">
					<view class="u-f-ac">
						<view class="icon iconfont icon-pinglun"></view>
						<view class="">{{item.commentnum}}</view>
					</view>
					<view class="u-f-ac">
						<view class="icon iconfont icon-zhuanfa"></view>
						<view class="">{{item.sharenum}}</view>
					</view>
				</view>
			</view>
		</view>
	
</template>

<script>
	export default {
		data() {
			return {
				//把接受过来的值重新赋值一下
				isguanzhu:this.item.isguanzhu,
				infonum:this.item.infonum,
				type:this.item.type
				
			};
		},
		//接受父组件传过来的值
		props:{
			item:Object,
			index:Number
		},
		methods:{
			//关注事件
			guanzhu(){
				this.isguanzhu=true;
				uni.showToast({
					title:"关注成功!"
				})
			},
			//顶踩
			caozuo(type){
				// infonum: {
				// 	index: 2, //0:没有,1:顶,2:踩
				// 	dingnum: 12,
				// 	cainum: 14
				// },
				switch (type){
					case "ding":
					if(this.item.infonum.index==0){
						this.item.infonum.index=1;
						this.item.infonum.dingnum++;
					}
					else if(this.infonum.index==1){
						this.infonum.index=0;
						this.infonum.dingnum--;
					}
					else if(this.infonum.index==2){
						this.infonum.index=1;
						this.infonum.dingnum++;
						this.infonum.cainum--;
					}
					break;
					case "cai":
					if(this.infonum.index==0){
						this.infonum.index=2;
						this.infonum.cainum++;
					}
					else if(this.infonum.index==2){
						this.infonum.index=0;
						this.infonum.cainum--;
					}
					else if(this.infonum.index==1){
						this.infonum.index=2;
						this.infonum.cainum++;
						this.infonum.dingnum--;
					}
					break;
				}
			},
			opendetail(){
				console.log("进入详情")
			}
		}
	}
</script>

<style lang="less" scoped>
.index-list {
	padding: 20rpx;
	border-bottom: 1rpx solid #eeeeee;
}
.index-list1 {
	padding: 10px 0;
	view:first-child {
		color: #999999;
		//头像
		image {
			width: 85rpx;
			height: 85rpx;
			border-radius: 100%;
			margin-right: 10rpx;
		}
	}
	view:last-child {
		border-radius: 5rpx;
		padding: 0 10rpx;
		background: #f4f4f4;
	}
}
.index-list2 {
	padding-top: 15rpx;
	font-size: 32rpx;
}
.index-list3 {
	padding-top: 15rpx;
	position: relative;
	//大图
	image {
		width: 100%;
		border-radius: 20rpx;
	}
	//视频
	.index-list-play {
		position: absolute;
		right: 136px;
		top: 38px;
		font-size: 130rpx;
		color: #8f8f8f;
	}
	//视频信息
	.index-list-playinfo {
		position: absolute;
		bottom: 8rpx;
		right: 8rpx;
		background: rgba(51, 51, 51, 0.72);
		color: #ffffff;
		border-radius: 40rpx;
		font-size: 12px;
		padding: 0 10rpx;
	}
}
.index-list4 {
	padding: 10px 0;
	
	view {
		color: #e8e8e8;
		//顶踩颜色
		.active{
			color: #ecec00;
			view{
				color: #ecec00;
			}
			}
		view {
			margin-right: 10rpx;
			:first-child {
				margin-right: 10rpx;
			}
		}
	}
}

</style>
