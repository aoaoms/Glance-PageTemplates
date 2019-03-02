##组件名称：
>glance 店铺购物车-小程序模板页 `glanceShopCart`
>
>单页文件，装载数据后 直接用吧

##组件功能：

* 商品购物车页面
* 结构化接口数据
* 交互方法：点击图片、商品名称、商品属性后触发click方法，可用于点击跳转至商品详情页
* 点击营销活动 跳转至营销活动

##使用场景：
*  店铺购物车页面
*  商品推荐部分需要自己完善~

##版本
<table border=”1”>
<tr>
<td>版本号</td>
<td>更新内容</td>
<td>待处理<td>
</tr>
tr>
<td>v0.9</td>
<td>
1、 模板样式微调
2、 添加滑动删除未操作时，自动归位功能（使用的scroll-left属性值结合屏幕滑动事件处理）
参见 scrollhoming 、 scrollhomed 方法
</td>
<td>样式规范与精简<td>
</tr>
</table>

###说明：
>组件使用 `HBuilderX` 开发，仅在 `微信小程序` 内测试通过

##组件属性：

<table border=”1”>
<tr>
<td>cart</td>
<td>Array</td>
<td> 页面中onload 事件里面有示例数据 请查看
</td>
<td>null</td>
<td>载入的分类结构化数据信息</td>
</tr>
</table>

> `cart` 数据格式及属性说明
<table border=”1”>
<tr>
<td>属性</td>
<td>值类型</td>
<td>值示例</td>
<td>默认值</td>
<td>备注</td>
</tr>
<tr>
<td>groupkey</td>
<td>String</td>	
<td>团购更多优惠</td>
<td>无</td>
<td>购物车内商品的分组值 用于商品归类或一组商品可用的营销活动</td>
</tr>
<tr>
<td>items</td>
<td>array</td>
<td>商品集合</td>
<td>无</td>
<td>购物车内分组的商品属性集</td>
</tr>
</table>

> `item` 数据格式及属性说明
<table border=”1”>
<tr>
<td>属性</td>
<td>值类型</td>
<td>值示例</td>
<td>默认值</td>
<td>备注</td>
</tr>
<tr>
<td>id</td>
<td>Number</td>	
<td>商品ID</td>
<td>无</td>
<td>商品id</td>
</tr>
<tr>
<td>name</td>
<td>String</td>
<td>商品名称</td>
<td>无</td>
<td>商品名称</td>
</tr>
<tr>
<td>imgsrc</td>
<td>String</td>	
<td>商品图片地址</td>
<td>无</td>
<td>商品图片地址</td>
</tr>
<tr>
<td>attributes</td>
<td>String</td>
<td>商品属性</td>
<td>无</td>
<td>商品属性</td>
</tr>
<tr>
<td>quantity</td>
<td>Number</td>	
<td>商品数量</td>
<td>无</td>
<td>商品数量</td>
</tr>
<tr>
<td>price</td>
<td>String</td>
<td>商品结算单价</td>
<td>无</td>
<td>商品结算单价</td>
</tr>
</table>

#使用步骤：
>单页面模板，装载数据后，直接用吧~
>
>示例效果参见图片

##说明
> 可自行改样式
> 
> 如果觉得好 就给个赞吧，辛苦付出 劳烦点个赞 人人为我 我为人人

##部分代码
~~~~~
// 加数量
plusitem(itemid){
    for (let i = 0; i < this.cart.length; i++) {
        for (let k = 0; k < this.cart[i].items.length; k++) {
            // 这里需要进行超卖控制 商品可售卖的数量 这里面示例可售卖100
            if ((this.cart[i].items[k].id == itemid) && (this.cart[i].items[k].quantity < 100)){
                // 更新item数量
                this.cart[i].items[k].quantity = this.cart[i].items[k].quantity +1
                // 加数量时未勾选则 勾选
                if (this.cart[i].items[k].id < 0){
                    this.cart[i].items[k].id = this._selected(this.cart[i].items[k].id)
                }
                // 勾选状态下更新数量和金额
                if (this.isselected(this.cart[i].items[k].id)){
                    // 更新总数量
                    this.updatecntitems(1)
                    // 更新总金额
                    this.updatetotalamt(this.cart[i].items[k].price)
                }
                return
            }
        }
    }
},

// 点击商品href
clickitemhref(str){
    uni.showModal({
        content: '点击了商品链接' + str
    })
},
// 点击了营销活动
clickgroupkey(str){
    let mehref = this.getgroupkeyhref(str)
    uni.showModal({
        content:'点击了营销活动'+ mehref
    })
},
// 更新合计金额
updatetotalamt(amt){
    this.totalamount = this.totalamount + amt
    this.totalamount = this.fmamount(this.totalamount)
    
},
// 更新合计数量
updatecntitems(cnt){
    this.cntitems = this.cntitems + 1
},
// 格式化金额
fmamount(amt){
    return Math.round(amt*100)/100
},
// 不勾选
_unselected(id){
    return - Math.abs(id)
},
// 勾选
_selected(id){
    return Math.abs(id)
},
// 是否勾选
isselected(id){
    return id > 0
},
// 获取营销页面链接
getgroupkeyhref(str){
    // 这里通过营销活动名称 获取营销活动页面 需要自己实现
    return '营销活动页面'
},
// 生成订单
createorder(){
    // 合计金额大于0 创建订单
    if (this.totalamount == 0){
        uni.showModal({
            content: '请选择下单的商品！'
        })
    }else{
        // 1、处理购物车内已选择的订单生成商品
        for (let i = 0; i < this.cart.length; i++) {
            for (let k = 0; k < this.cart[i].items.length; k++) {
                // item id 大于0 的是勾选的
                if (this.cart[i].items > 0){
                    //这里的item 是下单的
                }
            }
        }
        // 2、生成订单成功后 删除购物车内已生成订单的商品
    }
}
~~~~~

##特别说明
>商品列表的筛选和删除 使用商品id 值得变化控制：
>* 商品未勾选时：商品id 等于其负值
>* 删除商品时：商品id 等于-99-id
>
>因此，可以通过判断id值-99-id 时 获取购物车内已删除得商品;通过判断id值为正时，获取已勾选得商品

><font color='#FF0000' >本人水平有限&emsp;努力提升中...  </font> :blush:

如有问题，请留言；代码有了，想要的效果可以改到自己满意的为止~ 