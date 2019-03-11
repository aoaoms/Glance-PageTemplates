<!-- glance 店铺分类 -->
<template name="glance-ShopClassify">
	<view class="glance-shop-classify">
		<!-- 顶部显示搜索 -->
		
		<!-- 左侧列表占位 -->
		<view class="glance-shop-classify-left" >
			<!-- 左侧主分类列表 -->
			<view v-for="item in maintitels" :key='index'>
				<!-- 左侧分类项目 -->
				<view class="glance-shop-classify-left-item" style="" @click="clickleftitem(maintitels[index],index)"  >
				<view style="height: 15px;width: 3%;background-color: #ffffff;" :style="{'background-color':[activemaintitel == maintitels[index] ? '#f40':'#ffffff']}"></view>
				<view style="text-align: center;line-height: 15px;width: 93%;font-size: 0.8rem; " :class="[activemaintitel == maintitels[index] ? 'glance-shop-classify-left-item-activetxt':'']"> {{ maintitels[index] }}</view>
				</view>
			</view>
		</view>
		<!-- 右侧列表 -->
		<view style="float: right; width: 80%;">
			<!-- 左侧主分类列表 -->
			<scroll-view scroll-y= "true" scroll-left="0" scroll-with-animation="true" :scroll-into-view = "scrollintoid" :style="{height: scrollheight + 'px','overflow-y':auto}" @scroll ="scroll">
				<view :id="'scrollinto-' + idx" v-for="(des,idx) in maintitels" :key='idx' >
					<view v-for="(item,index) in subitems" :key='index' v-if="item.maintitel == maintitels[idx]">
						<view class="glance-shop-classify-right-item">
							<!-- 右侧顶部广告图 -->
							<image :src="item.bannerimgsrc" mode="scaleToFill" @error="imgerr" style="height: 120px;width: 100%;" :lazy-load="true" @click="clickitemhref(item.bannerimghref)"></image>
							<!-- 右侧子分类标题 -->
							<view class="glance-shop-classify-right-item-titel">{{ item.subtitel }}</view>
							<!-- 右侧子分类项目图文 -->
							<view class="glance-shop-classify-right-item-subitems">
								<view v-for="(subitem,k) in item.subitem" :key='k' style="width:33.33%;">
									<image :src="subitem.itemimgsrc" style="height: 100px; width:100%;" @click="clickitemhref(subitem.itemimghref)" :lazy-load="true"></image>
									<view class="glance-shop-classify-right-item-subtitel">{{ subitem.itemtitel }}</view>
								</view>
							</view>
						</view>
					</view>
				</view>
			</scroll-view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				// 滚动区域高度
				scrollheight:750,
				// 活动的左侧主分类
				activemaintitel:'',
				// 滚动到区域内的指定元素
				scrollintoid:'',
				// 主分类
				maintitels:[],
				// 子项目
				subitems:[],
				data:[]
			}
		},
		onLoad:function(){
			// 通过网络获取json格式数据 这里是示例数据：
			this.data = [
							{
								'maintitel':'居家生活',
								'bannerimgsrc':'../../static/5.png',
								'bannerimghref':'点击了推荐专区',
								'subtitel':'季末热卖',
								'itemimgsrc':'../../static/1.png',
								'itemtitel':'羽绒厚被',
								'itemimghref':'点击了羽绒厚被'
								},
								{
								'maintitel':'服饰鞋包',
								'bannerimgsrc':'../../static/1.png',
								'bannerimghref':'点击了服饰鞋包广告',
								'subtitel':'当季热销',
								'itemimgsrc':'../../static/1.png',
								'itemtitel':'毛衫围巾',
								'itemimghref':'点击了毛衫围巾'
								},
								{
								'maintitel':'服饰鞋包',
								'bannerimgsrc':'../../static/1.png',
								'bannerimghref':'点击了服饰鞋包广告',
								'subtitel':'当季热销',
								'itemimgsrc':'../../static/1.png',
								'itemtitel':'毛衫围巾',
								'itemimghref':'点击了毛衫围巾'
								},
								{
								'maintitel':'服饰鞋包',
								'bannerimgsrc':'../../static/1.png',
								'bannerimghref':'点击了服饰鞋包广告',
								'subtitel':'当季热销',
								'itemimgsrc':'../../static/1.png',
								'itemtitel':'毛衫围巾',
								'itemimghref':'点击了毛衫围巾'
								},
								{
								'maintitel':'男装',
								'bannerimgsrc':'../../static/1.png',
								'bannerimghref':'点击了服饰鞋包广告',
								'subtitel':'当季热销',
								'itemimgsrc':'../../static/1.png',
								'itemtitel':'毛衫围巾',
								'itemimghref':'点击了毛衫围巾'
								},
								{
								'maintitel':'男装',
								'bannerimgsrc':'../../static/1.png',
								'bannerimghref':'点击了服饰鞋包广告',
								'subtitel':'当季热销',
								'itemimgsrc':'../../static/1.png',
								'itemtitel':'毛衫围巾',
								'itemimghref':'点击了毛衫围巾'
								},
								{
								'maintitel':'包包',
								'bannerimgsrc':'../../static/1.png',
								'bannerimghref':'点击了服饰鞋包广告',
								'subtitel':'当季热销',
								'itemimgsrc':'../../static/1.png',
								'itemtitel':'毛衫围巾',
								'itemimghref':'点击了毛衫围巾'
								},
								{
								'maintitel':'包包',
								'bannerimgsrc':'../../static/1.png',
								'bannerimghref':'点击了服饰鞋包广告',
								'subtitel':'当季热销',
								'itemimgsrc':'../../static/1.png',
								'itemtitel':'毛衫围巾',
								'itemimghref':'点击了毛衫围巾'
								},
								{
								'maintitel':'包包',
								'bannerimgsrc':'../../static/1.png',
								'bannerimghref':'点击了服饰鞋包广告',
								'subtitel':'当季热销',
								'itemimgsrc':'../../static/1.png',
								'itemtitel':'毛衫围巾',
								'itemimghref':'点击了毛衫围巾'
								}
								
			]
			// 第一个标题
			var firsttitel = ''
			this.data.forEach((item,index) => {
				// 左侧主标题
				if (this.maintitels.indexOf(item.maintitel) <0) {
					if (firsttitel == ''){
						firsttitel = item.maintitel
					}
					this.maintitels.push(item.maintitel)
				}				
				// 右侧子项目items 
				let isexistsubitem = 0
				let isexistitem = 0
				for (let i = 0; i < this.subitems.length; i++) {
					// 不存在未处理的 则添加
					if (0 || this.subitems[i].mersubtitel == item.maintitel + '-' + item.subtitel){
						// 如果存在 则标记
						isexistsubitem = isexistsubitem + 1
					} 
					
				}
				// 不存在子项目对象数组时 添加
				if (isexistsubitem == 0){
					let subitem={'maintitel':'','mersubtitel':'','subtitel':'','bannerimgsrc':'','bannerimghref':'','subitem':[]}
					
					// 右侧顶端banner
					let isexist = 0
					for (let i = 0; i < this.subitems.length; i++) {
						// 不存在未处理的banner 则添加
						if (0 || this.subitems[i].subtitel == item.maintitel){
							isexist = isexist + 1
						} 
					}
					// console.log(isexist)
					// 不存在广告图 则添加
					if (isexist == 0){
						subitem['bannerimgsrc'] = item.bannerimgsrc
						subitem['bannerimghref'] = item.bannerimghref
						// console.log(this.subbanners)
					}
					subitem['mersubtitel'] = item.maintitel + '-' + item.subtitel
					subitem['maintitel'] = item.maintitel
					subitem['subtitel'] = item.subtitel
					subitem['subitem'] = []
					this.subitems.push(subitem)
					// console.log(this.subbanners)
				}

				// 子项目对象项目 添加
				let objitem={'itemimgsrc':'','itemtitel':'','itemimghref':''}
				objitem['itemimgsrc'] = item.itemimgsrc
				objitem['itemtitel'] = item.itemtitel
				objitem['itemimghref'] = item.itemimghref
				for (let i = 0; i < this.subitems.length; i++) {
					if (this.subitems[i].mersubtitel == item.maintitel + '-' + item.subtitel){
						this.subitems[i].subitem.push(objitem)
					}
				}
			})
			// console.log(this.subitems)
			// 第一个活动得左侧标题
			this.activemaintitel = firsttitel	
			this.clickleftitem(firsttitel,0)
			
			// 获取设备屏幕高度 用于设置滚动条高度
			// 项目中这里从全局变量获得
			try {
				const res = uni.getSystemInfoSync();
				this.scrollheight = res.windowHeight
			} catch (e) {
				this.scrollheight = 750
				// error
			}
		},
		methods:{
			// 点击左侧主分类
			clickleftitem(str,idx){
				// 实现点击左侧项目 右侧滚动至指定分类
				this.activemaintitel = str		
				this.scrollintoid = 'scrollinto-' + idx
				// console.log(this.scrollintoid)
			},
			// 滚动时处理主导航
			scroll:function(e){
				// 循环滚动区域内的元素项 判断top位置 设置主分类切换
				for (let i = 0; i < this.maintitels.length; i++) {
					let s = this.maintitels[i]
// 					let t = uni.createSelectorQuery().select('#');
// 					
// 					t.fields({dataset:true, size: true, rect: true, scrollOffset: true }, data => {
// 							console.log(JSON.stringify(data));
// 						}).exec();

					let g = uni.createSelectorQuery().select('#scrollinto-' + i);
					g.boundingClientRect(data => {
							let top
							top = data.top
							// 判断滚动区域内元素 top距离时 切换主分类
							if (( 0 < top) && (top < this.scrollheight*0.2)){
								// 设置主分类
								this.activemaintitel = s
							}
						}).exec();
				}
			},
			// 点击图片 跳转你要的页面
			clickitemhref(imghref){
				uni.showModal({
					content:'点击了图片，内容：'+imghref,
				})
			}
		}
	}
</script>

<style>
	.glance-shop-classify{
	width: 100%;
	background-color: #ffffff;
	}
	
	.glance-shop-classify-left{
		float: left;width: 20%;height: 100%; position:fixed;z-index: 100;border-right: #F5F5F5 1px solid;background-color: #ffffff;
	}
	
	.glance-shop-classify-right{
		float: left;width: 20%;height: 100%; position:fixed;z-index: 100;border-right: #F5F5F5 1px solid;background-color: #ffffff;
	}
	
	.glance-shop-classify-left-item{
		padding: 10px 0 15px 0; 
		height: 15px; line-height: 15px;text-align: center; width: 100%; font-size: 0.8rem;display: flex;
		display: -webkit-flex;
		flex-flow: row nowrap;
		align-items: center ;
		justify-content: flex-start;
	}
	
	.glance-shop-classify-right-item{
		/* // width: 95%; */
		padding-top: 10px;
		margin-left: 10px;
		margin-right: 10px;
		display: flex;
		display: -webkit-flex;
		z-index: -1;
		flex-flow: column nowrap;
		align-items: flex-start ;
		justify-content: flex-start;
	}
	
	.glance-shop-classify-right-item-titel{
		height: 25px;font-size: 0.8rem;text-align: left;border-bottom: solid 1px #F5F5F5;margin-bottom: 10px;margin-top: 10px;width: 100%;
	}
	
	.glance-shop-classify-right-item-subitems{
		display: flex; display: -webkit-flex ;flex-flow: row wrap;align-items: flex-start;justify-content: flex-start;width: 100%;
	}
	
	.glance-shop-classify-right-item-subtitel{
		height: 20px;line-height: 20px; font-size: 0.7rem;text-align: center;margin-bottom: 10px;
	}
	
	/* // 单行文本样式 */
	.glance-shop-classify-left-item-activeborder{background-color:  #f40;}
	.glance-shop-classify-left-item-activetxt{-webkit-transform: scale(1.2);transform: scale(1.2);color: #f40;}
</style>
