## LYOJ API 文档

本站所有 API 请求结果均被包裹在 `<pre style='word-wrap: break-word;white-space: pre-wrap;'></pre>` 标签里面，使用脚本处理时请使用正则表达式将正文两边的 tag 去掉。

本站所有 API 请求网址前均省略了 `http://172.25.50.253`，使用脚本请求时要记得在网址前加上刚刚那一串地址。

例如: 请求 pid=22 的题目信息，使用指令 `curl http://172.25.50.253/api/problem/info.php?pid=22` 即可获取到 pid=22 的题目信息的 JSON 数据格式，用正则表达式提取一下正文内容就可以使用 JSON 解析了。

所有 API 通用返回格式: 

|字段|类型|内容|备注|
|:-:|:-:|:-:|:-:|
|`code`|num|返回状态|`0` 表示成功|
|`message`|string|错误信息|请求成功时该项为空|
|`data`|obj|请求数据主体|请求失败时无此字段|
|`ttl`|num|1|-|

下面所有 API 均只介绍 `data` 主体内的内容。

### 其他

-----

#### 公共错误码

|错误代码|`message` 消息|含义|
|:-:|:-:|:-:|
|`-101`|`Not Login!`|请求中缺少正确的登录态|
|`-113`|`Email 'xxx' not verify!`|邮箱 `xxx` 未经过验证|
|`-400`|`Invalid ZIP Package`|无效的 ZIP 文件|
|`-400`|`Failed to send email!`|邮件发送失败|
|`-400`|`Failed to query database: xxx`|数据库查询失败，错误信息: xxx|
|`-400`|`Failed to execute database: xxx`|数据库执行失败，错误信息: xxx|
|`-403`|`Permission denied`|没有权限|
|`-404`|`Contest id xxx not found!`|无法找到 id 为 `xxx` 的比赛|
|`-404`|`Cannot found param "xxx"!`|请求中缺少参数 `xxx`|
|`-500`|`System Error!`|系统错误|
|`-500`|`Failed to connect database`|无法连接数据库|
|`-626`|`Connot found user "xxx"`|无法找到邮箱为 `xxx` 的用户|
|`-629`|`Username or password is incorrect!`|用户名或密码错误|
|`-652`|`Email 'xxx' have been used!`|邮箱 `xxx` 已被使用|
|`-652`|`Username 'xxx' have been used!`|用户名 `xxx` 已被使用|
|`-658`|`Salt value timed out! Please try again!`|盐值已过期，请重新获取|

-----

#### 语言代码

|`lang` 代码|含义|
|:-:|:-:|
|`0`|`C++98 (gcc9.3.0 amd64)`|
|`1`|`C++98 O2 (gcc9.3.0 amd64)`|
|`2`|`C++03 (gcc9.3.0 amd64)`|
|`3`|`C++03 O2 (gcc9.3.0 amd64)`|
|`4`|`C++11 (gcc9.3.0 amd64)`|
|`5`|`C++11 O2 (gcc9.3.0 amd64)`|
|`6`|`C++14 (gcc9.3.0 amd64)`|
|`7`|`C++14 O2 (gcc9.3.0 amd64)`|
|`8`|`C++17 (gcc9.3.0 amd64)`|
|`9`|`C++17 O2 (gcc9.3.0 amd64)`|
|`10`|`C++20 (gcc9.3.0 amd64)`|
|`11`|`C++20 O2 (gcc9.3.0 amd64)`|
|`12`|`C89 (gcc9.3.0 amd64)`|
|`13`|`C89 O2 (gcc9.3.0 amd64)`|
|`14`|`C90 (gcc9.3.0 amd64)`|
|`15`|`C90 O2 (gcc9.3.0 amd64)`|
|`16`|`C99 (gcc9.3.0 amd64)`|
|`17`|`C99 O2 (gcc9.3.0 amd64)`|
|`18`|`C11 (gcc9.3.0 amd64)`|
|`19`|`C11 O2 (gcc9.3.0 amd64)`|
|`20`|`C17 (gcc9.3.0 amd64)`|
|`21`|`C17 O2 (gcc9.3.0 amd64)`|
|`22`|`C18 (gcc9.3.0 amd64)`|
|`23`|`C18 O2 (gcc9.3.0 amd64)`|
|`24`|`C20 (gcc9.3.0 amd64)`|
|`25`|`C20 O2 (gcc9.3.0 amd64)`|
|`26`|`Pascal (fpc3 amd64)`|
|`27`|`jdk8 (openjdk-8 amd64)`|
|`28`|`jdk11 (openjdk-11 amd64)`|
|`29`|`jdk13 (openjdk-13 amd64)`|
|`30`|`jdk16 (openjdk-16 amd64)`|
|`31`|`jdk17 (openjdk-17 amd64)`|
|`32`|`php7.4 (php7.4 amd64)`|
|`33`|`php8.1 (php8.1 amd64)`|
|`34`|`Python2 (python2 amd64)`|
|`35`|`Python3 (python3 amd64)`|

-----

#### 题目难度

|题目难度代码|含义|
|:-:|:-:|
|`0`|暂无评定|
|`1`|入门|
|`2`|普及-|
|`3`|普及/提高-|
|`4`|普及+/提高|
|`5`|提高+/省选-|
|`6`|省选/NOI-|
|`7`|NOI/NOI+/CTSC|

### 题目相关 API

-----

#### 获取一道题目的基本信息

```bash
GET /api/problem/info.php
```

**参数**

|变量名|类型|必要性|含义|备注|
|:-:|:-:|:-:|:-:|:-:|
|`pid`|num|必需|题目id|-|

**返回值**

|字段|类型|内容|备注|
|:-:|:-:|:-:|:-:|
|`id`|num|题目id|-|
|`name`|string|题目标题|-|
|`bg`|string|题目背景 markdown|-|
|`input`|string|输入格式 markdown|-|
|`output`|string|输出格式 markdown|-|
|`cases`|string|样例文件 JSON|-|
|`hint`|string|题目提示 markdown|-|
|`hidden`|bool|题目是否隐藏|-|
|`banned`|bool|0|-|
|`difficult`|num|题目难度|-|
|`contest`|num|所属比赛 id|-|
|`accepted`|bool|通过状态|未登录时始终为 `0`|

-----

#### 获取题目配置内容

```bash
GET /api/problem/config.php
```

**参数**

|变量名|类型|必要性|含义|备注|
|:-:|:-:|:-:|:-:|:-:|
|`pid`|num|必需|题目id|-|

**返回值**

|字段|类型|内容|备注|
|:-:|:-:|:-:|:-:|
|`input`|string|输入文件名|`stdin`表示标准输入|
|`output`|string|输出文件名|`stdout`表示标准输出|
|`spj`|obj|Special Judge 信息|-|
|`data`|array|数据点信息|-|
|`subtask_depend`|array|子任务依赖信息|-|

`spj` 字段: 

|字段|类型|内容|备注|
|:-:|:-:|:-:|:-:|
|`type`|num|Special Judge 类型|`0` 表示自定义 SPJ|
|`source`|string|SPJ 源文件名|当 `type` 为 `0` 时才有效|
|`compile_cmd`|string|SPJ 编译指令|当 `type` 为 `0` 时才有效|
|`exec_path`|string|SPJ 可执行文件名|当 `type` 为 `0` 时才有效|
|`exec_name`|string|SPJ 可执行文件名|与 `exec_path` 的值相等，当 `type` 为 `0` 时才有效|
|`exec_param`|string|SPJ 额外运行参数|无论 `type` 为多少都有效|

`data` 数组:

|项|类型|内容|备注|
|:-:|:-:|:-:|:-:|
|`0`|obj|数据点 `#1`|-|
|`n`|obj|数据点 `#n+1`|-|
|...|obj|...|...|

`data` 数组中的对象: 

|字段|类型|内容|备注|
|:-:|:-:|:-:|:-:|
|`input`|string|输入文件|-|
|`output`|string|输出文件|-|
|`score`|num|测试点分数|-|
|`time`|num|测试点时间限制|-|
|`memory`|num|测试点空间限制|-|
|`subtask`|num|子任务编号|-|

`subtask_depend` 数组: 

|项|类型|内容|备注|
|:-:|:-:|:-:|:-:|
|`0`|array|子任务 `#1` 依赖|-|
|`n`|array|子任务 `#n+1` 依赖|-|
|...|array|...|...|

`subtask_depend` 中的数组:

|项|类型|内容|备注|
|:-:|:-:|:-:|:-:|
|`0`|num|子任务 `#i` 依赖 `#1`|-|
|`n`|num|子任务 `#i` 依赖 `#n+1`|-|
|...|num|...|...|

-----

#### 下载附加文件

```bash
GET /api/problem/addition.php
```

**参数**

|变量名|类型|必要性|含义|备注|
|:-:|:-:|:-:|:-:|:-:|
|`pid`|num|必要|题目id|-|
|`name`|string|必要|附加文件名称|-|

**返回值**

本 API 不返回 JSON，直接返回下载头

-----

#### 提交代码

```bash
POST /api/problem/submit.php
```

**参数**

|变量名|类型|必要性|含义|备注|
|:-:|:-:|:-:|:-:|:-:|
|`pid`|num|必要|题目id|-|
|`code`|string|必要|代码|-|
|`lang`|num|必要|语言id|具体见 [语言代码选项](#语言代码)|

**返回值**

|字段|类型|内容|备注|
|:-:|:-:|:-:|:-:|
|`id`|num|评测 id|-|
|`lang`|num|提交语言|-|
|`code`|string|提交代码|-|

-----

#### 新建一道题目

```bash
POST /api/problem/create.php
```

**参数**

|变量名|类型|必要性|含义|备注|
|:-:|:-:|:-:|:-:|:-:|
|`file`|string|必要|数据包 base64|-|
|`title`|string|非必要|题目名称|-|
|`background`|string|非必要|题目背景|-|
|`description`|string|非必要|题目描述|-|
|`input`|string|非必要|输入描述|-|
|`output`|string|非必要|输出描述|-|
|`input-file`|string|非必要|指定输入文件|`stdin` 表示标准输入|
|`output-file`|string|非必要|指定输出文件|`stdout` 表示标准输出|
|`cases`|string|非必要|样例 JSON|-|
|`hint`|string|非必要|题目提示|-|
|`tags`|string|非必要|题目标签|以 `,` 为分隔符|
|`contest`|num|非必要|题目所属比赛|`0` 为不属于任何比赛|
|`difficulty`|num|非必要|题目难度|具体见 [题目难度选项](#题目难度)|

**返回值**

|字段|类型|内容|备注|
|:-:|:-:|:-:|:-:|
|`id`|num|题目 id|-|
|`title`|string|题目名称|-|
|`background`|string|题目背景|-|
|`description`|string|题目描述|-|
|`input-file`|string|输入文件|`stdin` 表示标准输入|
|`output-file`|string|输出文件|`stdout` 表示标准输出|
|`input`|string|输入描述|-|
|`output`|string|输出描述|-|
|`cases`|string|题目样例 JSON|-|
|`tags`|string|题目标签|以 `,` 为分隔符|
|`contest`|num|题目所属比赛|`0` 表示不属于任何比赛|
|`difficulty`|num|题目难度|具体见 [题目难度选项](#题目难度)|

-----

#### 隐藏/显示一道题目

```bash
POST /api/problem/hidden.php
```

**参数**

|变量名|类型|必要性|含义|备注|
|:-:|:-:|:-:|:-:|:-:|
|`pid`|num|必要|题目 id|-|

**返回值**

|字段|类型|内容|备注|
|:-:|:-:|:-:|:-:|
|`id`|num|题目 id|-|
|`hidden`|bool|当前题目状态|`0` 为显示，`1` 为隐藏|

-----

#### 重测整题

```bash
POST /api/problem/rejudge.php
```

**参数**

|变量名|类型|必要性|含义|备注|
|:-:|:-:|:-:|:-:|:-:|
|`pid`|num|必要|题目 id|-|

**返回值**

|字段|类型|内容|备注|
|:-:|:-:|:-:|:-:|
|`id`|num|题目 id|-|

-----

#### 修改一道题目

```bash
POST /api/problem/update.php
```

**参数**

|变量名|类型|必要性|含义|备注|
|:-:|:-:|:-:|:-:|:-:|
|`pid`|num|必要|题目 id|-|
|`title`|string|非必要|题目名称|为空表示不修改|
|`background`|string|非必要|题目背景|为空表示不修改|
|`description`|string|非必要|题目描述|为空表示不修改|
|`input`|string|非必要|输入描述|为空表示不修改|
|`output`|string|非必要|输出描述|为空表示不修改|
|`input-file`|string|非必要|指定输入文件|为空表示不修改，`stdin` 表示标准输入|
|`output_file`|string|非必要|指定输出文件|为空表示不修改，`stdout` 表示标准输出|
|`cases`|string|非必要|题目样例 JSON|为空表示不修改|
|`hint`|string|非必要|题目提示|为空表示不修改|
|`data`|string|非必要|题目测试点配置 JSON|该 JSON 包含四个数组，分别为 `time`,`memory`,`score`,`subtask`，要求每个数组的大小必须与数组组数相同，否则会报错|
|`subtask_depenedence`|string|非必要|题目子任务依赖|-|
|`difficulty`|num|非必要|题目难度|具体见 [题目难度选项](#题目难度)|
|`contest`|num|非必要|题目所属比赛|`0` 表示不属于任何比赛|
|`tags`|string|非必要|题目标签|以 `,` 为分隔符|
|`spj_type`|num|非必要|SPJ 类型|`0` 为自定义 SPJ|
|`spj_source`|string|非必要|SPJ 源文件名|当 `spj_type` 为 `0` 才有效|
|`spj_compile`|string|非必要|SPJ 编译参数|当 `spj_type` 为 `0` 才有效|
|`spj_name`|string|非必要|SPJ 可执行文件名|当 `spj_type` 为 `0` 才有效|
|`spj_param`|string|非必要|SPJ 执行参数|-|

**返回值**

|字段|类型|内容|备注|
|:-:|:-:|:-:|:-:|
|`id`|num|题目 id|-|
|`title`|string|题目名称|-|
|`background`|string|题目背景|-|
|`description`|string|题目描述|-|
|`input-file`|string|输入文件|`stdin` 表示标准输入|
|`output-file`|string|输出文件|`stdout` 表示标准输出|
|`input`|string|输入描述|-|
|`output`|string|输出描述|-|
|`cases`|string|题目样例 JSON|-|
|`hint`|string|题目提示|-|
|`tags`|string|题目标签|以 `,` 为分隔符|
|`contest`|num|题目所属比赛|`0` 表示不属于任何比赛|
|`difficulty`|num|题目难度|具体见 [题目难度选项](#题目难度)|

-----

#### 重传题目数据

```bash
POST /api/problem/upload.php
```

**参数**

|变量名|类型|必要性|含义|备注|
|:-:|:-:|:-:|:-:|:-:|
|`file`|string|必要|数据包 base64|-|
|`pid`|num|必要|题目 id|-|

**返回值**

|字段|类型|内容|备注|
|:-:|:-:|:-:|:-:|
|`id`|num|题目 id|-|

-----

#### 下载题目数据

```bash
GET /api/problem/download.php
```

**参数**

|变量名|类型|必要性|含义|备注|
|:-:|:-:|:-:|:-:|:-:|
|`pid`|num|必要|题目 id|-|

**返回值**

本 API 不返回 JSON，直接返回下载头

-----

#### 上传题目附加文件

```bash
POST /api/problem/upload2.php
```

**参数**

|变量名|类型|必要性|含义|备注|
|:-:|:-:|:-:|:-:|:-:|
|`file`|string|必要|文件 base64|-|
|`pid`|num|必要|题目 id|-|
|`name`|string|必要|文件名|-|

**返回值**

|字段|类型|内容|备注|
|:-:|:-:|:-:|:-:|
|`id`|num|题目 id|-|
|`absolute_path`|string|文件绝对路径|-|
|`download_path`|string|文件下载路径|-|

-----

#### 删除题目附加文件

```bash
POST /api/problem/delete2.php
```

**参数**

|变量名|类型|必要性|含义|备注|
|:-:|:-:|:-:|:-:|:-:|
|`pid`|num|必要|题目 id|-|
|`name`|string|必要|文件名|-|

**返回值**

|字段|类型|内容|备注|
|:-:|:-:|:-:|:-:|
|`id`|num|题目 id|-|

-----

#### 删除题目

```bash
POST /api/problem/delete.php
```

**参数**

|变量名|类型|必要性|含义|备注|
|:-:|:-:|:-:|:-:|:-:|
|`pid`|num|必要|题目 id|-|

**返回值**

|字段|类型|内容|备注|
|:-:|:-:|:-:|:-:|
|`id`|num|题目 id|-|

### 提交记录相关 API

-----

#### 获取提交记录信息

```bash
GET /api/status/info.php
```

**参数**

|变量名|类型|必要性|含义|备注|
|:-:|:-:|:-:|:-:|:-:|
|`id`|num|必要|评测 id|-|

**返回值**

|字段|类型|内容|备注|
|:-:|:-:|:-:|:-:|
|`id`|num|评测 id|-|
|`uid`|num|提交用户 id|-|
|`pid`|num|提交题目|-|
|`lang`|num|提交语言|-|
|`code`|string|提交代码|-|
|`result`|string|评测结果 JSON|-|
|`time`|num|提交时间|-|
|`status`|string|评测状态|若评测完成直接返回评测最终状态|
|`ideinfo`|string|NULL|-|
|`judged`|bool|是否评测完成|-|
|`contest`|num|提交所属比赛|-|

-----

#### 获取评测状态 (不含各测试点状态)

```bash
GET /api/status/status.php
```

**参数**

|变量名|类型|必要性|含义|备注|
|:-:|:-:|:-:|:-:|:-:|
|`id`|num|必要|评测 id|-|

**返回值**

|字段|类型|内容|备注|
|:-:|:-:|:-:|:-:|
|`id`|num|评测 id|-|
|`result`|string|评测状态|-|

-----

#### 获取评测状态 (含各评测点状态)

```bash
GET /api/status/result.php
```

**参数**

|变量名|类型|必要性|含义|备注|
|:-:|:-:|:-:|:-:|:-:|
|`id`|num|必要|评测 id|-|

**返回值**

|字段|类型|内容|备注|
|:-:|:-:|:-:|:-:|
|`id`|num|评测 id|-|
|`compile_info`|string|编译信息|-|
|`info`|array|各评测点信息|-|
|`memory`|num|总内存信息|-|
|`time`|num|总时间信息|-|
|`result`|string|最终评测状态|-|

`info` 数组:

|项|类型|内容|备注|
|:-:|:-:|:-:|:-:|
|`0`|obj|数据点 `#1`|-|
|`n`|obj|数据点 `#n+1`|-|
|...|obj|...|...|

`info` 数组中的对象: 

|字段|类型|内容|备注|
|:-:|:-:|:-:|:-:|
|`state`|string|评测点状态|-|
|`info`|string|评测点测试信息|-|
|`memory`|num|评测点内存使用|-|
|`time`|num|评测点时间使用|-|
|`score`|num|评测点得分|-|

-----

#### 重测一次提交

```bash
POST /api/status/rejudge.php
```

**参数**

|变量名|类型|必要性|含义|备注|
|:-:|:-:|:-:|:-:|:-:|
|`id`|num|必要|评测 id|-|

**返回值**

本 API 返回值为空

### 比赛相关 API

-----

#### 获取一场比赛信息

```bash
GET /api/contest/info.php
```

**参数**

|变量名|类型|必要性|含义|备注|
|:-:|:-:|:-:|:-:|:-:|
|`id`|num|必要|比赛 id|-|

**返回值**

|字段|类型|内容|备注|
|:-:|:-:|:-:|:-:|
|`id`|num|比赛 id|-|
|`title`|string|比赛名称|-|
|`starttime`|num|比赛开始时间戳|-|
|`duration`|num|比赛时长|-|
|`type`|num|比赛类型|`0` 为 `OI` 赛制，`1` 为 `IOI` 赛制，`2` 为 `ACM` 赛制|
|`rated`|bool|是否记录积分|-|
|`problem`|array|包含题目|比赛未结束时无此字段|

`problem` 数组:

|项|类型|内容|备注|
|:-:|:-:|:-:|:-:|
|`0`|num|第 `1` 题题目编号|-|
|`n`|num|第 `n` 题题目编号`|-|
|...|num|...|...|

-----

#### 注册一场比赛

```bash
POST /api/contest/signup.php
```

**参数**

|变量名|类型|必要性|含义|备注|
|:-:|:-:|:-:|:-:|:-:|
|`id`|num|必要|比赛 id|-|

**返回值**

|字段|类型|内容|备注|
|:-:|:-:|:-:|:-:|
|`id`|num|比赛 id|-|
|`title`|string|比赛名称|-|
|`starttime`|num|比赛开始时间戳|-|
|`duration`|num|比赛时长|-|
|`type`|num|比赛类型|`0` 为 `OI` 赛制，`1` 为 `IOI` 赛制，`2` 为 `ACM` 赛制|
|`rated`|bool|是否记录积分|-|
|`problem`|array|包含题目|比赛未结束时无此字段|

`problem` 数组:

|项|类型|内容|备注|
|:-:|:-:|:-:|:-:|
|`0`|num|第 `1` 题题目编号|-|
|`n`|num|第 `n` 题题目编号`|-|
|...|num|...|...|

-----

#### 获取比赛排名

```bash
GET /api/contest/rank.php
```

**参数**

|变量名|类型|必要性|含义|备注|
|:-:|:-:|:-:|:-:|:-:|
|`id`|num|必要|比赛 id|-|

**返回值**

本 API 不返回 JSON，直接返回 HTML 代码

### 用户相关 API

-----

#### 更新用户个人介绍

```bash
POST /api/user/intro.php
```

**参数**

|变量名|类型|必要性|含义|备注|
|:-:|:-:|:-:|:-:|:-:|
|`intro`|string|必要|intro 内容|-|

**返回值** 

|字段|类型|内容|备注|
|:-:|:-:|:-:|:-:|
|`uid`|num|用户 id|-|
|`intro`|string|用户个人介绍|-|

-----

#### 更新用户头像

```bash
POST /api/user/header.php
```

**参数**

|变量名|类型|必要性|含义|备注|
|:-:|:-:|:-:|:-:|:-:|
|`data`|string|必要|文件 base64|-|

**返回值**

|字段|类型|内容|备注|
|:-:|:-:|:-:|:-:|
|`uid`|num|用户 id|-|
|`url`|string|文件路径|-|

-----

#### 更新用户空间头图

```bash
POST /api/user/background.php
```

**参数**

|变量名|类型|必要性|含义|备注|
|:-:|:-:|:-:|:-:|:-:|
|`data`|string|必要|文件 base64|-|

**返回值**

|字段|类型|内容|备注|
|:-:|:-:|:-:|:-:|
|`uid`|num|用户 id|-|
|`url`|string|文件路径|-|

### 登录相关 API

-----

#### 获取公钥

```bash
GET /api/login/public.php
```

**参数**

本 API 请求参数为空

**返回值**

|字段|类型|内容|备注|
|:-:|:-:|:-:|:-:|
|`key`|string|登录公钥|-|

-----

#### 获取盐值

```bash
GET /api/user/salt.php
```

**参数**

|变量名|类型|必要性|含义|备注|
|:-:|:-:|:-:|:-:|:-:|
|`email`|string|必要|用户邮箱|-|


**返回值**

|字段|类型|内容|备注|
|:-:|:-:|:-:|:-:|
|`uid`|num|用户 id|-|
|`salt`|string|用户盐值|-|

-----

#### 密码登录

```bash
POST /api/login/password.php
```

**参数**

|变量名|类型|必要性|含义|备注|
|:-:|:-:|:-:|:-:|:-:|
|`email`|string|必要|用户邮箱|-|
|`password`|string|必要|加密后的用户密码|-|

**返回值**

|字段|类型|内容|备注|
|:-:|:-:|:-:|:-:|
|`user`|obj|用户信息|-|
|`DedeUserID`|string|用户 id|-|
|`DedeUserID__ckMd5`|string|用户 id 的 md5 值|-|
|`CSRF_TOKEN`|string|身份验证代码|-|
|`SESSDATA`|string|身份验证代码|-|

`user` 对象: 

|字段|类型|内容|备注|
|:-:|:-:|:-:|:-:|
|`id`|num|用户 id|-|
|`name`|string|用户名|-|
|`title`|string||-|
|`permission`|string|权限|-|
|`email`|string|用户邮箱|-|
|`verify`|bool|是否通过邮箱验证|-|
|`rp`|num|rp值|-|
|`rptime`|num|上次更新 rp 时间戳|-|

-----

#### 注册账号

```bash
POST /api/user/register.php
```

**参数**

|变量名|类型|必要性|含义|备注|
|:-:|:-:|:-:|:-:|:-:|
|`name`|string|必要|用户名|-|
|`email`|string|必要|用户邮箱|-|
|`passwd`|string|必要|加密后的用户密码|-|

**返回值**

|字段|类型|内容|备注|
|:-:|:-:|:-:|:-:|
|`id`|num|用户 id|-|
|`name`|string|用户名|-|
|`title`|string||-|
|`permission`|string|权限|-|
|`email`|string|用户邮箱|-|
|`verify`|bool|是否通过邮箱验证|-|
|`rp`|num|rp值|-|
|`rptime`|num|上次更新 rp 时间戳|-|

### 后台管理 API

-----

### 工具类 API

-----

#### 核验登录态

```bash
GET /api/tool/checklogin.php
```

**参数**

本 API 请求参数为空

**返回值**

|字段|类型|内容|备注|
|:-:|:-:|:-:|:-:|
|`DedeUserID`|string|从 COOKIE 获取到的用户 id|-|
|`DedeUserID__ckMd5`|string|从 COOKIE 获取到的用户 id 的 md5|-|
|`CSRF_TOKEN`|string|从 COOKIE 获取到的 CSRF 身份验证代码|-|
|`SESSDATA`|string|从 COOKIE 获取到的 SESSDATA 身份验证代码|-|
|`login`|bool|核验结果|`0` 为无效的登录态，`1` 为有效的登录态|
|`user`|obj|用户信息|当 `login` 为 `0` 时无此字段|

`user` 对象: 

|字段|类型|内容|备注|
|:-:|:-:|:-:|:-:|
|`id`|num|用户 id|-|
|`name`|string|用户名|-|
|`title`|string||-|
|`permission`|string|权限|-|
|`email`|string|用户邮箱|-|
|`verify`|bool|是否通过邮箱验证|-|
|`rp`|num|rp值|-|
|`rptime`|num|上次更新 rp 时间戳|-|

-----

#### SHA256 加密

```bash
POST /api/tool/crypt.php
```

**参数**

|变量名|类型|必要性|含义|备注|
|:-:|:-:|:-:|:-:|:-:|
|`data`|string|必要|要加密的数据|-|
|`key`|string|必要|公钥|-|

**返回值**

|字段|类型|内容|备注|
|:-:|:-:|:-:|:-:|
|`result`|string|加密结果|-|