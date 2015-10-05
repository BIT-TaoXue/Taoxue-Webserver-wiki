### 1、查看个人资料 GetMyProfile
<big><pre>
请求方式：    POST
请求参数：    userId: String      // 用户 ID
返回：       JSON
URL 示例：   http://localhost/Personal/GetMyProfile
JSON 示例：
{
    "status":0,
    "description":"获取成功",
    "userDetails":{
        UserDetails              // 参照 [UserDetails Model](Home.md#6userdetails-model)，已加载 user
    }
}
</pre></big>

### 2、修改密码 ModifyPassword
<big><pre>
请求方式：    POST
请求参数：    userId: String      // 用户 ID
             oldPassword: String // 原密码
             newPassword: String // 新密码（确认密码前端自行校验）
返回：       JSON
URL 示例：   http://localhost/Personal/ModifyPassword
JSON 示例：
{
    "status":0,
    "description":"修改成功"
}
</pre></big>

### 3、修改个人资料 ModifyMyProfile
<big><pre>
请求方式：    POST
请求参数：    userId: String      // 用户 ID
             campus: String      // 修改后的校区
             school: String      // 修改后的学院
             major: String       // 修改后的专业
             grade: int          // 修改后的年级（入学年份）
             location: String    // 修改后的具体位置
             /\* 提供两种图片上传机制，任选其一，可不传，表示不修改 \*/
             images: File[]      // 修改后的头像图片文件，可选
             dataUrls: String[]  // 修改后的头像图片字符串数组，可选，见 [说明](Shop.md#0note)
返回：       JSON
URL 示例：   http://localhost/Personal/ModifyMyProfile
JSON 示例：
{
    "status":0,
    "description":"修改成功"
}
</pre></big>

### 4、获取我发布的所有商品的种类 GetMyCategories
<big><pre>
请求方式：    POST
请求参数：    userId: String      // 用户 ID
返回：       JSON
URL 示例：   http://localhost/Personal/GetMyCategories
JSON 示例：
{
    "status":0,
    "description":"获取成功",
    "categories":[{
        Category                 // 参照 [Category Model](Home.md#2category-model)，已加载 itemCount
    }]
}
</pre></big>

### 5、获取我发布的商品 GetMyItems
<big><pre>
请求方式：    POST
请求参数：    userId: string      // 用户 ID
             categoryId: String  // 种类 ID，可选，默认为全部
             cntStart: int       // 开始的个数（含），可选，从 0 开始
             cntEnd: int         // 结束的个数（不含），可选，从 0 开始
返回：       JSON
URL 示例：   http://localhost/Personal/GetMyItems
JSON 示例：
{
    "status":0,
    "description":"获取成功",
    "items":[{
        Item                     // 参照 [Item Model](Home.md#1item-model)，已加载 category 和 images
    }]
}
</pre></big>

### 6、编辑我的商品 EditMyItem
<big><pre>
请求方式：    POST
请求参数：    itemId: String      // 商品 ID
             userId: String      // 用户 ID
             itemName: String    // 商品名称
             price: float        // 商品价格
             categoryId: String  // 商品种类 ID
             details: String     // 商品详细信息
             images: File[]      // 商品图片文件数组，可选
             dataUrls: String[]  // 商品图片字符串数组，可选，见 [说明](Shop.md#0note)
返回：       JSON
URL 示例：   http://localhost/Personal/EditMyItem
JSON 示例：
{
    "status":0,
    "description":"修改成功"
}
</pre></big>

### 7、删除我的商品 DeleteMyItem
<big><pre>
请求方式：    POST
请求参数：    itemId: String      // 商品 ID
             userId: String      // 用户 ID
返回：       JSON
URL 示例：   http://localhost/Personal/DeleteMyItem
JSON 示例：
{
    "status":0,
    "description":"删除成功"
}
</pre></big>

### 8、获取我关注的卖家 GetMyFavoriteSellers
<big><pre>
请求方式：    POST
请求参数：    userId: String      // 用户 ID
             cntStart: int       // 开始的个数（含），可选，从 0 开始
             cntEnd: int         // 结束的个数（不含），可选，从 0 开始
返回：       JSON
URL 示例：   http://localhost/Personal/GetMyFavoriteSellers
JSON 示例：
{
    "status":0,
    "description":"获取成功",
    "favoriteSellers":[{
        User                     // 参照 [User Model](Home.md#5user-model)
    }]
}
</pre></big>

### 9、获取我收藏的宝贝 GetMyFavoriteItems
<big><pre>
请求方式：    POST
请求参数：    userId: string      // 用户 ID
             cntStart: int       // 开始的个数（含），可选，从 0 开始
             cntEnd: int         // 结束的个数（不含），可选，从 0 开始
返回：       JSON
URL 示例：   http://localhost/Personal/GetMyFavoriteItems
JSON 示例：
{
    "status":0,
    "description":"获取成功",
    "favoriteItems":[{
        Item                     // 参照 [Item Model](Home.md#1item-model)，已加载 images、seller 和 commentCount
    }]
}
</pre></big>

### 10、商品下架 UnshelveMyItem
<big><pre>
请求方式：    POST
请求参数：    itemId: String      // 商品 ID
             userId: String      // 用户 ID
返回：       JSON
URL 示例：   http://localhost/Personal/UnshelveMyItem
JSON 示例：
{
    "status":0,
    "description":"下架成功"
}
</pre></big>

### 11、商品续期 RenewMyItem
<big><pre>
请求方式：    POST
请求参数：    itemId: String      // 商品 ID
             userId: String      // 用户 ID
返回：       JSON
URL 示例：   http://localhost/Personal/RenewMyItem
JSON 示例：
{
    "status":0,
    "description":"续期成功"
}
</pre></big>

### 12、获取指定学校的所有院系 GetSchools
<big><pre>
**已弃用，请用 [GetSchools](College.md#user-content-2获取指定学校的所有院系-getschools)**
<s>
请求方式：    POST
请求参数：    college: String     // 学校名称，如：北京理工大学
返回：       JSON
URL 示例：   http://localhost/Personal/GetSchools
JSON 示例：
{
    "status":0,
    "description":"获取成功",
    "schools":[
        "计算机学院",
        "经济与管理学院"
    ]
}
</s>
</pre></big>

### 13、获取指定学校的某一院系的所有专业 GetMajors
<big><pre>
**已弃用，请用 [GetMajors](College.md#user-content-3获取指定学校的某一院系的所有专业-getmajors)**
<s>
请求方式：    POST
请求参数：    college: String     // 指定学校的学校名称，如：北京理工大学
             school: String      // 指定的院系，如：计算机学院
返回：       JSON
URL 示例：   http://localhost/Personal/GetMajors
JSON 示例：
{
    "status":0,
    "description":"获取成功",
    "majors":[
        "计算机科学与技术",
        "物联网"
    ]
}
</s>
</pre></big>

### 14、获取可选的年级 GetGrades
<big><pre>
**已弃用，请用 [GetGrades](College.md#user-content-4获取可选的年级-getgrades)**
<s>
请求方式：    POST
请求参数：    无
返回：       JSON
URL 示例：   http://localhost/Personal/GetGrades
JSON 示例：
{
    "status":0,
    "description":"获取成功",
    "grades":[
        2015,
        2014,
        2013,
        2012,
        2011
    ]
}
</s>
</pre></big>

### 15、获取我正在审核中的商品个数 GetMyReviewingItemCount
<big><pre>
请求方式：    POST
请求参数：    userId: string      // 当前登录用户 ID
返回：       JSON
URL 示例：   http://localhost/Personal/GetMyReviewingItemCount
JSON 示例：
{
    "status":0,
    "description":"获取成功",
    "itemCount":5
}
</pre></big>

### 16、获取我正在审核中的商品 GetMyReviewingItems
<big><pre>
请求方式：    POST
请求参数：    userId: string      // 当前登录用户 ID
             cntStart: int       // 开始的个数（含），可选，从 0 开始
             cntEnd: int         // 结束的个数（不含），可选，从 0 开始
返回：       JSON
URL 示例：   http://localhost/Personal/GetMyReviewingItems
JSON 示例：
{
    "status":0,
    "description":"获取成功",
    "items":[{
        Item                     // 参照 [Item Model](Home.md#1item-model)，已加载 category 和 images
    }]
}
</pre></big>
