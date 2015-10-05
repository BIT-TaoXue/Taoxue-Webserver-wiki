### 1、获取所有商品种类 GetCategories
<big><pre>
请求方式：    POST
请求参数：    campus: String      // 学校和校区，可选，用“,”分隔，如“北京理工大学,良乡”
返回：       JSON
URL 示例：   http://localhost/Market/GetCategories
JSON 示例：
{
    "status":0,
    "description":"获取成功",
    "categories":[{
        Category                 // 参照 [Category Model](Home.md#2category-model)，已加载 itemCount
    }]
}
</pre></big>


### 2、获取商品列表 GetItems
<big><pre>
请求方式：    POST
请求参数：    keyWord: String     // 搜索关键字，可选
             categoryId: String  // 种类 ID，可选
             order: int          /\* 排序方式，可选
                                  \* 默认 0 时间降序，1 价格降序，2 价格升序
                                  \*/
             userId: String      // 用户 ID，可选
             campus: String      // 学校和校区，可选，用“,”分隔，如“北京理工大学,良乡”
             cntStart: int       // 开始的个数（含），可选，从 0 开始
             cntEnd: int         // 结束的个数（不含），可选，从 0 开始
返回：       JSON
URL 示例：   http://localhost/Market/GetItems
JSON 示例：
{
    "status":0,
    "description":"获取成功",
    "items":[{
        Item                     // 参照 [Item Model](Home.md#1item-model)，已加载 images、seller 和 commentCount
    }]
}
</pre></big>

### 3、获取商品详细信息 GetItemDetails
<big><pre>
请求方式：    POST
请求参数：    itemId：String      // 商品 ID
返回：       JSON
URL 示例：   http://localhost/Market/GetItemDetails
JSON 示例：
{
    "status":0,
    "description":"获取成功",
    "item":{
        Item                     // 参照 [Item Model](Home.md#1item-model)，已加载 category、images、seller 和 commentCount
    }
}
</pre></big>

### 4、获取商品评论 GetItemComments
<big><pre>
请求方式：    POST
请求参数：    itemId：String      // 商品 ID
返回：       JSON
URL 示例：   http://localhost/Market/GetItemComments
JSON 示例：
{
    "status":0,
    "description":"获取成功",
    "comments":[{
        Comment                  // 参照 [ItemComment Model](Home.md#3itemcomment-model)，已加载 maker
    }]
}
</pre></big>

### 5、撰写商品评论 WriteItemComment
<big><pre>
请求方式：    POST
请求参数：    itemId：String      // 商品 ID
             userId：String      // 当前登录用户 ID
             content：String     // 评论内容
             refId：String       // 引用的评论 ID，可为空
返回：       JSON
URL 示例：   http://localhost/Market/WriteItemComment
JSON 示例：
{
    "status":0,
    "description":"评论成功"
}
</pre></big>

### 6、收藏商品 AddItemToFavorite
<big><pre>
请求方式：    POST
请求参数：    userId：String      // 当前登录用户 ID
             itemId：String      // 商品 ID
返回：       JSON
URL 示例：   http://localhost/Market/AddItemToFavorite
JSON 示例：
{
    "status":0,
    "description":"收藏成功"
}
</pre></big>

### 7、获取卖家的联系方式 GetSellerContact
<big><pre>
请求方式：    POST
请求参数：    sellerId：String    // 卖家 ID
返回：       JSON
URL 示例：   http://localhost/Market/GetSellerContact
JSON 示例：
{
    "status":0,
    "description":"获取成功",
    "sellerAccount":"10086"
}
</pre></big>

### 8、获取卖家的详细信息 GetSellerDetails
<big><pre>
请求方式：    POST
请求参数：    sellerId：String    // 卖家 ID
返回：       JSON
URL 示例：   http://localhost/Market/GetSellerDetails
JSON 示例：
{
    "status":0,
    "description":"获取成功",
    "sellerDetails":{
        UserDetails Model        // 参照 [UserDetails Model](Home.md#6userdetails-model)，已加载 user 和 items
    }
}
</pre></big>

### 9、关注卖家 AddSellerToFavorite
<big><pre>
请求方式：    POST
请求参数：    userId：String      // 用户 ID
             sellerId：String    // 卖家 ID
返回：       JSON
URL 示例：   http://localhost/Market/AddSellerToFavorite
JSON 示例：
{
    "status":0,
    "description":"关注成功"
}
</pre></big>

### 10、取消收藏商品 RemoveItemFromFavorite
<big><pre>
请求方式：    POST
请求参数：    userId：String      // 用户 ID
             itemId：String      // 商品 ID
返回：       JSON
URL 示例：   http://localhost/Market/RemoveItemFromFavorite
JSON 示例：
{
    "status":0,
    "description":"取消收藏成功"
}
</pre></big>

### 11、取消关注卖家 RemoveSellerFromFavorite
<big><pre>
请求方式：    POST
请求参数：    userId：String      // 用户 ID
             sellerId：String    // 卖家 ID
返回：       JSON
URL 示例：   http://localhost/Market/RemoveSellerFromFavorite
JSON 示例：
{
    "status":0,
    "description":"取消关注成功"
}
</pre></big>

### 12、是否收藏商品 IsFavoriteItem
<big><pre>
请求方式：    POST
请求参数：    userId：String      // 用户 ID
             itemId：String      // 商品 ID
返回：       JSON
URL 示例：   http://localhost/Market/IsFavoriteItem
JSON 示例：
{
    "status":0,                  // 没有收藏返回 0，已经收藏返回 1
    "description":"没有收藏"
}
</pre></big>

### 13、是否关注卖家 IsFavoriteSeller
<big><pre>
请求方式：    POST
请求参数：    userId：String      // 用户 ID
             sellerId：String    // 卖家 ID
返回：       JSON
URL 示例：   http://localhost/Market/IsFavoriteSeller
JSON 示例：
{
    "status":0,                  // 没有关注返回 0，已经关注返回 1
    "description":"没有关注"
}
</pre></big>

### 14、获取首页图片 GetHomePageImages
<big><pre>
**已弃用，请用 [GetHomePageInfo](Home Page.md#user-content-1获取首页信息-gethomepageinfo)**
<s>
请求方式：    POST
请求参数：    无
返回：       JSON
URL 示例：   http://localhost/Market/GetHomePageImages
JSON 示例：
{
    "status":0,
    "description":"获取成功",
    "homePageImages":[
        "/image/1.jpeg",
        "/image/2.jpeg",
        "/image/3.jpeg"
    ]
}
</s>
</pre></big>

### 15、 举报商品 ReportItem
<big><pre>
请求方式：    POST
请求参数：    userId：String      // 用户 ID
             itemId：String      // 商品 ID
             content：String     // 举报内容
返回：       JSON
URL 示例：   http://localhost/Market/ReportItem
JSON 示例：
{
    "status":0,
    "description":"举报成功"
}
</pre></big>
