### 1、获取当前注册人数 GetUserCount
<big><pre>
请求方式：    POST
请求参数：    无
返回：       JSON
URL 示例：   http://localhost/Statistics/GetUserCount
JSON 示例：
{
    "status":0,
    "description":"获取成功",
    "count":100
}
</pre></big>

### 2、获取当前注册商铺数 GetShopCount
<big><pre>
请求方式：    POST
请求参数：    type: int    /\* 商铺类型，可选，不传表示获取所有
                          \*/ 0~3 同 [Shop Model](Shop.md#1shop-model) 中的 type
                          \*/ 10~13 同 [Report Model](Admin.md#1report-model) 中的 objectType
返回：       JSON
URL 示例：   http://localhost/Statistics/GetShopCount
JSON 示例：
{
    "status":0,
    "description":"获取成功",
    "count":100
}
</pre></big>

### 3、获取商店订单数据 GetOrderStatistics
<big><pre>
请求方式：    POST
请求参数：    dateStart: String   // 起始日期（含），可选，yyyy-MM-dd
             dateEnd: String     // 结束日期（不含），可选，yyyy-MM-dd
返回：       JSON
URL 示例：   http://localhost/Statistics/GetOrderStatistics
JSON 示例：
{
    "status":0,
    "description":"获取成功",
    "result":{
        "count":100,             // 总订单数
        "amount":100.0,          // 总订单额
        "dates":[
            String               // 日期
        ],
        "counts":[
            long                 // 对应日期的订单数
        ],
        "amounts":[
            float                // 对应日期的订单额
        ]
    }
}
</pre></big>

### 4、获取市场交易数据 GetTradingStatistics
<big><pre>
请求方式：    POST
请求参数：    dateStart: String   // 起始日期（含），可选，yyyy-MM-dd
             dateEnd: String     // 结束日期（不含），可选，yyyy-MM-dd
返回：       JSON
URL 示例：   http://localhost/Statistics/GetTradingStatistics
JSON 示例：
{
    "status":0,
    "description":"获取成功",
    "result":{
        "count":100,             // 总交易数
        "amount":100.0,          // 总交易额
        "dates":[
            String               // 日期
        ],
        "counts":[
            long                 // 对应日期的交易数
        ],
        "amounts":[
            float                // 对应日期的交易额
        ]
    }
}
</pre></big>

### 5、获取APP活跃用户数据 GetActiveUserStatistics
<big><pre>
请求方式：    POST
请求参数：    dateStart: String   // 起始日期（含），可选，yyyy-MM-dd
             dateEnd: String     // 结束日期（不含），可选，yyyy-MM-dd
返回：       JSON
URL 示例：   http://localhost/Statistics/GetTradingStatistics
JSON 示例：
{
    "status":0,
    "description":"获取成功",
    "result":{
        "dates":[
            String               // 日期
        ],
        "counts":[
            long                 // 对应日期的活跃用户数
        ]
    }
}
</pre></big>
