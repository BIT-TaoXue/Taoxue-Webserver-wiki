### 0、note
**网页端上传图片的说明**
因为上传图片需要经过裁剪，裁剪后无法直接以 File 格式上传，所以采用字符串格式上传。
**格式说明**
每一张图片 name 均为 `dataUrls`，value 格式为 `data:image/*;base64,**`，`*` 处可以是 `png`、`jpeg`、`bmp`、`gif`，`**` 处为图片数据的 Base64 编码，上传前用 `encodeURIComponent` 函数对 value 进行 URI 编码。

## 一、Model 部分

### 1、Shop Model
<big><pre>
Shop // 商铺
{
    /\* DB 字段 \*/
    shopId: String              // 商铺 ID
    category: String            // 商铺分类
    name: String                // 商铺名称
    address: String             // 地址
    introduction: String        // 简介
    registerTime: Timestamp     // 注册时间
    logo: String                // 图标，相对路径
    background: String          // 背景图片，相对路径，可选
    ownerId: String             // 卖家 ID
    bulletin: String            // 公告
    speed: int                  // 送货速度，比如 30 表示 30 分钟送到
    timePeriods: String         /\* 营业时间段，用分号“;”分隔
                                 \* 格式为“hh:mm-hh:mm;...”
                                 \*/
    type: int                   /\* 商铺类型
                                 \* 0 表示学生商铺，1 表示校内商铺
                                 \* 2 表示校外商铺，3 表示淘学商铺
                                 \*/
    contact: String             // 联系方式
    price: float                // 起送价
    target: String              // 服务对象，用分号“;”分隔
    orderType: int              /\* 订单选项
                                 \* 最低位 0 表示支持预订，1 表示不支持预订
                                 \* 第二位 0 表示接收短信提醒，1 表示不接收
                                 \* 第三位 0 表示支持无线打印，1 表示不支持
                                 \*/
    other: String               // 其他信息，用于审核
    priority: Long              // 优先级，用于排序
 
    /\* 附加属性 \*/
    owner: User                 // 参照 [User Model](Home.md#5user-model)
    classes: [                  // 商品分类数组
        String
    ]
    items: [
        ShopItem                // 参照 [ShopItem Model](#2shopitem-model)
    ]
    reviewType: int             // 审核类型
    ESN： String                // 无线打印机编号
    sellCount: long             // 月销量
}
</pre></big>

### 2、ShopItem Model
<big><pre>
ShopItem // 商铺的商品
{
    /\* DB 字段 \*/
    itemId: String              // 商品 ID
    itemName: String            // 商品名称
    price: float                // 价格
    details: String             // 详情
    clazz: String               // 分类
    shopId: String              // 所属商铺 ID
    status: int                 // 状态，0 表示正常，1 表示已删除，2 表示隐藏
    stock: long                 // 库存，为空表示没有库存限制
 
    /\* 附加属性 \*/
    images: [
        ItemImage               // 参照 [ItemImage Model](Home.md#4itemimage-model)
    ]
    comments: [
        ItemComment             // 参照 [ItemComment Model](Home.md#3itemcomment-model)
    ]
    shop: Shop                  // 参照 [Shop Model](#ishop-model)
    sellCount: long             // 月销量
}
</pre></big>

### 3、Order Model
<big><pre>
Order // 订单
{
    /\* DB 字段 \*/
    orderId: String             // 订单 ID
    time: Timestamp             // 生成时间
    shopId: String              // 商铺 ID
    userId: String              // 买家 ID
    address: String             // 配送地址
    contact: String             // 买家联系方式
    status: int                 /\* 订单状态
                                 \* 最低位 0 表示用户未删除，1 表示用户已删除
                                 \* 第二位 0 表示商家未读，1 表示商家已读
                                 \* 第三位 0 表示商家未打印，1 表示商家已打印
                                 \*/
    note: String                // 备注
 
    /\* 附加属性 \*/
    items: [
        OrderItem               // 参照 [OrderItem Model](#4orderitem-model)
    ]
    totalPrice: float           // 总价
    shop: Shop                  // 参照 [Shop Model](#1shop-model)
    user: User                  // 参照 [User Model](Home.md#5user-model)
}
</pre></big>

### 4、OrderItem Model
<big><pre>
OrderItem // 订单中的商品
{
    /\* DB 字段 \*/
    id: String                  // ID
    orderId: String             // 订单 ID
    itemId: String              // 商品 ID
    price: float                // 商品单价
    quantity: int               // 商品数量
 
    /\* 附加属性 \*/
    item: ShopItem              // 参照 [ShopItem Model](#2shopitem-model)，总是加载
}
</pre></big>

## 二、客户端接口部分

### 1、获取所有商铺 GetShops
<big><pre>
请求方式：    POST
请求参数：    type: int           // 商铺类型，见 [Shop Model](#1shop-model)
             userId: String      // 用户 ID，可选
             <s>location: String    // 位置，可选，格式为"经度,纬度"</s> **已弃用，请用 campus**
             campus: String      // 学校和校区，可选，用“,”分隔，如“北京理工大学,良乡”
             category: String    // 商铺种类，可选
             cntStart: int       // 开始的个数（含），可选，从 0 开始
             cntEnd: int         // 结束的个数（不含），可选，从 0 开始
返回：       JSON
URL 示例：   http://localhost/Shop/GetShops
JSON 示例：
{
    "status":0,
    "description":"获取成功",
    "shops":[{
        Shop                     // 参照 [Shop Model](#1shop-model)，已加载 classes 和 sellCount
    }]
}
</pre></big>

### 2、获取商铺详情 GetShopDetails
<big><pre>
请求方式：    POST
请求参数：    shopId: String      // 商铺 ID
返回：       JSON
URL 示例：   http://localhost/Shop/GetShopDetails
JSON 示例：
{
    "status":0,
    "description":"获取成功",
    "shop":{
        Shop                     // 参照 [Shop Model](#1shop-model)，已加载 classes 和 sellCount
    }
}
</pre></big>

### 3、获取商铺中的商品 GetShopItems
<big><pre>
请求方式：    POST
请求参数：    shopId: String      // 商铺 ID
             clazz: String       // 分类，可选
返回：       JSON
URL 示例：   http://localhost/Shop/GetShopItems
JSON 示例：
{
    "status":0,
    "description":"获取成功",
    "items":[                    // 类型为 Map\<String, List\<ShopItem\>\>
        "分类1":[{
            ShopItem             // 参照 [ShopItem Model](#2shopitem-model)，已加载 images 和 sellCount
        }],
        "分类2":[{
            ShopItem             // 参照 [ShopItem Model](#2shopitem-model)，已加载 images 和 sellCount
        }]
    ]
}
</pre></big>

### 4、获取商铺商品详情 GetShopItemDetails
<big><pre>
请求方式：    POST
请求参数：    itemId: String      // 商品 ID
返回：       JSON
URL 示例：   http://localhost/Shop/GetShopItemDetails
JSON 示例：
{
    "status":0,
    "description":"获取成功",
    "item":{
        ShopItem                 // 参照 [ShopItem Model](#2shopitem-model)，已加载 images 和 sellCount
    }
}
</pre></big>

### 5、获取商铺商品的详细信息 GetItemComments
<big><pre>
请求方式：    POST
请求参数：    itemId: String      // 商品 ID
返回：       JSON
URL 示例：   http://localhost/Shop/GetItemComments
JSON 示例：
{
    "status":0,
    "description":"获取成功",
    "comments":[{
        ItemComment              // 参照[ItemComment Model](Home.md#3itemcomment-model)，已加载 maker
    }]
}
</pre></big>

### 6、评论商铺商品 WriteItemComment
<big><pre>
请求方式：    POST
请求参数：    itemId: String      // 商品 ID
             userId: String      // 用户 ID
             content: String     // 评论内容
             refId: String       // 引用 ID，表示另一条评论，可为空
返回：       JSON
URL 示例：   http://localhost/Shop/WriteItemComment
JSON 示例：
{
    "status":0,
    "description":"评论成功"
}
</pre></big>

### 7、获取我的订单 GetMyOrders
<big><pre>
请求方式：    POST
请求参数：    userId: String      // 用户 ID
             cntStart: int       // 开始的个数（含），可选，从 0 开始
             cntEnd: int         // 结束的个数（不含），可选，从 0 开始
返回：       JSON
URL 示例：   http://localhost/Shop/GetMyOrders
JSON 示例：
{
    "status":0,
    "description":"获取成功",
    "orders":[{
        Order                    // 参照 [Order Model](#3order-model)，已加载 items、totalPrice 和 shop
    }]
}
</pre></big>

### 8、生成订单 CreateOrder
<big><pre>
请求方式：    POST
请求参数：    userId: String      // 用户 ID
             shopId: String      // 商铺 ID
             address: String     // 配送地址
             contact: String     // 买家联系方式
             note: String        // 备注
             itemIds: String[]   // 商品 ID 数组
             quantities: int[]   // 购买数量数组
返回：       JSON
URL 示例：   http://localhost/Shop/CreateOrder
JSON 示例：
{
    "status":0,
    "description":"下单成功"
}
</pre></big>

### 9、获取商铺联系方式 GetShopContact
<big><pre>
请求方式：    POST
请求参数：    shopId: String      // 商铺 ID
返回：       JSON
URL 示例：   http://localhost/Shop/GetShopContact
JSON 示例：
{
    "status":0,
    "description":"获取成功",
    "contact":"10086"
}
</pre></big>

### 10、删除订单 DeleteOrder
<big><pre>
请求方式：    POST
请求参数：    userId: String      // 用户 ID
             orderId: String     // 订单 ID
返回：       JSON
URL 示例：   http://localhost/Shop/DeleteOrder
JSON 示例：
{
    "status":0,
    "description":"删除成功"
}
</pre></big>


##三、网页端接口部分

### 1、获取商铺种类 GetCategories
<big><pre>
请求方式：    POST
请求参数：    type: int           // 商铺类型，见 [Shop Model](#1shop-model)
返回：       JSON
URL 示例：   http://localhost/Shop/GetCategories
JSON 示例：
{
    "status":0,
    "description":"获取成功",
    "categories":[
        String
    ]
}
</pre></big>

### 2、注册商铺 Register
<big><pre>
请求方式：    POST
请求参数：    userId: String          // 用户 ID
             name: String            // 商铺名称
             category: String        // 商铺种类
             address: String         // 地址
             introduction: String    // 简介
             speed: int              // 送货速度，比如 30 表示 30 分钟送到
             timePeriods: String     // 营业时间段，见 [Shop Model](#1shop-model)
             type: int               // 商铺类型，见 [Shop Model](#1shop-model)
             contact: String         // 联系方式
             price: float            // 起送价
             target: String          // 服务对象，可选，用分号“;”分隔
             orderType: int          // 接受订单方式，0 为短信，1 为 POS 机
             other: String           // 其他信息，用于审核
             dataUrls: String[]      // 图片字符串数组，见 [说明](#0note)，第一张为 logo，第二张为 background
返回：       JSON
URL 示例：   http://localhost/Shop/Register
JSON 示例：
{
    "status":0,
    "description":"注册成功"
}
</pre></big>

### 3、登录商铺 Login
<big><pre>
请求方式：    POST
请求参数：    account: String     // 账号
             password: String    // 密码
返回：       JSON
URL 示例：   http://localhost/Shop/Login
JSON 示例：
{
    "status":0,                  /\* 状态码
                                  \* 账号不存在时为 20，账号存在、商铺不存在时为 21
                                  \*/ 商铺正在审核中时为 22，商铺审核失败时为 23
    "description":"登录成功",
    "shopId":"id",               // 商铺 ID，没有商铺则为空
    "userId":"id"                // 用户 ID，没有账号则为空
}
</pre></big>

### 4、获取我的商铺 GetMyShop
<big><pre>
请求方式：    POST
请求参数：    shopId: String      // 商铺 ID
返回：       JSON
URL 示例：   http://localhost/Shop/Login
JSON 示例：
{
    "status":0,
    "description":"登录成功",
    "shop":{
        Shop                     // 参照 [Shop Model](#1shop-model)，已加载 owner、classes 和 items
    }
}
</pre></big>

### 5、修改商铺资料 ModifyShopProfile
<big><pre>
请求方式：    POST
请求参数：    shopId: String          // 商铺 ID
             name: String            // 商铺名称
             category: String        // 商铺种类
             address: String         // 地址
             introduction: String    // 简介
             speed: int              // 送货速度，比如 30 表示 30 分钟送到
             timePeriods: Time       // 营业时间段，见 [Shop Model](#1shop-model)
             contact: String         // 联系方式
             price: float            // 起送价
             target: String          // 服务对象，用分号“;”分隔
             orderType: int          // 接受订单方式，0 为短信，1 为 POS 机
             other: String           // 其他信息，用于审核，可选
             dataUrls: String[]      // 图片字符串数组，见 [说明](#0note)，第一张为 logo，第二张为 background
返回：       JSON
URL 示例：   http://localhost/Shop/ModifyShopProfile
JSON 示例：
{
    "status":0,
    "description":"修改成功"
}
</pre></big>

### 6、发布商品 AddItem
<big><pre>
请求方式：    POST
请求参数：    shopId: String      // 商铺 ID
             itemName: String    // 商品名称
             price: Float        // 价格
             details: String     // 详情
             clazz: String       // 分类
             dataUrls: String[]  // 图片字符串数组，见 [说明](#0note)
返回：       JSON
URL 示例：   http://localhost/Shop/AddItem
JSON 示例：
{
    "status":0,
    "description":"发布成功"
}
</pre></big>

### 7、获取订单 GetOrders
<big><pre>
请求方式：    POST
请求参数：    shopId: String      // 商铺 ID
             dateStart: Date     // 起始日期，可选，默认为最早订单的日期
             dateEnd: Date       // 截止日期，可选，默认为当前日期
返回：       JSON
URL 示例：   http://localhost/Shop/GetOrders
JSON 示例：
{
    "status":0,
    "description":"获取成功",
    "orders":[{
        Order                    // 参照 [Order Model](#3order-model)，已加载 items、totalPrice 和 user
    }]
}
</pre></big>

### 8、将订单标为已读 ReadOrder
<big><pre>
请求方式：    POST
请求参数：    orderId: String     // 订单 ID
返回：       JSON
URL 示例：   http://localhost/Shop/ReadOrder
JSON 示例：
{
    "status":0,
    "description":"已读成功"
}
</pre></big>

### 9、获取订单详情 GetOrderDetails
<big><pre>
请求方式：    POST
请求参数：    orderId: String     // 订单 ID
返回：       JSON
URL 示例：   http://localhost/Shop/GetOrderDetails
JSON 示例：
{
    "status":0,
    "description":"获取成功",
    "order":{
        Order                    // 参照 [Order Model](#3order-model)，已加载全部附加属性
    }
}
</pre></big>

### 10、更新公告 EditBulletin
<big><pre>
请求方式：    POST
请求参数：    shopId: String      // 商铺 ID
             bulletin: String    // 公告
返回：       JSON
URL 示例：   http://localhost/Shop/EditBulletin
JSON 示例：
{
    "status":0,
    "description":"修改成功"
}
</pre></big>

### 11、删除分类 DeleteClass
<big><pre>
请求方式：    POST
请求参数：    shopId: String      // 商铺 ID
             clazz: String       // 分类
返回：       JSON
URL 示例：   http://localhost/Shop/DeleteClass
JSON 示例：
{
    "status":0,
    "description":"删除成功"
}
</pre></big>

### 12、删除商品 DeleteItem
<big><pre>
请求方式：    POST
请求参数：    shopId: String      // 商铺 ID
             itemId: String      // 商品 ID
返回：       JSON
URL 示例：   http://localhost/Shop/DeleteItem
JSON 示例：
{
    "status":0,
    "description":"删除成功"
}
</pre></big>

### 13、编辑商品 EditItem
<big><pre>
请求方式：    POST
请求参数：    itemId: String      // 商品 ID
             itemName: String    // 商品名称
             price: float        // 价格
             details: String     // 详情
             clazz: String       // 分类
             dataUrls: String[]  // 图片字符串数组，见 [说明](#0note)
返回：       JSON
URL 示例：   http://localhost/Shop/EditItem
JSON 示例：
{
    "status":0,
    "description":"修改成功"
}
</pre></big>

### 14、获取商铺审核信息 GetReviewInfo
<big><pre>
请求方式：    POST
请求参数：    shopId: String      // 商铺 ID
返回：       JSON
URL 示例：   http://localhost/Shop/GetReviewInfo
JSON 示例：
{
    "status":0,
    "description":"获取成功",
    "report":{
        Report                   // 参照 [Report Model](Admin.md#1report-model)
    }
}
</pre></big>

### 15、隐藏商铺 HideMyShop
<big><pre>
请求方式：    POST
请求参数：    shopId: String      // 商铺 ID
返回：       JSON
URL 示例：   http://localhost/Shop/HideMyShop
JSON 示例：
{
    "status":0,
    "description":"隐藏成功"
}
</pre></big>

### 16、显示商铺 ShowMyShop
<big><pre>
请求方式：    POST
请求参数：    shopId: String      // 商铺 ID
返回：       JSON
URL 示例：   http://localhost/Shop/ShowMyShop
JSON 示例：
{
    "status":0,
    "description":"显示成功"
}
</pre></big>

### 17、是否登录 IsLogin
<big><pre>
请求方式：    POST
请求参数：    无
返回：       JSON
URL 示例：   http://localhost/Shop/IsLogin
JSON 示例：
{
    "status":0,
    "description":"已登录",
    "user":{
        User                     // 参照 [User Model](Home.md#5user-model)，已加载 userDetails
    }
}
</pre></big>

### 18、退出登录 Logout
<big><pre>
请求方式：    POST
请求参数：    userId: String      // 用户ID
返回：       JSON
URL 示例：   http://localhost/Shop/Logout
JSON 示例：
{
    "status":0,
    "description":"退出登录成功"
}
</pre></big>
