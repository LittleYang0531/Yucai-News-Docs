## 头像替换

**前置条件**

1. 账号已处于登录态



**API地址**

```
POST https://www.littleyang.ml/api/account/header.php
```



**认证方式**

使用 COOKIE 进行认证 (SESSDATA)



**参数**

| 变量名                | 变量类型     | 必要性   | 含义       | 备注                   |
| --------------------- | ------------ | -------- | ---------- | ---------------------- |
| setting-header-submit | 无限制       | **必须** | 无含义     | 无参数要求，设置了就行 |
| setting-header        | _FILE object | **必须** | 文件结构体 | 限制后缀名为 .jpg      |



**API回复**

部分直接返回 GUI 的 HTML 代码，部分返回 JSON



**示例：**

```bash
curl 'https://www.littleyang.ml/api/account/header.php' \
-b 'SESSDATA=xxx&DedeUserId=xxx&DedeUserId__ckMd5=xxx&CSRF=xxx'
```



**查看响应示例 (HTML):**

上传成功 :

```html
<script>
    alert('上传成功');
    window.location.href='https://www.littleyang.ml/index.php?method=setting';
</script>
```

COOKIE 无效 :

```html
<script>
    alert('请先登录!');
    window.history.back(-1);
</script>
```

内部错误 :

```html
<script>
    alert('错误:xxx');
    window.history.back(-1);
</script>
```

```html
<script>
    alert('数据库查询错误!');
    window.history.back(-1);
</script>
```



**查看响应示例 (JSON):**

调用方法错误 :

```json
{
    "code":-405,
    "message":"调用方法错误",
    "ttl":1
}
```

