# RESTful API 设计规范

---

### 1、协议

使用Https协议。



---

### 2、域名

应该尽量将API部署在专用域名之下：

https://api.example.com

将API的版本号放入URL：

https://api.example.com/v1/

---

### 3、路径

表示API的具体网址。在RESTful架构中，每个网址代表一种资源（resource），所以网址中不能有动词，只能有名词，而且所用的名词往往与数据库的表格名对应。

举例说明：

- <https://api.example.com/v1/zoos>
- <https://api.example.com/v1/animals>
- https://api.example.com/v1/employees



---

### 4、HTTP动词

常用的HTTP动词有下面五个（括号里是对应的SQL命令）：

1. GET（SELECT）：从服务器取出资源（一项或多项）。 
2. POST（CREATE）：在服务器新建一个资源。  
3. PUT（UPDATE）：在服务器更新资源（客户端提供改变后的完整资源）。
4.  PATCH（UPDATE）：在服务器更新资源（客户端提供改变的属性）。  
5. DELETE（DELETE）：从服务器删除资源。

举例说明：

- 获取所有任务：GET/missions；
- 注册：POST/register;
- 删除任务：DELETE/missions;
- 修改个人信息：PUT/user。

注：GET方法和查询参数不能改变资源状态。



------

### 5、避免层级过深的URI

`在url中表达层级，用于按实体关联关系进行对象导航，一般根据id导航。

过深的导航容易导致url膨胀，不易维护，如 `GET /zoos/1/areas/3/animals/4`，尽量使用查询参数代替路劲中的实体导航，如`GET /user?uid=1&password=3`。



---

### 6、过滤、排序、选择信息

##### 6.1 过滤

​	API应该提供参数，过滤返回结果。

##### 6.2 排序

​	API允许针对多个字段排序。

##### 6.3 选择

​	有时候API使用者不需要所有的结果，在进行横向限制的时候（例如值返回API结果的前十项）还应该可以进行纵向限制。



---

### 7、使用Http头声明序列化格式

使用Http头声明序列化格式。在客户端和服务端，双方都要知道通讯的格式，格式在HTTP-Header中指定：

- Content-Type 定义请求格式。  

- Accept 定义系列可接受的响应格式。

---

### 8、状态码

服务器向用户返回的状态码和提示信息，常见的有以下一些（方括号中是该状态码对应的HTTP动词）。

- 200 – OK – 一切正常  201 – OK – 新的资源已经成功创建 。
- 204 – OK – 资源已经成功擅长  304 – Not Modified – 客户端使用缓存数据 。 
- 400 – Bad Request – 请求无效，需要附加细节解释如 "JSON无效"  。
- 401 – Unauthorized – 请求需要用户验证  。
- 403 – Forbidden – 服务器已经理解了请求，但是拒绝服务或这种请求的访问是不允许的。  
- 404 – Not found – 没有发现该资源 。 
- 422 – Unprocessable Entity – 只有服务器不能处理实体时使用，比如图像不能被格式化，或者重要字段丢失。  
- 500 – Internal Server Error – API开发者应该避免这种错误。

更新和创建操作应该返回对应的状态码，防止用户多次的API调用。



---

### 9、错误处理

如果状态码是4xx，就应该向用户返回出错信息。一般来说，返回的信息中将error作为键名，出错信息作为键值即可。 使用详细的错误包装错误：

```json
{
  "errors": [
   {
    "userMessage": "Sorry, the requested resource does not exist",
    "internalMessage": "No car found in the database",
    "code": 34,
    "more info": "http://dev.mwaysolutions.com/blog/api/v1/errors/12345"
   }
  ]
}
```



---

### 10、返回结果

##### 10.1 Response不要包装

response 的 body直接就是数据，不要做多余的包装。错误实例：

```json
{     
	"success":true,     
	"data":{"id":1, "name":"xiaotuan"} 
}
```

##### 10.2 结果规范

- GET /collection：返回资源对象的列表（数组）  
- GET /collection/resource：返回单个资源对象  
- POST /collection：返回新生成的资源对象  
- PUT /collection/resource：返回完整的资源对象  
- PATCH /collection/resource：返回完整的资源对象  
- DELETE /collection/resource：返回一个空文档



---

### 11、Hypermedia API

RESTful API最好做到Hypermedia，即返回结果中提供链接，连向其他API方法，使得用户不查文档，也知道下一步应该做什么。  

比如，当用户向api.example.com的根目录发出请求，会得到这样一个文档：

```json
{"link":{
  "rel":  "collection https://www.example.com/zoos",
  "href": "https://api.example.com/zoos",
  "title":"List of zoos",
  "type": "application/vnd.yourformat+json"
}}
```



---

### 12、基于验证的缓存  

不要在服务端存储应用状态：

- RESTful HTTP的交互必须是无状态的，这表明每一次请求要包含处理该请求所需的一切信息，每一次请求都应该包含鉴权证明。  

- 客户端负责维护应用状态，RESTful服务端不需要在请求间保留应用状态，服务端负责维护资源状态而不是应用状态。  

- 通过使用ssl我们可以不用每次都提供用户名和密码：我们可以给用户返回一个随机产生的token。 
-  这样可以极大的方便使用浏览器访问API的用户。  
- 这种方法适用于用户可以首先通过一次用户名-密码的验证并得到token，并且可以拷贝返回的token到以后的请求中。  
- 如果不方便，可以使用OAuth 2来进行token的安全传输。



---

### 13、其他

1. 数据类型尽量使用JSON，避免使用XML。





