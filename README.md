# 第四题技术文档

### 1 整体框架

主要思路是第一个接口的识别码通过redis的查找对比来实现，查找是否有该key值即可。玩家信息存储mongo数据库，先连接mongo数据库，玩家信息以mongodb的集合方式存入mongodb数据库。

### 2 目录结构

![image-20210719113803673](/Users/fuyuanfu/Library/Application Support/typora-user-images/image-20210719113803673.png)

### 3 代码逻辑分层

应用层：/app/http/http.go   /app/start       调用路由层，启动进程。

控制层： /internal/ctrl        请求参数验证，处理请求后构造回复信息。

handler层：/internal/handler   处理具体业务 不可同层调用 被控制层调用

模型层：/internal/model  数据模型，操作数据库。

路由层：/internal/router 路由转发 

service层：/internal/service 通用业务逻辑，可同层调用

### 4 存储设计

| ***\*内容\****                     | ***\*数据库\****  | ***\*key\**** | ***\*类型\****  |
| ---------------------------------- | ----------------- | ------------- | --------------- |
| ***\*name\****                     | ***\*mongodb\**** | ***\*UID\**** | ***\*table\**** |
| ***\*G\*******\*oldcoinnumber\**** | ***\*mongodb\**** | ***\*UID\**** | ***\*table\**** |
| ***\*D\*******\*iamondnumber\****  | ***\*mongodb\**** | ***\*UID\**** | ***\*table\**** |

### 5 接口设计

#### 请求方法

http post

#### 接口地址

Https://localhost:8080/register

#### 请求参数

一个识别码 一个字符串，类似：jrTn5htC 9Xf9GAx5 

#### 请求响应

生成一个UID 或者返回一个字符串：唯一UID，金币数，钻石数。

#### 请求状态码

| ***\*状态码\**** | ***\*说明\****               |
| ---------------- | ---------------------------- |
| ***\*无\****     | ***\*成功\****               |
| ***\*1001\****   | ***\*参数为空\****           |
| ***\*1002\****   | ***\*服务器内部错误\****     |
| ***\*1003\****   | ***\*参数含有非数字字符\**** |
| ***\*1004\****   | ***\*未找到指定目标\****     |

### 6.第三方库

google/protobuf/any.proto  

用于调用用protobuf的方法

### 7 编译执行

进入/app/start.go启动即可

### 8 todo

将代码判错性代码补充，提高代码强度

### 9 流程图

<img width="445" alt="第四题的流程图" src="https://user-images.githubusercontent.com/87068277/126103936-b08fcf13-4e71-4032-8763-8d512437a160.png">

<img width="336" alt="image-20210719144006692" src="https://user-images.githubusercontent.com/87068277/126114333-19143041-c8b5-44f3-93d4-ba133cbcf8d3.png">

