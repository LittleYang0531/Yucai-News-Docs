## 基础信息修改

**前置条件**

1. 账号已处于登录态



**API地址**

```
POST https://www.littleyang.ml/api/account/information.php
```



**认证方式**

使用 COOKIE 进行认证 (SESSDATA)



**参数**

| 变量名   | 变量类型 | 必要性     | 含义     | 备注                   |
| -------- | -------- | ---------- | -------- | ---------------------- |
| realname | string   | **非必须** | 真实名称 |                        |
| school   | string   | **非必须** | 所属学校 |                        |
| grade    | integer  | **非必须** | 年级     |                        |
| class    | integer  | **非必须** | 班级     |                        |
| qq       | integer  | **非必须** | QQ 号    |                        |
| bilibili | integer  | **非必须** | B 站 UID |                        |
| birth    | string   | **非必须** | 生日     | 格式限制: 'xxxx-xx-xx' |
| sign     | string   | **非必须** | 个性签名 |                        |



**API回复**

| 变量名   | 变量类型 | 含义     | 备注             |
| -------- | -------- | -------- | ---------------- |
| realname | string   | 真实名称 | 等同于传入的参数 |
| school   | string   | 所属学校 | 等同于传入的参数 |
| grade    | integer  | 年级     | 等同于传入的参数 |
| class    | integer  | 班级     | 等同于传入的参数 |
| qq       | integer  | QQ 号    | 等同于传入的参数 |
| bilibili | integer  | B 站 UID | 等同于传入的参数 |
| birth    | string   | 生日     | 等同于传入的参数 |
| sign     | string   | 个性签名 | 等同于传入的参数 |



**示例：**

```bash
curl 'https://www.littleyang.ml/api/account/information.php' \
--data-urlencode 'realname=xxx' \
--data-urlencode 'school=xxx' \
--data-urlencode 'grade=10' \
--data-urlencode 'class=20' \
--data-urlencode 'qq=1234567890' \
--data-urlencode 'bilibili=1234567890' \
--data-urlencode 'birth=xxxx-xx-xx' \
--data-urlencode 'sign=xxx' \
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
        "realname":"xxx",
        "school":"xxx",
        "grade":10,
        "class":20,
        "qq":1234567890,
        "bilibili":1234567890,
        "birth":"xxxx-xx-xx",
        "sign":"xxx"
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

COOKIE 无效:

```json
{
    "code":-101,
    "message":"请先登录",
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

