### 1、登录 Login
<big><pre>
请求方式：    POST
请求参数：    account: String     // 账号，手机号
             password: String    // 密码
返回：       JSON
URL 示例：   http://localhost/Login
JSON 示例：
{
    "status":0,
    "description":"登录成功",
    "user":{
        User                     // 参照 [User Model](Home.md#5user-model)，已加载 userDetails
    }
}
</pre></big>

### 2、注册 Register
<big><pre>
请求方式：    POST
请求参数：    account: String     // 账号，手机号
             userName: String    // 昵称
             password: String    // 密码，确认密码前端自行校验
             college: String     // 学校
             location: String    // 地址
返回：       JSON
URL 示例：   http://localhost/Register
JSON 示例
{
    "status":0,
    "description":"注册成功",
    "user":{
        User                     // 参照 [User Model](Home.md#5user-model)，已加载 userDetails
    }
}
</pre></big>

### 3、校验账号 CheckAccount
<big><pre>
请求方式：    POST
请求参数：    account: String     // 账号
返回：       JSON
URL 示例：   http://localhost/CheckAccount
JSON 示例：
{
    "status":0,
    "description":"可以注册"
}
</pre></big>

### 4、校验昵称 CheckUserName
<big><pre>
请求方式：    POST
请求参数：    userName: Sting    // 昵称
返回：       JSON
URL 示例：   http://localhost/CheckUserName
JSON 示例：
{
    "status":0,
    "description":"可以注册"
}
</pre></big>

### 5、重置密码 ResetPassword
<big><pre>
请求方式：    POST
请求参数：    acount: String      // 账号
             password: String    // 密码（确认密码前端自行校验）
返回：       JSON
URL 示例：   http://localhost/ResetPassword
JSON 示例：
{
    "status":0,
    "description":"重置密码成功"
}
</pre></big>

### 6、发送校验码 SendCheckCode
<big><pre>
请求方式：    POST
请求参数：    acount: String      // 账号
             type: int           // 类型，0 为注册，1 为重置密码
返回：       JSON
URL 示例：   http://localhost/SendCheckCode
JSON 示例：
{
    "status":0,
    "description":"发送成功"
}
</pre></big>

### 7、验证校验码 VerifyCheckCode
<big><pre>
请求方式：    POST
请求参数：    acount: String      // 账号
             checkCode: String   // 校验码
返回：       JSON
URL 示例：   http://localhost/VerifyCheckCode
JSON 示例：
{
    "status":0,                  // 2 为验证码错误
    "description":"验证成功"
}
</pre></big>
