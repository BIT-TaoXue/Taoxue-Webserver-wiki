## 一、Model 部分

### 1、Talk Model
<big><pre>
Talk
{
    /\* DB 字段 \*/
    id: String              // 树洞 ID
    time: String            // 发布时间
    content: String         // 内容
    senderId: String        // 发布者 ID
    readCount: long         // 阅读数
 
    /\* 附加属性 \*/
    sender: User            // 参照 [User Model](Home.md#5user-model)
    comments: [
        TalkComment         // 参照 [TalkComment Model](#2talkcomment-model)
    ]
    commentCount: long      // 评论数
}
</pre></big>

### 2、TalkComment Model
<big><pre>
TalkComment
{
    /\* DB 字段 \*/
    id: String              // 评论 ID
    time: String            // 评论时间
    content: String         // 评论内容
    refId: String           // 引用的 ID
    senderId: String        // 评论者 ID
    talkId: String          // 树洞 ID
 
    /\* 附加属性 \*/
    sender: User            // 参照 [User Model](Home.md#5user-model)
}
</pre></big>

## 二、接口部分

### 1、获取树洞列表 GetTalks
<big><pre>
请求方式：    POST
请求参数：    userId: String  // 用户 ID，可选
             campus: String  // 学校和校区，可选，用“,”分隔，如“北京理工大学,良乡”
             cntStart: int   // 开始的个数（含），可选，从 0 开始
             cntEnd: int     // 结束的个数（不含），可选，从 0 开始
返回：       JSON
URL 示例：   http://localhost/Talk/GetTalks
JSON 示例：
{
    "status":0,
    "description":"获取成功",
    "talks":[{
        Talk                 // 参照 [Talk Model](#1talk-model)，已加载 sender 和 commentCount
    }]
}
</pre></big>

### 2、获取某一条树洞的评论 GetTalkComments
<big><pre>
请求方式：    POST
请求参数：    talkId: String  // 树洞 ID
返回：       JSON
URL 示例：   http://localhost/Talk/GetTalkComments
JSON 示例：
{
    "status":0,
    "description":"获取成功",
    "talkComments":[{
        TalkComment          // 参照 [TalkComment Model](#2talkcomment-model)，已加载 sender
    }]
}
</pre></big>

### 3、发表一条新的树洞 AddTalk
<big><pre>
请求方式：    POST
请求参数：    userId: String  // 用户 ID
             content: String // 树洞内容
返回：       JSON
URL 示例：   http://localhost/Talk/AddTalk
JSON 示例：
{
    "status":0,
    "description":"发布成功"
}
</pre></big>

### 4、撰写树洞评论 WriteTalkComment
<big><pre>
请求方式：    POST
请求参数：    talkId: String  // 评论的树洞 ID
             userId: String  // 评论者 ID
             content: String // 内容
             refId: String   // 引用的评论，可为空
返回：       JSON
URL 示例：   http://localhost/Talk/WriteTalkComment
JSON 示例：
{
    "status":0,
    "description":"评论成功"
}
</pre></big>

### 5、获取一个树洞消息 GetTalkById
<big><pre>
请求方式：    POST
请求参数：    talkId: String  // 评论的树洞 ID
返回：       JSON
URL 示例：   http://localhost/Talk/GetTalkById
JSON 示例：
{
    "status":0,
    "description":"获取成功",
    "talk":{
        Talk                 // 参照 [Talk Model](#1talk-model)，已加载 sender 和 commentCount
    }
}
</pre></big>

### 6、举报树洞 ReportTalk
<big><pre>
请求方式：    POST
请求参数：    talkId: String  // 树洞 ID
             userId: String  // 用户 ID
             content：String // 举报内容
返回：       JSON
URL 示例：   http://localhost/Talk/ReportTalk
JSON 示例：
{
    "status":0,
    "description":"举报成功"
}
</pre></big>
