#mposp接口规范
> **Beta:**
> 该API仍处于 Beta 阶段

```
1. 该接口适用对象：中汇自有APP
2. 该接口实现功能：用户收单理财
3. 该接口调用规范：采用HTTP请求与中汇的前置POSP进行通信
```
> **注：**
> 文中所有 `<>` 标注的字段，均需根据你的实际情况替换（无需 `<>` 符号，仅作标注之用）
> 文中所有 `:id` 标注的字段，均需根据该资源的实际 `id` 值替换
> 文中所有 `{x|y|...}` 标注的字段，均需根据你的实际情况用其中一个 `x` 或者 `y`（ `|` 分割）替换

## API 接口地址
```
暂无 # 生产环境
http://mposp.21er.tk # 测试环境
```

## 标准请求
```sh
curl -X POST \
    http://mposp.21er.tk/<资源路径> \
    # 其他可选参数，参数以键值对呈现...
```

## 标准响应
* 订单校验通过的情况下  
```
HTTP/1.1 200 OK
Server: Nginx
Date: Thu, 09 Apr 2015 11:36:53 GMT
Content-Type: application/json; charset=utf-8
Connection: keep-alive
Cache-Control: no-cache
Content-Length: 100

...body...
```

* 订单校验未通过的情况下  
```
HTTP/1.1 401 Unauthorized
```
* 请求 Method 不被支持的情况下  
```
HTTP/1.1 405 Method Not Allowed
```
* 请求参数不正确的情况下  
```
HTTP/1.1 403 Forbidden
```

## 功能路径列表
| 资源名称     | 路径                                     | Content-Type         | 请求方式     |
|-------------|-----------------------------------------|----------------------|---------------|
| 获取验证码| [/sendMobileMessage](#sendMobileMessage)                      | urlencoded           | POST   |
| 登录| [/login](#login)                      | urlencoded           | GET      |
| 注册| [/register](#register)                      | urlencoded           | POST   |
| 激活绑定设备| [/activeAndBindEquip](#activeAndBindEquip)                      | urlencoded           | POST   |

  
----------------------------------------------------------------------------------
<a id="sendMobileMessage"></a>
### 获取验证码  /sendMobileMessage
#### 1\. 通过手机号获取验证码
请求：  
```
POST /sendMobileMessage HTTP/1.1
Host: mposp.21er.tk
Date: Wed, 8 Apr 2015 15:51 GMT
Content-Type: application/x-www-form-urlencoded; charset=utf-8
Content-Length: 30

{
    "reqTime": "20151125160124",
    "mobile": "15801376995",
    "appVersion": "设备名.系统名.系统版本号"
}
```
响应：  
```
HTTP/1.1 200 OK
Server: Nginx
Date: Thu, 09 Apr 2015 11:36:53 GMT
Content-Type: application/json; charset=utf-8
Connection: keep-alive
Cache-Control: no-cache
Content-Length: 100

{
   "respTime":"20151125161740",
   "isSuccess":true,
   "respCode":"SUCCESS",
   "respMsg":"发送验证码成功,注意查收",
   "cookie":{
        "name":"idCode",
        "value":"193286617aaa4285810d13ac56e0fd61",
        "comment":null,
        "domain":null,
        "maxAge":-1,
        "path":null,
        "secure":false,
        "version":0,
        "httpOnly":false
    }
}
```

<a id="login"></a>
### 登录  /login
#### 1\. 手机号登录
请求：  
```
POST /login HTTP/1.1
Host: mposp.21er.tk
Date: Wed, 8 Apr 2015 15:51 GMT
Content-Type: application/x-www-form-urlencoded; charset=utf-8
Content-Length: 30

{
    "reqTime": "20151125160124",
    "loginName": "张珊",
    "password": "123456",
    "position": "117.194778,39.113809",
    "appVersion": "设备名.系统名.系统版本号"
}
```
响应：  
```
HTTP/1.1 200 OK
Server: Nginx
Date: Thu, 09 Apr 2015 11:36:53 GMT
Content-Type: application/json; charset=utf-8
Connection: keep-alive
Cache-Control: no-cache
Content-Length: 100

{
  
}
```

<a id="register"></a>
### 注册  /register
#### 1\. 通过手机号注册
请求：  
```
POST /register HTTP/1.1
Host: mposp.21er.tk
Date: Wed, 8 Apr 2015 15:51 GMT
Content-Type: application/x-www-form-urlencoded; charset=utf-8
Content-Length: 30

{
    "reqTime": "20151125160124",
    "mobile": "张三",
    "password": "12345",
    "appVersion": "设备名.系统名.系统版本号"
}
```
响应：  
```
HTTP/1.1 200 OK
Server: Nginx
Date: Thu, 09 Apr 2015 11:36:53 GMT
Content-Type: application/json; charset=utf-8
Connection: keep-alive
Cache-Control: no-cache
Content-Length: 100

{
  
}
```

<a id="activeAndBindEquip"></a>
### 激活绑定设备  /activeAndBindEquip
#### 1\. 激活绑定设备
请求：  
```
POST /activeAndBindEquip HTTP/1.1
Host: mposp.21er.tk
Date: Wed, 8 Apr 2015 15:51 GMT
Content-Type: application/x-www-form-urlencoded; charset=utf-8
Content-Length: 30

{
    "reqTime": "20151125160124",
    "ksnNo": "5010100000023402",
    "mobile": "15801376995",
    "activeCode": "11C718FF1FD14531",
    "product": "mobile_v1",
    "appVersion": "设备名.系统名.系统版本号"
}
```
响应：  
```
HTTP/1.1 200 OK
Server: Nginx
Date: Thu, 09 Apr 2015 11:36:53 GMT
Content-Type: application/json; charset=utf-8
Connection: keep-alive
Cache-Control: no-cache
Content-Length: 100

{
  
}
```
