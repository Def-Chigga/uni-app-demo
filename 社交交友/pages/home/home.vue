<template>
	<view class="home">
		<!-- tab选项卡 -->
		<scroll-view class="tab" scroll-x :scroll-into-view="scrollInto" scroll-with-animation
		 >
			<view class="tab-list">
				<view :id="'tab'+index" @click="changeTab(index)" :class="['list-item', tabIndex === index ? 'active' : '']" v-for="(item,index) in tabList" :key="index">{{item}}</view>
			</view>
		</scroll-view>
		<swiper 
		class="swiper" :autoplay="false" :current="tabIndex" @change="changeSwiper">
			<swiper-item v-for="(item,index) in newsList" :key="index">
				<scroll-view class="swiper-list" scroll-y="true">
					<view class="list-item"  v-for="(item1,index1) in item.list" :key="index1">
						{{item1}}
					</view>
				</scroll-view>
			</swiper-item>
		</swiper>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				tabList: ['关注','推荐','体育','热点','财经','娱乐2','关注2','推荐2','体育2','热点2','财经2','娱乐2'],
				tabIndex: 0,
				scrollInto: '',
				newsList: [
					{
						list: ['11','2','3','4','5']
					},
					{
						list: ['12','2','3','4','5']
					},
					{
						list: ['13','2','3','4','5']
					},
					{
						list: ['14','2','3','4','5']
					},
					{
						list: ['15','2','3','4','5']
					}
				]
			};
		},
		methods: {
			// 切换tab栏
			changeTab(idx) {
				if(this.tabIndex === idx){
					return
				}
				this.tabIndex = idx
				// 滚动到指定元素
				this.scrollInto = 'tab'+idx
				console.log(this.scrollInto);
			},
			// 切换swiper
			changeSwiper(e) {
				console.log(e.detail.current);
				this.changeTab(e.detail.current)
			}
		}
	}
</script>

<style lang="scss">
.home{
	width: 100%;
	height: 100%;
	background: #FFFFFF;
	.tab{
		width: 100%;
		height: 100rpx;
		.tab-list{
			width: 100%;
			height: 100%;
			@include flexRow;
			.list-item{
				white-space: nowrap;
				padding: 0 30rpx;
				box-sizing: border-box;
				font-size: 32rpx;
				&.active{
					font-size: 40rpx;
					font-weight: bold;
					color: $chigga-main-color;
				}
			}
		}
	}
	.swiper{
		width: 100%;
		height: calc(100% - 100rpx);
		background: red;
		.swiper-list{
			height: 100%;
		}
	}
}
</style>
