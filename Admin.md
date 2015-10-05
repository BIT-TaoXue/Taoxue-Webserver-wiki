## 一、Model 部分

### 1、Report model
<big><pre>
Report // 举报（审核）信息
{
    /\* DB 字段 \*/
    reportId: String            // 举报 ID
    objectId: String            // 被举报事物 ID
    objectType: int             /* 被举报事物类型
                                 \* 0 为商品，1 为树洞
                                 \* 10 为审核中的商铺，11 为审核失败的商铺
                                 \* 12 为隐藏的商铺，13 为强制隐藏的商铺
                                 \*/
    userId: String              // 举报者 ID
    content: String             // 举报理由或内容
    reportTime: Timestamp       // 举报时间
 
    /\* 附加属性 \*/
    reporter: User              // 举报者，参照 [User Model](Home.md#5user-model)
    item: Item                  // 被举报商品，参照 [Item Model](Home.md#1item-model)
    talk: Talk                  // 被举报树洞，参照 [Talk Model](Talk.md#1talk-model)
    shop: Shop                  // 审核中、审核失败、隐藏或强制隐藏的商铺，参照 [Shop Model](Shop.md#1shop-model)
}
</pre></big>

获取商品和树洞详情，调用 `/Market/GetItemDetails` 和 `/Talk/GetTalkById`
获取商铺详情，调用 `/Shop/GetMyShop`

### 2、Advice Model
<big><pre>
Advice // 建议
{
    /\* DB 字段 \*/
    adviceId: String            // 建议 ID
    content: String             // 内容
    time: Timestamp             // 时间
}
</pre></big>

## 二、接口部分

### 1、管理员登录 Login
<big><pre>
请求方式：    POST
请求参数：    account: String    // 账号
             password: String	// 密码
返回：       JSON
URL 示例：   http://localhost/Admin/Login
JSON 示例：
{
    "status":0,
    "description":"获取成功",
    "user":{
        User                    // 参照 [User Model](Home.md#5user-model)
    }
}
</pre></big>

### 2、获取正在审核中的商品 GetReviewingItems
<big><pre>
请求方式：    POST
请求参数：    无
返回：       JSON
URL 示例：   http://localhost/Admin/GetReviewingItems
JSON 示例：
{
    "status":0,
    "description":"获取成功",
    "reports":[{
        Report                  // 参照 [Report Model](#1report-model)，已加载 reporter 和 item
    }]
}
</pre></big>

### 3、获取正在审核中的树洞 GetReviewingTalks
<big><pre>
请求方式：    POST
请求参数：    无
返回：       JSON
URL 示例：   http://localhost/Admin/GetReviewingTalks
JSON 示例：
{
    "status":0,
    "description":"获取成功",
    "reports":[{
        Report                  // 参照 [Report Model](#1report-model)，已加载 reporter 和 talk
    }]
}
</pre></big>

### 4、获取正在审核中的商铺 GetReviewingShops
<big><pre>
请求方式：    POST
请求参数：    无
返回：       JSON
URL 示例：   http://localhost/Admin/GetReviewingShops
JSON 示例：
{
    "status":0,
    "description":"获取成功",
    "reports":[{
        Report                  // 参照 [Report Model](#1report-model)，已加载 reporter 和 shop
    }]
}
</pre></big>

### 5、某物通过审核 ApproveObject
<big><pre>
请求方式：    POST
请求参数：    objectId: String   // 对象 ID
返回：       JSON
URL 示例：   http://localhost/Admin/ApproveObject
JSON 示例：
{
    "status":0,
    "description":"通过审核成功"
}
</pre></big>

### 6、某物未通过审核 DisapproveObject
<big><pre>
请求方式：    POST
请求参数：    objectId: String   // 对象 ID
             content: String    // 理由，可选
返回：       JSON
URL 示例：   http://localhost/Admin/DisapproveObject
JSON 示例：
{
    "status":0,
    "description":"删除成功"
}
</pre></big>

### 7、删除某条评论（级联） DeleteComment
<big><pre>
请求方式：    POST
请求参数：    commentId: String  // 评论 ID
返回：       JSON
URL 示例：   http://localhost/Admin/DeleteComment
JSON 示例：
{
    "status":0,
    "description":"删除成功"
}
</pre></big>

### 8、获取所有建议 GetAdvices
<big><pre>
请求方式：    POST
请求参数：    无
返回：       JSON
URL 示例：   http://localhost/Admin/GetAdvices
JSON 示例：
{
    "status":0,
    "description":"获取成功",
    "advices":[{
        Advice                  // 参照 [Advice Model](#2advice-model)
    }]
}
</pre></big>

### 9、删除某条建议 DeleteAdvice
<big><pre>
请求方式：    POST
请求参数：    adviceId: String   // 建议 ID
返回：       JSON
URL 示例：   http://localhost/Admin/DeleteAdvice
JSON 示例：
{
    "status":0,
    "description":"删除成功"
}
</pre></big>

### 10、获取所有商铺 GetAllShops
<big><pre>
请求方式：    POST
请求参数：    type: int          // 商铺类型
返回：       JSON
URL 示例：   http://localhost/Admin/GetAllShops
JSON 示例：
{
    "status":0,
    "description":"获取成功",
    "shops":[{
        Shop                    // 参照 [Shop Model](Shop.md#1shop-model)，已加载 reviewType
    }]
}
</pre></big>

### 11、强制隐藏商铺 HideShop
<big><pre>
请求方式：    POST
请求参数：    userId: String     // 用户 ID
             shopId: String     // 商铺 ID
返回：       JSON
URL 示例：   http://localhost/Admin/HideShop
JSON 示例：
{
    "status":0,
    "description":"隐藏成功"
}
</pre></big>

### 12、显示商铺 ShowShop
<big><pre>
请求方式：    POST
请求参数：    userId: String     // 用户 ID
             shopId: String     // 商铺 ID
返回：       JSON
URL 示例：   http://localhost/Admin/ShowShop
JSON 示例：
{
    "status":0,
    "description":"显示成功"
}
</pre></big>

### 13、交换商铺优先级 ExchangeShopPriority
<big><pre>
请求方式：    POST
请求参数：    shopId: String     // 商铺 ID 1
             objectId: String   // 商铺 ID 2
返回：       JSON
URL 示例：   http://localhost/Admin/ExchangeShopPriority
JSON 示例：
{
    "status":0,
    "description":"交换成功"
}
</pre></big>

### 14、退出登录 Logout
<big><pre>
请求方式：    POST
请求参数：    userId: String     // 用户 ID
返回：       JSON
URL 示例：   http://localhost/Admin/DeleteAdvice
JSON 示例：
{
    "status":0,
    "description":"退出登录成功"
}
</pre></big>
