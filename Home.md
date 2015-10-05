## 一、Model 部分

### 1、Item Model
<big><pre>
Item // 商品
{
    /\* DB 字段 \*/
    itemId: String              // 商品 ID
    itemName: String            // 商品名称
    price: float                // 价格
    details: String             // 简介
    releaseTime: Timestamp      // 发布时间
    unshelveTime: Timestamp     // 下架时间
    categoryId: String          // 商品种类 ID
    sellerId: String            // 卖家 ID
    readCount: long             // 阅读数
 
    /\* 附加属性 \*/
    category: Category          // 参照 [Category Model](#2category-model)
    seller: User                // 参照 [User Model](#5user-model)
    images: [
        ItemImage               // 参照 [ItemImage Model](#4itemimage-model)
    ]
    comments: [
        ItemComment             // 参照 [ItemComment Model](#3itemcomment-model)
    ]
    commentCount: long          // 评论数
}
</pre></big>

### 2、Category Model
<big><pre>
Category // 商品种类
{
    /\* DB 字段 \*/
    id: String                  // 种类 ID
    name: String                // 种类名称
    image: String               // 图片，相对路径
    priority: long              // 优先级，用于排序
­­ 
    /\* 附加属性 \*/
    itemCount: long             // 商品数
}
</pre></big>

### 3、ItemComment Model
<big><pre>
ItemComment // 商品评论
{
    /\* DB 字段 \*/
    commentId: String           // 评论 ID
    time: Timestamp             // 评论时间
    content: String             // 评论内容
    refId: String               // 引用 ID，为另一条评论的 ID，可为空
    makerId: String             // 评论者 ID
    itemId: String              // 商品 ID
 
    /\* 附加属性 \*/
    maker: User                 // 参照 [User Model](#5user-model)
}
</pre></big>

### 4、ItemImage Model
<big><pre>
ItemImage // 商品图片
{
    /\* DB 字段 \*/
    picId: String               // 图片 ID
    picUrl: String              // 图片相对路径
    itemId: String              // 商品 ID
}
</pre></big>

### 5、User Model
<big><pre>
User // 用户
{
    /\* DB 字段 \*/
    userId: String              // 用户 ID
    account: String             // 账号
    password: String            // 密码
    userName: String            // 昵称
    college: String             // 学校
    location: String            // 地址
    avatar: String              // 头像，相对路径
    role: int                   // 角色，0 为普通用户，1 为淘学管理员，2 为学校管理员
­­ 
    /\* 附加属性 \*/
    userDetails: UserDetails    // 参照 [UserDetails Model](#6userdetails-model)
}
</pre></big>

### 6、UserDetails Model
<big><pre>
UserDetails // 用户详细信息
{
    /\* DB 字段 \*/
    detailId: String            // ID
    campus: String              // 校区
    school: String              // 学院
    major: String               // 专业
    grade: int                  // 年级
    userId: String              // 用户ID
 
    /\* 附加属性 \*/
    user: User                  // 参照 [User Model](#5user-model)
    items: [
        Item                    // 参照 [Item Model](#1item-model)
    ]
    favoriteItems: [
        Item                    // 参照 [Item Model](#1item-model)
    ]
    favoriteSellers: [
        User                    // 参照 [User Model](#5user-model)
    ]
}
</pre></big>
