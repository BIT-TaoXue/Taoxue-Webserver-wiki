System 下的所有 action 都没有包名，即 URL 均为 http://localhost/actionName

### 1、获取服务器时间 GetServerTime
<big><pre>
请求方式：    POST
请求参数：    无
返回：       JSON
URL 示例：   http://localhost/GetServerTime
JSON 示例：
{
    "status":0,
    "description":"获取成功",
    "now":"2014-06-24T23:35:10"
}
</pre></big>

### 2、提交建议 SubmitAdvice
<big><pre>
请求方式：    POST
请求参数：    content: String    // 建议内容
返回：       JSON
URL 示例：   http://localhost/SubmitAdvice
JSON 示例：
{
    "status":0,
    "description":"提交成功"
}
</pre></big>

### 3、获取 APP 最低支持版本 GetAppMinVersion
<big><pre>
请求方式：    POST
请求参数：    appType: int       /\* APP 类型
                                 \* 0 为 iOS，1 为 Android，2 为 Windows Phone
                                 \*/
返回：       JSON
URL 示例：   http://localhost/GetAppMinVersion
JSON 示例：
{
    "status":0,
    "description":"获取成功",
    "minVersion":"1.0.0"
}
</pre></big>
