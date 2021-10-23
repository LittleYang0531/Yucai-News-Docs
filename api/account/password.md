## 密码&邮箱修改

**前置条件**

1. 账号已处于登录态
2. 已获取到服务器默认公钥，建议阅读: [登录操作类 ( login ) - 系统公钥获取 ( public )](../login/public.md)
3. 已发送邮箱验证码并获取到 challenge 码，建议阅读: [账户操作类 ( account ) - 账户操作邮箱验证 ( verify )](../account/verify.md)



**API地址**

```
POST https://www.littleyang.ml/api/account/password.php
```



**认证方式**

使用 COOKIE 进行认证 (SESSDATA)

该 API 中密码加密方法: 将密码与获取到的服务器默认公钥进行 RSA 算法加密，得到的结果即为加密后的密码。

操作执行完成后，会自动清空全平台的登录态，因此登录态会返回为 false。



**参数**

| 变量名       | 变量类型 | 必要性     | 含义                | 备注                               |
| ------------ | -------- | ---------- | ------------------- | ---------------------------------- |
| old          | string   | **必须**   | 原密码              |                                    |
| oldemail     | string   | **必须**   | 原邮箱              |                                    |
| oldchallenge | string   | **必须**   | 原邮箱 challenge 码 |                                    |
| oldecode     | integer  | **必须**   | 原邮箱验证码        |                                    |
| new          | string   | **非必须** | 新密码              |                                    |
| newemail     | string   | **非必须** | 新邮箱              |                                    |
| newchallenge | string   | **非必须** | 新邮箱 challenge 码 | 若新邮箱不为空则该参数**不能**为空 |
| newecode     | integer  | **非必须** | 新邮箱验证码        | 若新邮箱不为空则该参数**不能**为空 |



**API回复**

| 变量名   | 变量类型 | 含义             | 备注         |
| -------- | -------- | ---------------- | ------------ |
| uid      | integer  | 用户 id          |              |
| isLogin  | boolean  | 登录态           | 固定为 false |
| password | string   | 用户操作后的密码 |              |
| email    | string   | 用户操作后的邮箱 |              |



**示例：**

```bash
curl 'https://www.littleyang.ml/api/account/password.php' \
--data-urlencode 'old=xxx' \
--data-urlencode 'oldemail=xxx' \
--data-urlencode 'oldchallenge=xxx' \
--data-urlencode 'oldecode=xxx' \
--data-urlencode 'new=xxx' \
--data-urlencode 'newemail=xxx' \
--data-urlencode 'newchallenge=xxx' \
--data-urlencode 'newecode=xxx' \
-b 'SESSDATA=xxx&DedeUserId=xxx&DedeUserId__ckMd5=xxx&CSRF=xxx'
```



**查看响应示例 (JSON):**

修改成功:

```json
{
    "code":0,
    "message":"",
    "data":
    {
        "uid":1,
		"isLogin":false,
		"password":"xxx",
		"email":"xxx"
    },
    "ttl":0
}
```

COOKIE 无效:

```json
{
    "code":-652,
    "message":"账号未登录",
    "ttl":0
}
```

必要参数为空:

```json
{
    "code":-653,
    "message":"xxx不能为空",
    "ttl":0
}
```

数据库连接失败:

```json
{
    "code":-500,
    "message":"无法连接数据库",
    "ttl":0
}
```

数据库查询错误:

```json
{
    "code":-400,
    "message":"数据库查询错误",
    "ttl":0
}
```

数据库执行错误:

```json
{
    "code":-400,
    "message":"数据库执行错误",
    "ttl":0
}
```

原密码/邮箱错误:

```json
{
    "code":-629,
    "message":"原密码/邮箱错误",
    "ttl":0
}
```

challenge 值有误:

```json
{
    "code":-629,
    "message":"原邮箱/新邮箱验证码challenge无效",
    "ttl":0
}
```

邮箱验证码有误:

```json
{
    "code":-629,
    "message":"原邮箱/新邮箱验证码有误",
    "ttl":0
}
```

新邮箱已被使用:

```json
{
    "code":-404,
    "message":"新邮箱已被使用",
    "ttl":0
}
```

