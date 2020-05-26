<template>
	<view class="uni-list list-pd">
		<view class="uni-list-cell cell-pd">
			<view class="uni-uploader">
				<view class="uni-uploader-head">
					<view class="uni-uploader-title">点击可预览选好的图片</view>
					<view class="uni-uploader-info">{{ imageList.length }}/9</view>
				</view>
				<view class="uni-uploader-body">
					<view class="uni-uploader__files">
						<block v-for="(image, index) in imageList" :key="index">
							<view class="uni-uploader__file">
								<!-- 删除图标 -->
								<image class="uni-uploader__img" :src="image" :data-src="image" @tap="previewImage"></image>
								<view class="icon iconfont icon-shanchu" @tap="deltapic(index)">	</view>	
								
							</view>
						</block>
						<view class="uni-uploader__input-box"><view class="uni-uploader__input" @tap="chooseImage"></view></view>
					</view>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	
	export default{
		data() {
			return {
				imageList: []
			}
		},
		methods:{
			// 点击图片预览
			previewImage: function(e) {
				var current = e.target.dataset.src;
				uni.previewImage({
					current: current,
					urls: this.imageList
				});
			},
			//选择图片
			chooseImage: async function() {
				uni.chooseImage({
					success: res => {
						this.imageList = this.imageList.concat(res.tempFilePaths);
						this.$emit('upload',this.imageList)//通过事件把图片数量传递到父组件
					}
				});
			},
			//删除图片
			deltapic(index){
				uni.showModal({
				    title: '提示',
				    content: '是否要删除图片?',
				    success:  (res) =>{
				        if (res.confirm) {
				           this.imageList.splice(index,1)
							  this.$emit('upload',this.imageList)
							  
				        } 
				    }
				});
			}
			
		},
		props:{
			
		}
	}
</script>

<style scoped>
	.cell-pd {
			padding: 22upx 30upx;
		}
	
		.list-pd {
			margin-top: 60upx;
		}
		.icon-shanchu{
			background: #333333;
			color: #F7F7F7;
			position:absolute;
			border-radius: 8rpx;
			padding: 2rpx 6rpx;
			right: 0;
			top: 0;
			}
			.uni-uploader__file{
				position: relative;
			}
			
</style>
