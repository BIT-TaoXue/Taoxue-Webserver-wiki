###1、发布商品 AddItem
<big><pre>
请求方式：    POST
请求参数：    itemName: String           // 商品名称
             price: float               // 商品价格
             categoryId: String         // 商品种类 ID
             details: String            // 商品详细信息
             userId: String             // 商品卖家 ID
             /\* 提供两种图片上传机制，任选其一 \*/
             images: File[]             // 商品图片文件数组，可选
             dataUrls: String[]         // 商品图片字符串数组，可选，见 [说明](Shop.md#0note)
返回：       JSON
URL 示例：   http://localhost/AddItem
JSON 示例：
{
    "status":0,
    "description":"发布成功"
}
</pre></big>
