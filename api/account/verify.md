## 账户操作邮箱验证

**前置条件**

1. 账号已处于登录态 (当传入参数 check 的值为 true 时)
2. 有效的 User-Agent



**API地址**

```
POST https://www.littleyang.ml/api/account/verify.php
```



**认证方式**

使用 COOKIE 进行认证 (SESSDATA)



**参数**

| 变量名 | 变量类型 | 必要性   | 含义           | 备注   |
| ------ | -------- | -------- | -------------- | ------ |
| email  | string   | **必须** | 邮箱           |        |
| check  | boolean  | **必须** | 是否验证登录态 | 见说明 |

变量 check 说明: 当 check 的值为 true 时，API 会验证输入的邮箱与登录态所对应的邮箱是否相同，常用于验证操作者是否为用户本人。



**API回复**

| 变量名    | 变量类型 | 含义              | 备注 |
| --------- | -------- | ----------------- | ---- |
| email     | string   | 邮箱              |      |
| challenge | string   | 邮箱 challenge 码 |      |



**示例：**

```bash
curl 'https://www.littleyang.ml/api/account/verify.php' \
--data-urlencode 'email=xxx' \
--data-urlencode 'check=1' \
```



**查看响应示例 (JSON):**

邮件发送成功:

```json
{
    "code":0,
    "message":"",
    "data":
    {
        "email":"xxx",
        "challenge":"xxx"
    },
    "ttl":0
}
```

调用方法错误:

```json
{
	"code":-405,
    "message":"调用方法错误",
    "ttl":0
}
```

COOKIE 无效 (当 check 的值为 true 时会引发):

```json
{
    "code":-652,
    "message":"账号未登录",
    "ttl":0
}
```

输入邮箱与登录态不对应 (当 check 的值为 true 时会引发):

```json
{
    "code":-629,
    "message":"邮箱与账户不对应",
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

User-Agent 无效:

```json
{
    "code":-404,
    "message":"无效的UserAgent",
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

邮箱未创建账号:

```json
{
    "code":-626,
    "message":"此邮箱没有创建账号!",
    "ttl":0
}
```

被封禁的账号:

```json
{
    "code":-102,
    "message":"此账号已被封禁!",
    "ttl":0
}
```

邮件发送错误:

```json
{
    "code":-400,
    "message":"邮件发送错误",
    "ttl":0
}
```

