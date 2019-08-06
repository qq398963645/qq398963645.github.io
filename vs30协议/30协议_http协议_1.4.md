# 30协议-HTTP协议-1.4

新增请求验证取货码的接口

***

**接口使用http，post的方式**

#### 1、同步商品信息
**请求参数：/sync_goodsinfo**

**触发场景：(1)App打开；(2)货道运行信息发生变化（如货道故障）；(3)货道配置信息发生变化（如更改商品价格、更改商品编号）；(4)出货成功；(5)补货；(6)每60分钟**

**特别注意：当出货标记位为1时，不需要返回goodsinfo_list字段**

```
{
    "timestamp": "时间戳",
    "id": "终端编号",
    "protocol_version": "版本号",
	"counter_no": "机柜号",
	"number": "逻辑料道数量",
	"add_goods":"补货标记位",	//1补货，0非补货
	"shipment":"出货标记位",		//1出货，0非出货
    "goodsinfo_list":[
		{
			"chan_no":"1",	//货道序号
			"exist":"是否存在",  //1存在/物理，0不存在/逻辑
			"goods_id":"201024",	//商品编号
			"capacity":10,	//容量
			"stock":5,	//库存容量
			"price":50,	//价格：单位为分
			"chan_type":3,	//货道类型：电机、电磁阀
			"fault_code":9	//故障码
		},
		……
	]
}
```

**返回结果：**

```
{
    "code": 0,
    "msg": "ok",
	"goodsinfo_list":[	//当出货标记位为1时，该字段数据不需要返回
		{
			"goods_id":"201024",	//商品编号
			"name":"王老吉",	//商品名称
			"image":"http://xxxx.jpg",	//商品图片
			"spec":"瓶",	//规格
			"size":"300毫升"		//容量
			"desc":"王老吉，正宗的红罐凉茶，好喝好喝真好喝"	//商品介绍
		},
		……
	]
}
```

#### 2、系统运行信息

**请求参数：/sys_run**

```
{
    "timestamp": "时间戳",
    "id": "终端编号",
    "protocol_version": "版本号",
	"running_state": "售货机运行状态",
	"hardware_state": "售货机硬件状态",
	"notes_state": "纸币器状态",
	"coins_state": "硬币器状态",
	"notes_number": "纸币数量",
	"coins_number": "硬币数量"
}
```

**返回结果：**

```
{
    "code": 0,
    "msg": "ok"
}
```


#### 3、系统配置信息

**请求参数：/sys_conf**

```
{
    "timestamp": "时间戳",
    "id": "终端编号",
    "protocol_version": "版本号",
	"counter_no": "机柜号",
	"config": "售卖配置",
	"light": "照明",
	"light_time": "灯时间",
	"left_room": "左室",
	"right_room": "右室",
	"save_time": "节能时间",
	"cool_temp": "制冷温度",
	"left_temp": "左室仓内实际温度",
	"heat_temp": "加热温度",
	"right_temp": "右室仓内实际温度"
}
```

**返回结果：**

```
{
    "code": 0,
    "msg": "ok"
}
```


#### 4、商品销售信息

**请求参数：/sale**

```
{
    "timestamp": "时间戳",
    "id": "终端编号",
    "protocol_version": "版本号",
	"counter_no": "机柜号",
	"channel_no": "料道序号",
	"goods_code": "商品遍号",
	"price": "售卖金额",
	"seq": "序列号",
	"pay": "支付方式",
	"status": "出货情况",
	"card": "卡号",
	"flow": "流水号"
}
```

**返回结果：**

```
{
    "code": 0,
    "msg": "ok"
}
```

#### 5、商品销售汇总信息

**请求参数：/sale_summary**

```
{
    "timestamp": "时间戳",
    "id": "终端编号",
    "protocol_version": "版本号",
	"total_number": "商品销售总数量",
	"total_price": "商品销售的总金额",
	"cash_number": "现金销售总数量",
	"cash_price": "现金销售总金额",
	"card_number": "一卡通销售总数量",
	"card_price": "一卡通销售总金额",
	"union_number": "银联卡销售总数量",
	"union_price": "银联卡销售总金额",
	"pc_number": "PC正常提货总数量",
	"pc_price": "PC正常提货销售金额",
	"local_alipay_number": "本地支付宝购物总数量",
	"local_alipay_price": "本地支付宝购物销售金额",
	"local_wxpay_number": "本地微信支付总数量",
	"local_wxpay_price": "本地微信支付销售金额",
	"pick_number": "提货码总数量",
	"pick_price": "提货码销售金额",
	"app_score_number": "APP积分总数量",
	"app_score_price": "APP积分销售金额",
	"app_alipay_number": "APP支付宝总数量",
	"app_alipay_price": "APP支付宝销售金额",
	"app_wxpay_number": "APP微信总数量",
	"app_wxpay_price": "APP微信销售金额",
	"weixin_score_number": "公众号积分总数量",
	"weixin_score_price": "公众号积分销售金额",
	"weixin_wxpay_number": "公众号微信总数量",
	"weixin_wxpay_price": "公众号微信销售金额",
	"other_3rd_number1": "其它第三方在线支付1销售数量",
	"other_3rd_price1": "其它第三方在线支付1销售金额",
	"other_3rd_number2": "其它第三方在线支付2销售数量",
	"other_3rd_price2": "其它第三方在线支付2销售金额",
	"other_3rd_number3": "其它第三方在线支付3销售数量",
	"other_3rd_price3": "其它第三方在线支付3销售金额"
}
```

**返回结果：**

```
{
    "code": 0,
    "msg": "ok"
}
```



**返回结果：**

```
{
    "code": 0,
    "msg": "ok"
}
```

#### 6、支付宝及微信二维码申请协议

**请求参数：/qrcode**

```
{
    "timestamp": "时间戳",
    "id": "终端编号",
    "protocol_version": "版本号",
	"pay": "标志位",
	"goods_code": "商品代码",
	"price": "商品价格"
}
```

**返回结果：**

```
{
    "code": 0,
    "msg": "ok",
	"pay": "标志位",
	"qrcode": "二维码字符串"
}
```


#### 7、支付宝及微信二维码申请协议

**请求参数：/qrcodes**

```
{
    "timestamp": "时间戳",
    "id": "终端编号",
    "protocol_version": "版本号",
	"goods_code": "商品代码",
	"price": "商品价格"
}
```

**返回结果：**

```
{
    "code": 0,
    "msg": "ok",
	"wx_qrcode": "微信二维码字符串",
	"ali_qrcode": "支付宝二维码字符串"
}
```

#### 8、获取机器信息

**请求参数：/info**

```
{
    "timestamp": "时间戳",
    "id": "终端编号",
    "protocol_version": "版本号",
}
```

**返回结果：**

```
{
    "code": 0,
    "msg": "ok",
	"data": {
	    "name" : "机器名称",
	    "address" : "机器地址",
	    "mid" : "4位机器编号",
	    "baidu_lbs" : { // 百度地图坐标
	        "latitude" : 0.0, // 纬度
	        "longitude" : 0.0 // 经度
	    },
	    "qq_lbs" : { // 腾讯地图坐标
	        "latitude" : 0.0, // 纬度
	        "longitude" : 0.0 // 经度
	    }
	}
}
```

#### 9、h5获取微信支付信息

**请求参数：/order/precreate**

```
{
    "timestamp": "14位的时间戳",
    "id": "终端的编号",
    "protocol_version": "协议的版本号",
    "goods_id" : "商品的编号",
    "pay" : "支付方式", // wxpay或alipay
    "openid" : "微信openid" // 当pay=wxpay才有这个字段
}
```

**返回结果：**

```
{
    "code": 0,
    "msg": "ok",
    "order_pay_wx_info":{ // pay=wxpay才返回这个字段
        "appId" ： "wx2421b1c4370ec43b", // 公众号名称，由商户传入     
        "timeStamp"：" 1395712654",  // 时间戳，自1970年以来的秒数     
        "nonceStr" ： "随机串",
        "package" ： "prepay_id=u802345jgfjsdfgsdg888",     
        "signType" ： "签名方式",
        "paySign" ： "签名" 
    },
    "order_pay_alipay_info":{ // pay=alipay才返回这个字段
        "alipayurl"="" //支付宝支付链接
    }
}
```

#### 10、h5广告以及商品信息

**请求参数：/goods/info**

```
{
    "timestamp": "14位的时间戳",
    "id": "终端的编号",
    "protocol_version": "协议的版本号",
    "goods_id" : "商品的编号"
}
```

**返回结果：**

```
{
    "code": 0,
    "msg": "ok",
   "goods_info":{
        "name":"商品的名称",
        "price":"商品的价格",
        "image":"商品的图片"
        //后续还可能添加字段        
    }
}
```

#### 11、验证取货码

**请求参数：/pickcode**

```
{
    "timestamp": "14位的时间戳",
    "id": "终端的编号",
    "protocol_version": "协议的版本号",
    "pick_code" : "取货码"
}
```

**返回结果：**

```
{
    "code": 0,
    "msg": "ok"
}
```

#### 12、商品搜索
**请求参数：/goods/search**

```
{
    "timestamp": "14位的时间戳",
    "id": "终端的编号",
    "protocol_version": "协议的版本号",
    "keyword" : "搜索关键词"//首字母、全拼、中文
}
```

**返回结果：**

```
{
    "code": 0,
    "msg": "ok",
    "goodsinfo_list":[
        {
            "goods_id":"201024",    //商品编号
            "name":"王老吉",   //商品名称
            "image":"http://xxxx.jpg",  //商品图片
            "price":150 //商品价格
        },
        ……
    ]
}
```
