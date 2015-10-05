### 1、获取热销商品统计 GetHotItems
<big><pre>
请求方式：    POST
请求参数：    shopId: String      // 商铺 ID
返回：       JSON
URL 示例：   http://localhost/Shop/Statistics/GetHotItems
JSON 示例：
{
    "status":0,
    "description":"获取成功",
    "result":{
        "name":[
            String               // 商品名称
        ],
        "value":[
            long                 // 销售量
        ]
    }
}
</pre></big>

### 2、获取订单数统计 GetOrderStatistics
<big><pre>
请求方式：    POST
请求参数：    shopId: String      // 商铺 ID
             dateStart: String   // 起始日期（含），可选，yyyy-MM-dd
             dateEnd: String     // 结束日期（不含），可选，yyyy-MM-dd
返回：       JSON
URL 示例：   http://localhost/Shop/Statistics/GetOrderStatistics
JSON 示例：
{
    "status":0,
    "description":"获取成功",
    "result":{
        "name":[
            String               // 日期
        ],
        "value":[
            long                 // 对应日期的订单数
        ]
    }
}
</pre></big>

### 3、获取销售额统计 GetSaleStatistics
<big><pre>
请求方式：    POST
请求参数：    shopId: String      // 商铺 ID
             dateStart: String   // 起始日期（含），可选，yyyy-MM-dd
             dateEnd: String     // 结束日期（不含），可选，yyyy-MM-dd
返回：       JSON
URL 示例：   http://localhost/Shop/Statistics/GetSaleStatistics
JSON 示例：
{
    "status":0,
    "description":"获取成功",
    "result":{
        "name":[
            String               // 日期
        ],
        "value":[
            float                // 对应日期的销售额
        ]
    }
}
</pre></big>
