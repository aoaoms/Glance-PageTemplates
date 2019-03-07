<!-- glance 店铺分类 -->
<template name="glanceShopClassify">
	<view class="glance-shop-classify">
		<!-- 顶部显示搜索 -->
		
		<!-- 左侧列表占位 -->
		<view style=" float: left;width: 20%;height: 100%; position:fixed;z-index: 100;border-right: #F5F5F5 1px solid;background-color: #ffffff;">
			<!-- 左侧主分类列表 -->
			<view v-for="item in maintitels" :key='index'>
				<!-- 左侧分类项目 -->
				<view class="glance-shop-classify-left-item" style="" @click="clickleftitem(maintitels[index])"  >
				<view style="height: 15px;width: 3%;background-color: #ffffff;" :style="{'background-color':[activemaintitel == maintitels[index] ? '#f40':'#ffffff']}"></view>
				<view style="text-align: center;line-height: 15px;width: 93%;font-size: 0.8rem; " :class="[activemaintitel == maintitels[index] ? 'glance-shop-classify-left-item-activetxt':'']"> {{ maintitels[index] }}</view>
				</view>
			</view>
		</view>
		<!-- 右侧列表 -->
		<view style="float: right; width: 80%;" v-if="activemaintitel">
			<view style="width: 98%;text-align: center;">
				<!-- 右侧顶部广告图 -->
				<view style="margin-top: 10px; background-color: #ffffff;width: 100%;z-index: 10;">
					<image :src="activebanner.src" mode="scaleToFill" @error="imgerr" style="height: 120px;width: 90%;" @click="clickitemhref(activebanner.imghref)"></image>
				</view>
				<!-- 左侧主分类列表 -->
				<scroll-view scroll-y= "true" scroll-left="0" :scroll-top="scrollTop" scroll-with-animation="true" style="background-color: #ffffff;">
					<view class="glance-shop-classify-right-item">
						<view v-for="(item,index) in activesubitems" :key='index' style="width: 95%;">
							<!-- 右侧子分类标题 -->
							<view style="height: 25px;font-size: 0.8rem;text-align: left;border-bottom: solid 1px #F5F5F5;margin-bottom: 20px;">{{ item.subtitel }}</view>
							<!-- 右侧子分类项目图文 -->
							<view style="display: flex; display: -webkit-flex;	flex-flow: row wrap;align-items: flex-start;justify-content: flex-start;" >
							<view v-for="(subitem,k) in item.subitem" :key='k' style="width:33.33%;">
								<image :src="subitem.itemimgsrc" style="height: 100px; width:100%;" @click="clickitemhref(subitem.itemimghref)" lazy-load="true"></image>
								<view style="height: 20px;line-height: 20px; font-size: 0.7rem;text-align: center;margin-bottom: 20px;">{{ subitem.itemtitel }}</view>
							</view>
							</view>
						</view>
					</view>
				</scroll-view>
			</view>
		</view>
	</view>
</template>

<script>
	var _this
	export default {
		data() {
			return {
				activemaintitel:'',
				activebanner:{'src':'','imghref':''},
				maintitels:[],
				subtitels:[],
				subbanners:[],
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
								'maintitel':'居家生活',
								'bannerimgsrc':'../../static/5.png',
								'bannerimghref':'点击了推荐专区',
								'subtitel':'季末热卖',
								'itemimgsrc':'../../static/1.png',
								'itemtitel':'磨毛件套',
								'itemimghref':'点击了磨毛件套'
								}
								,
								{
								'maintitel':'居家生活',
								'bannerimgsrc':'../../static/5.png',
								'bannerimghref':'点击了推荐专区',
								'subtitel':'家纺床品',
								'itemimgsrc':'../../static/1.png',
								'itemtitel':'毛巾浴巾',
								'itemimghref':'点击了毛巾浴巾'
								},
								{
								'maintitel':'居家生活',
								'bannerimgsrc':'../../static/5.png',
								'bannerimghref':'点击了推荐专区',
								'subtitel':'家纺床品',
								'itemimgsrc':'../../static/1.png',
								'itemtitel':'床品件套',
								'itemimghref':'点击了床品件套'
								},
								{
								'maintitel':'居家生活',
								'bannerimgsrc':'../../static/1.png',
								'bannerimghref':'点击了推荐专区',
								'subtitel':'家纺床品',
								'itemimgsrc':'../../static/1.png',
								'itemtitel':'布艺软装',
								'itemimghref':'点击了布艺软装'
								},
								{
								'maintitel':'服饰鞋包',
								'bannerimgsrc':'../../static/1.png',
								'bannerimghref':'点击了服饰鞋包广告',
								'subtitel':'当季热销',
								'itemimgsrc':'../../static/1.png',
								'itemtitel':'毛呢羽绒',
								'itemimghref':'点击了毛呢羽绒'
								},
								{
								'maintitel':'服饰鞋包',
								'bannerimgsrc':'../../static/1.png',
								'bannerimghref':'点击了服饰鞋包广告',
								'subtitel':'当季热销',
								'itemimgsrc':'../../static/1.png',
								'itemtitel':'新春出行',
								'itemimghref':'点击了新春出行'
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
								'itemtitel':'春季流行',
								'itemimghref':'点击了春季流行'
								},
								{
								'maintitel':'服饰鞋包',
								'bannerimgsrc':'../../static/1.png',
								'bannerimghref':'点击了服饰鞋包广告',
								'subtitel':'男装',
								'itemimgsrc':'../../static/1.png',
								'itemtitel':'男式外套',
								'itemimghref':'点击了男式外套'
								},
								{
								'maintitel':'服饰鞋包',
								'bannerimgsrc':'../../static/1.png',
								'bannerimghref':'点击了服饰鞋包广告',
								'subtitel':'当季热销',
								'itemimgsrc':'../../static/1.png',
								'itemtitel':'毛呢羽绒',
								'itemimghref':'点击了毛呢羽绒'
								},
								{
								'maintitel':'服饰鞋包',
								'bannerimgsrc':'../../static/1.png',
								'bannerimghref':'点击了服饰鞋包广告',
								'subtitel':'当季热销',
								'itemimgsrc':'../../static/1.png',
								'itemtitel':'新春出行',
								'itemimghref':'点击了新春出行'
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
								'itemtitel':'春季流行',
								'itemimghref':'点击了春季流行'
								},
								{
								'maintitel':'服饰鞋包',
								'bannerimgsrc':'../../static/1.png',
								'bannerimghref':'点击了服饰鞋包广告',
								'subtitel':'男装',
								'itemimgsrc':'../../static/1.png',
								'itemtitel':'男式外套',
								'itemimghref':'点击了男式外套'
								},
								{
								'maintitel':'服饰鞋包',
								'bannerimgsrc':'../../static/1.png',
								'bannerimghref':'点击了服饰鞋包广告',
								'subtitel':'当季热销',
								'itemimgsrc':'../../static/1.png',
								'itemtitel':'新春出行',
								'itemimghref':'点击了新春出行'
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
								'itemtitel':'春季流行',
								'itemimghref':'点击了春季流行'
								},
								{
								'maintitel':'服饰鞋包',
								'bannerimgsrc':'../../static/1.png',
								'bannerimghref':'点击了服饰鞋包广告',
								'subtitel':'男装',
								'itemimgsrc':'../../static/1.png',
								'itemtitel':'男式外套',
								'itemimghref':'点击了男式外套'
								},
								{
								'maintitel':'服饰鞋包',
								'bannerimgsrc':'../../static/1.png',
								'bannerimghref':'点击了服饰鞋包广告',
								'subtitel':'当季热销',
								'itemimgsrc':'../../static/1.png',
								'itemtitel':'新春出行',
								'itemimghref':'点击了新春出行'
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
								'itemtitel':'春季流行',
								'itemimghref':'点击了春季流行'
								},
								{
								'maintitel':'服饰鞋包',
								'bannerimgsrc':'../../static/1.png',
								'bannerimghref':'点击了服饰鞋包广告',
								'subtitel':'男装',
								'itemimgsrc':'../../static/1.png',
								'itemtitel':'男式外套',
								'itemimghref':'点击了男式外套'
								},
								{
								'maintitel':'服饰鞋包',
								'bannerimgsrc':'../../static/1.png',
								'bannerimghref':'点击了服饰鞋包广告',
								'subtitel':'当季热销',
								'itemimgsrc':'../../static/1.png',
								'itemtitel':'新春出行',
								'itemimghref':'点击了新春出行'
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
								'itemtitel':'春季流行',
								'itemimghref':'点击了春季流行'
								},
								{
								'maintitel':'服饰鞋包',
								'bannerimgsrc':'../../static/1.png',
								'bannerimghref':'点击了服饰鞋包广告',
								'subtitel':'男装',
								'itemimgsrc':'../../static/1.png',
								'itemtitel':'男式外套',
								'itemimghref':'点击了男式外套'
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
				// 右侧子标题
				if (this.subtitels.indexOf(item.maintitel+'-'+item.subtitel) <0) {
					this.subtitels.push(item.maintitel+'-'+item.subtitel)
				}
				// 右侧顶端banner
				let isexist = 0
				for (let i = 0; i < this.subbanners.length; i++) {
					// 不存在未处理的banner 则添加
					if (0 || this.subbanners[i].maintitel == item.maintitel){
						isexist = isexist + 1
					} 
				}
				// console.log(isexist)
				// 不存在 添加
				if (isexist == 0){
					let obj={'bannerimgsrc':'','bannerimghref':''},subbanner={'maintitel':'','subbanner':[]}
					obj['bannerimgsrc'] = item.bannerimgsrc
					obj['bannerimghref'] = item.bannerimghref
					
					subbanner['maintitel'] = item.maintitel
					subbanner['subbanner'] = obj
					this.subbanners.push(subbanner)
					// console.log(this.subbanners)
				}
				// 右侧子项目items 
				let isexistsubitem = 0
				let isexistitem = 0
				for (let i = 0; i < this.subitems.length; i++) {
					// 不存在未处理的 则添加
					if (0 || this.subitems[i].subtitel == item.maintitel+'-'+item.subtitel){
						// 如果存在 则标记
						isexistsubitem = isexistsubitem + 1
					} 
					
				}
				// 不存在子项目对象数组时 添加
				if (isexistsubitem == 0){
					let subitem={'subtitel':'','subitem':[]}
					
					subitem['subtitel'] = item.maintitel+'-'+item.subtitel
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
					if (this.subitems[i].subtitel == item.maintitel+'-'+item.subtitel){
						this.subitems[i].subitem.push(objitem)
					}
				}
			})
			// console.log(this.subbanners)
			// console.log(this.subitems)
			// 第一个活动得左侧标题
			this.clickleftitem(firsttitel)
		},
		computed:{
			// 通过左侧活动标题内容过滤获得右侧获得项目
			activesubitems(){
				var str = this.activemaintitel
				var obj = this.subitems
				return obj.filter(item => item.subtitel.indexOf(str) > -1 )
			},
			// 格式化子标题 A-B 留B 官方不支持啊~
			fmsubtitel(){
				return function(str) {
					// console.log(str)
					let idx = str.indexOf('-')
					return str.substr(idx+1,100)
				}
			}
		},
		methods:{
			clickleftitem(str){
				// 实现点击左侧项目 更新数据
				this.activemaintitel = str
				// 刷新 当前活动得广告图属性
				for (var i = 0; i < this.subbanners.length; i++) {
					if (this.activemaintitel == this.subbanners[i].maintitel){
						this.activebanner.imghref = this.subbanners[i].subbanner.bannerimghref
						this.activebanner.src = this.subbanners[i].subbanner.bannerimgsrc
					}
				}
				// console.log(this.activebanner)
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

<style lang="scss">
.glance-shop-classify{
	width: 100%;
	background-color: #ffffff;
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
	width: 95%;
	margin-top: 10px;
	margin-left: 15px;
	display: flex;
	display: -webkit-flex;
	z-index: -1;
	flex-flow: column nowrap;
	align-items: flex-start ;
	justify-content: flex-start;
}
// 单行文本样式
.glance-shop-classify-left-item-activeborder{background-color:  #f40;}
.glance-shop-classify-left-item-activetxt{-webkit-transform: scale(1.2);transform: scale(1.2);color: #f40;}
</style>
