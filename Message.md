## 一、Model 部分

### 1、Message Model
<big><pre>
Message
{
    /\* DB 字段 \*/
    id: String                  // 消息 ID
    content: String             // 消息内容
    time: String                // 生成时间
    senderId: String            // 发送者 ID
    receiverId: String          // 接收者 ID
    refType: int                /\* 引用类型，用来跳转
                                 \*/ 0 为商品，1 为树洞，2 为商铺的商品
    refId: String               // 引用 ID，为商品 ID 或树洞 ID
    isRead: int                 // 是否已读，0 表示未读，1 表示已读
 
    /\* 附加属性 \*/
    sender: User                // 参照 [User Model](Home.md#5user-model)
}
</pre></big>

## 二、接口部分

### 1、获取用户未读消息 GetMessages
<big><pre>
请求方式：    POST
请求参数：    userId: String      // 用户 ID
             cntStart: int       // 开始的个数（含），可选，从 0 开始
             cntEnd: int         // 结束的个数（不含），可选，从 0 开始
返回：       JSON
URL 示例：   http://localhost/Message/GetMessages
JSON 示例：
{
    "status":0,
    "description":"获取成功",
    "messages":[{
        Message                  // 参照 [Message Model](#1message-model)，已加载 sender
    }]
}
</pre></big>

### 2、获取用户全部消息 GetAllMessages
<big><pre>
请求方式：    POST
请求参数：    userId: String      // 用户 ID
             cntStart: int       // 开始的个数（含），可选，从 0 开始
             cntEnd: int         // 结束的个数（不含），可选，从 0 开始
返回：       JSON
URL 示例：   http://localhost/Message/GetAllMessages
JSON 示例：
{
    "status":0,
    "description":"获取成功",
    "messages": [{
        Message                  // 参照 [Message Model](#1message-model)，已加载 sender
    }]
}
</pre></big>

### 3、将一个消息标记为已读 ReadMessage
<big><pre>
请求方式：    POST
请求参数：    messageId: String   // 消息 ID
返回：       JSON
URL 示例：   http://localhost/Message/ReadMessage
JSON 示例：
{
    "status":0,
    "description":"成功"
}
</pre></big>

### 4、获取用户未读消息数量 GetUnreadMessageCount
<big><pre>
请求方式：    POST
请求参数：    userId: String      // 用户 ID
返回：       JSON
URL 示例：   http://localhost/Message/GetUnreadMessageCount
JSON 示例：
{
    "status":0,
    "description":"获取成功",
    "unreadMessageCount":5
}
</pre></big>

### 5、清空用户的所有消息 ClearAllMessages
<big><pre>
请求方式：    POST
请求参数：    userId: String      // 用户 ID
返回：       JSON
URL 示例：   http://localhost/Message/ClearAllMessages
JSON 示例：
{
    "status":0,
    "description":"清空成功"
}
</pre></big>
