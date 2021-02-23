# 育才新闻api文档

------

## 目录

- [用户登录](#用户登录)
- [文章信息](#文章信息)
- [用户信息](#用户信息)
- [栏目信息](#栏目信息)
- [视频播放器](#视频播放器)

------

#### 用户登录

> [http://www.littleyang.ml/api/login](http://www.littleyang.ml/api/login)

*请求方式：GET*

##### 正文参数

|  参数名  | 类型 |   内容   | 必要性 | 备注 |
| :------: | :--: | :------: | :----: | :--: |
| UserName | str  |  用户名  |  必要  |      |
| Password | str  | 用户密码 |  必要  |      |
|  goUrl   | str  | 返回地址 | 非必要 |      |

##### json回复

根对象:

|  字段   | 类型 |       内容       |                             备注                             |
| :-----: | :--: | :--------------: | :----------------------------------------------------------: |
|  code   | num  |      返回值      | 0:成功<br>-653:用户名或用户密码为空<br>-629:用户名或用户密码错误 |
|   ts    | num  |    当前时间戳    |                       登录失败才会显示                       |
| message | num  |     错误信息     |                            恒为0                             |
|  data   | obj  | 登录成功返回信息 |                        登陆失败不返回                        |
|   ttl   | num  |     生存时间     |                            恒为1                             |

data对象:

|  字段   | 类型 |   内容   |          备注           |
| :-----: | :--: | :------: | :---------------------: |
|   uid   | num  |  用户id  |                         |
| islogin | bool | 是否登录 |                         |
|  goUrl  | str  | 返回地址 | 默认为www.littleyang.ml |

##### 示例

```shell
curl 'http://www.littleyang.ml/api/login?UserName=LittleYang0531&Password=xxxxxx&goUrl=//www.littleyang.ml/blog/'
```

<details>
<summary>查看响应示例：</summary>

```json
{
    "code":0,
    "message":"0",
    "ttl":1,
    "data":
    {
        "uid":"1",
        "isLogin":true,
        "goUrl":"//www.littleyang.ml/blog/"
    }
}
```

</details>

------

#### 文章信息

> [http://www.littleyang.ml/api/artical](http://www.littleyang.ml/api/artical)

*请求方式：GET*

##### 正文参数

| 参数名 | 类型 |  内容  | 必要性 | 备注 |
| :----: | :--: | :----: | :----: | :--: |
| column | num  | 栏目id |  必要  |      |
|   id   | num  | 文章id |  必要  |      |

##### json回复

根对象:

|  字段   | 类型 |   内容   |               备注                |
| :-----: | :--: | :------: | :-------------------------------: |
|  code   | num  |  返回值  | 0:成功<br>-400:栏目id或文章id无效 |
| message | num  | 错误信息 |                                   |
|  data   | obj  | 返回信息 |          请求失败不返回           |
|   ttl   | num  | 生存时间 |               恒为1               |

data对象:

|   字段   | 类型 |    内容    |   备注    |
| :------: | :--: | :--------: | :-------: |
| columnid | num  |   栏目id   |           |
|    id    | num  |   文章id   |           |
|   name   | str  |  文章标题  |           |
|  author  | str  | 作者用户名 |           |
|   view   | num  |   观看量   |           |
|   like   | num  |   点赞量   | 暂时恒为0 |

##### 示例

```shell
curl 'http://www.littleyang.ml/api/artical?column=1&id=1'
```

<details>
<summary>查看响应示例：</summary>


```json
{
    "code":0,
    "message":"0",
    "ttl":1,
    "data":
    {
        "columnid":"1",
        "id":"1",
        "name":"三巨头割据20班 各大势力疯狂扩充同僚",
        "author":"Dyro",
        "view":"45",
        "like":1
    }
}
```

</details>

------

#### 用户信息

> [http://www.littleyang.ml/api/account](http://www.littleyang.ml/api/account)

*请求方式：GET*

##### 正文参数

| 参数名 | 类型 |  内容  | 必要性 | 备注 |
| :----: | :--: | :----: | :----: | :--: |
|  uid   | num  | 用户id |  必要  |      |

##### json回复

根对象:

|  字段   | 类型 |   内容   |           备注            |
| :-----: | :--: | :------: | :-----------------------: |
|  code   | num  |  返回值  | 0:成功<br>-400:用户id无效 |
| message | num  | 错误信息 |                           |
|  data   | obj  | 返回信息 |      请求失败不返回       |
|   ttl   | num  | 生存时间 |           恒为1           |

data对象:

|    字段    | 类型 |         内容         |                  备注                  |
| :--------: | :--: | :------------------: | :------------------------------------: |
|    uid     | num  |        用户id        |                                        |
|    name    | str  |        用户名        |                                        |
|   birth    | date |         生日         |                                        |
|   school   | str  |         学校         |                                        |
|   class    | num  |         班级         |                                        |
|   grade    | num  |         年级         |                                        |
|   title    | str  |         称号         |                                        |
|    mail    | str  |         邮箱         |                                        |
|     QQ     | num  |         QQ号         |                                        |
|    bili    | str  | 用户哔哩哔哩主页地址 |                                        |
|   header   | str  |     用户头像地址     |                                        |
| background | str  |    用户背景图地址    |                                        |
| authority  | num  |       用户权限       | 0:普通权限<br>1:记者权限<br>2:超管权限 |

##### 示例

```shell
curl 'http://www.littleyang.ml/api/account?uid=1'
```

<details>
<summary>查看响应示例：</summary>


```json
{
    "code":0,
    "message":"0",
    "ttl":1,
    "data":
    {
        "uid":"1",
        "name":"LittleYang0531",
        "birth":"2006-05-**",
        "school":"重庆育才成功学校",
        "class":"20",
        "grade":"9",
        "title":"代码编辑组成员",
        "mail":"328676****@qq.com",
        "QQ":"328676****",
        "bili":"https://space.bilibili.com/399329***/",
        "header":"http://www.littleyang.ml/Person/LittleYang0531/header.jpg",
        "background":"http://www.littleyang.ml/Person/LittleYang0531/background.jpg",
        "authority":"2"
    }
}
```

</details>

------

#### 栏目信息

> [http://www.littleyang.ml/api/column](http://www.littleyang.ml/api/column)

*请求方式：GET*

##### 正文参数

| 参数名 | 类型 |  内容  | 必要性 | 备注 |
| :----: | :--: | :----: | :----: | :--: |
|   id   | num  | 栏目id |  必要  |      |

##### json回复

根对象:

|  字段   | 类型 |   内容   |           备注            |
| :-----: | :--: | :------: | :-----------------------: |
|  code   | num  |  返回值  | 0:成功<br>-400:栏目id无效 |
| message | num  | 错误信息 |                           |
|  data   | obj  | 返回信息 |      请求失败不返回       |
|   ttl   | num  | 生存时间 |           恒为1           |

data对象:

|   字段   | 类型 |     内容     | 备注 |
| :------: | :--: | :----------: | :--: |
|    id    | num  |    栏目id    |      |
|   name   | str  |    栏目名    |      |
| opentime | date | 创建栏目时间 |      |
| overtime | date | 截止投稿时间 |      |
|   view   | num  |    观看量    |      |

##### 示例

```shell
curl 'http://www.littleyang.ml/api/column?id=1'
```

<details>
<summary>查看响应示例：</summary>


```json
{
    "code":0,
    "message":"0",
    "ttl":1,
    "data":
    {
        "id":"1",
        "name":"初三上第十四周:2020\/11\/29-2020\/12\/04",
        "opentime":"2020-12-12",
        "overtime":"2021-12-12",
        "view":"85"
    }
}
```

</details>

------

#### 视频播放器

> http://www.littleyang.ml/beta%20features/video/index.html

*请求方式：GET*

##### 正文参数

| 参数名 | 类型 |  内容   | 必要性 |                  备注                  |
| :----: | :--: | :-----: | :----: | :------------------------------------: |
|  src   | str  | 资源url |  必要  | 目前仅允许mp4格式,且允许外部网站的链接 |

**建议使用内联框架(iframe)进行调用，页面直接返回HTML代码**

##### 示例

```html
<iframe src="http://www.littleyang.ml/beta%20features/video/index.html?src=http://www.littleyang.ml/photo/video/One%20Day.mp4">
</iframe>
```

<details>
<summary>查看响应示例：</summary>
<iframe width="1920px"
        height="680px"
        src="https://www.littleyang.ml/beta%20features/video/index.html?src=https://www.littleyang.ml/photo/video/One%20Day.mp4"></iframe>
</details>

