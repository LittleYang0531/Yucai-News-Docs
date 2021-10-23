## 忘记密码选项

**前置条件**

1. 已获取到服务器默认公钥，建议阅读: [登录操作类 ( login ) - 系统公钥获取 ( public )](../login/public.md)
2. 已发送邮箱验证码并获取到 challenge 码，建议阅读: [账户操作类 ( account ) - 账户操作邮箱验证 ( verify )](../account/verify.md)



**API地址**

```
POST https://www.littleyang.ml/api/account/password2.php
```



**认证方式**

无

该 API 中密码加密方法: 将密码与获取到的服务器默认公钥进行 RSA 算法加密，得到的结果即为加密后的密码。

操作执行完成后，会自动清空全平台的登录态，因此登录态会返回为 false。



**参数**

| 变量名    | 变量类型 | 必要性   | 含义              | 备注 |
| --------- | -------- | -------- | ----------------- | ---- |
| email     | string   | **必须** | 邮箱              |      |
| challenge | string   | **必须** | 邮箱 challenge 码 |      |
| ecode     | integer  | **必须** | 邮箱验证码        |      |
| new       | string   | **必须** | 新密码            |      |



**API回复**

| 变量名   | 变量类型 | 含义             | 备注         |
| -------- | -------- | ---------------- | ------------ |
| uid      | integer  | 用户 id          |              |
| isLogin  | boolean  | 登录态           | 固定为 false |
| password | string   | 用户操作后的密码 |              |
| email    | string   | 用户邮箱         |              |



**示例：**

```bash
curl 'https://www.littleyang.ml/api/account/password2.php' \
--data-urlencode 'email=xxx' \
--data-urlencode 'challenge=xxx' \
--data-urlencode 'ecode=xxx' \
--data-urlencode 'new=xxx' \
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

challenge 值有误:

```json
{    "code":-629,    "message":"原邮箱验证码challenge无效",    "ttl":0}
```

邮箱验证码有误:

```json
{    "code":-629,    "message":"原邮箱验证码有误",    "ttl":0}
```

