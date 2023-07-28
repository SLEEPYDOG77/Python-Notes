# Requests库

[Requests库文档](https://requests.readthedocs.io/en/master/)

## 简介





## 安装





## HTTP协议

#### HTTP

HTTP（Hypertext Transfer Protocol），超文本传输协议。

是一个基于 **请求与响应** 模式的、**无状态**的**应用层协议**。

采用 **URL** 作为定位网络资源的标识。



#### URL

##### 格式

```python
http://host[:port][path]

#host: 合法的Internet主机域名或IP地址
#port: 端口号，缺省端口为80
#path: 请求资源的路径
```

##### 实例

```python
http://www.bit.edu.cn
http://220.181.111.188/duty
```

##### 理解

URL是通过 HTTP 协议存取资源的 Internet 路径，一个URL对应一个数据资源。



#### HTTP协议对资源的操作

| 方法   | 说明                                                      |
| ------ | --------------------------------------------------------- |
| GET    | 请求获取URL位置的资源                                     |
| HEAD   | 请求获取URL位置资源的响应信息报告，即获得该资源的头部信息 |
| POST   | 请求向URL位置的资源后附加新的数据                         |
| PUT    | 请求向URL位置存储一个资源，覆盖原URL位置的资源            |
| PATCH  | 请求局部更新URL位置的资源，及改变该处资源的部分内容       |
| DELETE | 请求删除URL位置存储的资源                                 |

> HTTP协议通过URL和命令管理资源，操作独立五状态，网络通道及服务器成为了黑盒子。

> PUT和PATCH的区别：
>
> - 采用PATCH：仅向URL提交局部更新请求，节省网络带宽
> - 采用PUT：将全部字段一并提交到URL



## Requests库基础

#### Response对象

Response对象包含服务器返回的所有信息，也包含请求的Request信息。

##### 示例

```python
import requests
r = requests.get("http://www.baidu.com")
print(r.status_code)
#200
type(r)
#<class 'requests.models.Response'>
r.headers
#{'Cache-Control': 'private, no-cache, no-store, proxy-revalidate, no-transform', 'Connection': 'keep-alive', 'Content-Encoding': 'gzip', 'Content-Type': 'text/html', 'Date': 'Thu, 14 Jan 2021 06:44:51 GMT', 'Last-Modified': 'Mon, 23 Jan 2017 13:27:36 GMT', 'Pragma': 'no-cache', 'Server': 'bfe/1.0.8.18', 'Set-Cookie': 'BDORZ=27315; max-age=86400; domain=.baidu.com; path=/', 'Transfer-Encoding': 'chunked'}
```



##### 属性

| 属性                | 说明                                             |
| ------------------- | ------------------------------------------------ |
| r.status_code       | HTTP请求的返回状态，200 - 连接成功；404 - 失败。 |
| r.text              | HTTP响应内容的字符串形式，即 url 对应的页面内容  |
| r.encoding          | 从HTTP header中猜测的响应内容编码方式            |
| r.apparent_encoding | 从内容中分析出的响应内容编码方式（备选编码方式） |
| r.content           | HTTP响应内容的二进制形式                         |

> - r.status_code == 200时，连接成功
>   - 才能解析出 r.text / r.encoding / r.apparent_encoding / r.content 等内容
> - r.status_code == 404时，连接失败
>   - 某些原因出错，将产生异常



##### 编码

**r.encoding**

> 如果 header 中不存在charset，则认为编码为 `ISO-8859-1` ，r-text 则根据 r.encoding 显示网页内容

**r.apparent_encoding**

> 根据网页内容分析出的编码方式，可以看做是 r.encoding 的备选



#### 异常 Exception

| 异常                      | 说明                                          |
| ------------------------- | --------------------------------------------- |
| requests.ConnectionError  | 网络连接错误异常，如DNS查询失败、拒绝连接等。 |
| requests.HTTPError        | HTTP错误异常                                  |
| requests.URLRequired      | URL缺失异常                                   |
| requests.TooManyRedirects | 超过最大重定向次数，产生重定向异常            |
| requests.ConnectTimeout   | 连接远程服务器超时异常                        |
| requests.Timeout          | 请求URL超时，产生超时异常                     |

##### 异常判断 raise_for_status()

在方法内部判断 r.status_code 是否等于200，不需要增加额外的 if 语句，便于利用 try-except 进行异常处理。



#### 爬取网页的通用代码框架

```python
import requests

def getHTMLText(url):
    try:
        r = requests.get(url, timeout = 30)
        r.raise_for_status()
        r.encoding = r.apparent_encoding
        return r.text
    except:
        return "产生异常"
    
if __name__ = "__main__":
    url = "http://www.baidu.com"
    print(getHTMLText(url))
```



## Requests库的七个主要方法

| 方法               | 说明                                           | HTTP协议 |
| ------------------ | ---------------------------------------------- | -------- |
| requests.request() | 构造一个请求，支撑以下各方法的基础方法         |          |
| requests.get()     | 获取HTML网页的主要方法，对应于HTTP的GET        | GET      |
| requests.head()    | 获取HTML网页头信息的方法，对应于HTTP的HEAD     | HEAD     |
| requests.post()    | 向HTML网页提交POST请求的方法，对应于HTTP的POST | POST     |
| requests.put()     | 向HTML网页提交PUT请求的方法，对应于HTTP的PUT   | PUT      |
| requests.patch()   | 向HTML网页提交局部修改请求，对应于HTTP的PATCH  | PATCH    |
| requests.delete()  | 向HTML页面提交删除请求，对应于HTTP的DELETE     | DELETE   |



### 控制访问的参数

| 参数            | 说明                                           |
| --------------- | ---------------------------------------------- |
| params          | 字典或字节序列，作为参数增加到url中            |
| data            | 字典、字节序列或文件对象，作为Request的内容    |
| json            | JSON格式的数据，作为Request的内容              |
| headers         | 字典，HTTP定制头                               |
| cookies         | 字典或CookieJar，Request中的cookie             |
| auth            | 元组，支持HTTP认证功能                         |
| files           | 字典类型，传输文件                             |
| timeout         | 设定超时时间，秒为单位                         |
| proxies         | 字典类型，设定访问代理服务器，可以增加登录认证 |
| allow_redirects | 重定向开关，True/False，默认为True             |
| stream          | 获取内容立即下载开关，True/False，默认为True   |
| verify          | 认证SSL证书开关，True/False，默认为True        |
| cert            | 本地SSL证书路径                                |



### request()方法

> 构造一个请求，支撑以下各方法的基础方法。

```python
requests.request(method, url, **kwargs)
#method: 请求方式，对应get/put/post等7种
#url: 拟获取页面的url链接
#**kwargs: 控制访问的参数，共13个
```



### get()方法

> 获取HTML网页的主要方法，对应于HTTP的GET。

```python
r = requests.get(url)
#构造一个向服务器请求资源的Request对象
#返回一个包含服务器资源的Response对象
```

```python
requests.get(url, params=None, **kwargs)
#url: 拟获取页面的url链接
#params: url中的额外参数，字典或字节流格式（可选）
#**kwargs: 12个控制访问的参数
```



### head()方法

> 获取HTML网页头信息的方法，对应于HTTP的HEAD。

```python
requests.head(url, **kwargs)
#url: 拟获取页面的url链接
#**kwargs: 12个控制访问的参数
```



```python
import requests
r = requests.head("http://www.baidu.com")
r.headers
r.text
```



### post()方法

> 向HTML网页提交POST请求的方法，对应于HTTP的POST。

```python
requests.post(url, data=None, json=None, **kwargs)
#url: 拟获取页面的url链接
#data: 字典、字节序列或文件，Request的内容
#json: JSON格式的数据，Request的内容
#**kwargs: 12个控制访问的参数
```



1. **向URL POSt一个字典，自动编码为表单（form）**

```python
import requests
payload = {'key1':'value1', 'key2':'value2'}
r = requests.post('http://www.baidu.com/post', data = payload)
print(r.text)
#向URL POSt一个字典，自动编码为表单（form）
#{
#    "form":{
#        "key2":"value2",
#        "key1":"value1"
#    },
#}
```

2. **向URL POST一个字符串，自动编码为 data**

```python
import requests
r = requests.post('http://www.baidu.com/post', data = 'ABC')
print(r.text)
#向URL POST一个字符串，自动编码为 data
#{
#    "data":"ABC"
#    "form":{}
#}
```



### put()方法

> 向HTML网页提交PUT请求的方法，对应于HTTP的PUT。

```python
requests.put(url, data=None, **kwargs)
#url: 拟获取页面的url链接
#data: 字典、字节序列或文件，Request的内容
#**kwargs: 12个控制访问的参数
```



```python
import requests
payload = {'key1': 'value1', 'key2':'value2'}
r = requests.put('http://www.baidu.com/put', data = payload)
print(r.text)
#向URL PUT一个字典，自动编码为表单（form）
#{
#    "form":{
#        "key2":"value2",
#        "key1":"value1"
#    },
#}
```



### patch()方法

> 向HTML网页提交局部修改请求，对应于HTTP的PATCH。

```python
requests.patch(url, data=None, **kwargs)
#url: 拟获取页面的url链接
#data: 字典、字节序列或文件，Request的内容
#**kwargs: 12个控制访问的参数
```



### delete()方法

> 向HTML页面提交删除请求，对应于HTTP的DELETE

```python
requests.delete(url, **kwargs)
#url: 拟删除页面的url链接
#**kwargs: 12个控制访问的参数
```





## 实战案例

- 实例1：京东商品页面的爬取
- 实例2：亚马逊商品页面的爬取
- 实例3：百度/360搜索关键字提交
- 实例4：网络图片的爬取和存储
- 实例5：IP地址归属地的自动查询



### 实例1：京东商品页面的爬取

```python
import requests
url = "http://item.jd.com/2967929.html"
try:
    r = requests.get(url)
    r.raise_for_status()
    r.encoding = r.apparent_encoding
    print(r.text[:1000])
except:
    print("爬取失败")
```



### 实例2：亚马逊商品页面的爬取

```python
import requests
url = "http://www.amazon.cn/gp/product/B01M8L5Z3Y"
try:
    kv = {'user-agent':'Mozilla/5.0'}
    r = requests.get(url, headers = kv)
    r.raise_for_status()
    r.encoding = r.apparent_encoding
    print(r.text[1000:2000])
except:
    print("爬取失败")
```



### 实例3：百度/360搜索关键字提交

百度

```python
import requests
keyword = "Python"
try:
    kv = {'wd':keyword}
    r = requests.get("http://www.baidu.com/s", params = kv)
    print(r.request.url)
    r.raise_for_status()
    print(len(r.text))
except:
    print("爬取失败")
```

360

```python
import requests
keyword = "Python"
try:
    kv = {'q':keyword}
    r = requests.get("http://www.so.com/s", params = kv)
    print(r.request.url)
    r.raise_for_status()
    print(len(r.text))
except:
    print("爬取失败")
```



### 实例4：网络图片的爬取和存储

```python
import requests
import os
url = "http://image.nationalgeographic.com.cn/2017/0211/20170211061910157.jpg"
root = "D://pics//"
path = root + url.split('/')[-1]
try:
    if not os.path.exists(root):
        os.mkdir(root)
    if not os.path.exists(path):
        r = requests.get(url)
        with open(path, 'wb') as f:
            f.write(r.content)
            f.close()
            print("文件保存成功")
    else:
        print("文件已存在")
except:
    print("爬取失败")
```



### 实例5：IP地址归属地的自动查询

```python
import requests
url = "http://m.ip138.com/ip.asp?ip="
try:
    r = requests.get(url+'202.204.80.112')
    r.raise_for_status()
    r.encoding = r.apparent_encoding
    print(r.text[-500:])
except:
    print("爬取失败")
```

