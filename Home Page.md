### 1、获取首页信息 GetHomePageInfo
<big><pre>
请求方式：    POST
请求参数：    userId: String         // 用户 ID，可选
             <s>location: String    // 位置，可选，格式为“经度,纬度”</s> **已弃用，请用campus**
             campus: String         // 学校和校区，可选，用“,”分隔，如“北京理工大学,良乡”
返回：       JSON
URL 示例：   http://localhost/GetHomePageInfo
JSON 示例：
{
    "status":0,
    "description":"获取成功",
    "result":{
        "homePageImages":[          // 首页图片相对路径
            String
        ],
        "hotItems":[{               // 热门商品
            ShopItem                // 参照 [ShopItem Model](Shop.md#2shopitem-model)，已加载 images、shop 和 sellCount
        }],
        "hotShops":[{               // 热门商铺
            Shop                    // 参照 [Shop Model](Shop.md#1shop-model)，已加载 classes 和 sellCount
        }],
        "hotCategories":[{          // 热门分类
            "type":0,               // 商铺类型，见 [Shop Model](Shop#1shop-model)
            "category":"代理团购"	    // 商铺分类名
        }],
    }
}
</pre></big>

### 2、修改首页图片 ChangeHomePageImage
<big><pre>
请求方式：    POST
请求参数：    dataUrls: String[]     // 图片字符串数组，见 [说明](Shop.md#0note)，一次传一张
             index: int             // 索引，表示第几张，从 0 开始
             campus: String         // 学校和校区，可选，用“,”分隔，如“北京理工大学,良乡”
返回：       JSON
URL 示例：   http://localhost/HomePage/ChangeHomePageImage
JSON 示例：
{
    "status":0,
    "description":"修改成功"
}
</pre></big>

### 3、修改首页热门商品 ChangeHomePageItems
<big><pre>
请求方式：    POST
请求参数：    itemIds: String[]      // 商品 ID 数组
             campus: String         // 学校和校区，可选，用“,”分隔，如“北京理工大学,良乡”
返回：       JSON
URL 示例：   http://localhost/HomePage/ChangeHomePageItems
JSON 示例：
{
    "status":0,
    "description":"修改成功"
}
</pre></big>

### 4、修改首页热门商铺 ChangeHomePageShops
<big><pre>
请求方式：    POST
请求参数：    shopIds: String[]      // 商铺 ID 数组
             campus: String         // 学校和校区，可选，用“,”分隔，如“北京理工大学,良乡”
返回：       JSON
URL 示例：   http://localhost/HomePage/ChangeHomePageShops
JSON 示例：
{
    "status":0,
    "description":"修改成功"
}
</pre></big>

### 5、修改首页热门分类 ChangeHomePageCategories
<big><pre>
请求方式：    POST
请求参数：    types: String[]        // 商铺类型数组
             categories: String[]   // 分类名数组
             campus: String         // 学校和校区，可选，用“,”分隔，如“北京理工大学,良乡”
返回：       JSON
URL 示例：   http://localhost/HomePage/ChangeHomePageCategories
JSON 示例：
{
    "status":0,
    "description":"修改成功"
}
</pre></big>
