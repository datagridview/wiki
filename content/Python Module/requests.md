---
title: "Requests"
date: 2017-08-17 11:36
updated: 2017-08-17 11:36
tag: Python Module
log: "官方解释"
---

官方网站：[Requests](http://docs.python-requests.org/zh_CN/latest/user/quickstart.html#id9)

## 会话

```python
s = requests.Session()

#一般样例
s.get(url, headers=headers, data=playload,\ 
		files=files, params=payload, \
		cookies=cookies, proxies=proxies, \
		verify=True, cert='/wrong_path/client.pem')
```

选项 `verify` 仅应用于主机证书

## GET发送请求

```python
>>> payload = {'key1': 'value1', 'key2': ['value2', 'value3']}

>>> r = requests.get('http://httpbin.org/get', params=payload)
>>> print(r.url)
http://httpbin.org/get?key1=value1&key2=value2&key2=value3
```

* Requests 允许你使用 `params` 关键字参数，以一个字符串字典来提供这些参数。
* 字典里值为 **`None`** 的键都不会被添加到 URL 的查询字符串里.

```python
>>> r.encoding
'utf-8'
>>> r.encoding = 'ISO-8859-1'
```

通过修改编码来重新对response进行编码。

* `r.text`返回编码过的数据
* `r.content`返回二进制字节文件
* `r.json()`返回json对象处理文件

```python
>>> url = 'https://api.github.com/some/endpoint'
>>> headers = {'user-agent': 'my-app/0.0.1'}

>>> r = requests.get(url, headers=headers)
```

- 如果在 `.netrc` 中设置了用户认证信息，使用 headers= 设置的授权就不会生效。而如果设置了`auth=` 参数，``.netrc`` 的设置就无效了。
- 如果被重定向到别的主机，授权 header 就会被删除。
- 代理授权 header 会被 URL 中提供的代理身份覆盖掉。
- 在我们能判断内容长度的情况下，header 的 Content-Length 会被改写。

## POST请求

```python
>>> payload = {'key1': 'value1', 'key2': 'value2'}
>>> r = requests.post("http://httpbin.org/post", data=payload)
```

### 上传多部分编码文件

```python
>>> url = 'http://httpbin.org/post'
>>> files = {'file': open('report.xls', 'rb')}
>>> r = requests.post(url, files=files)
```

## Cookie

```python
>>> url = 'http://httpbin.org/cookies'
>>> cookies = dict(cookies_are='working')

>>> r = requests.get(url, cookies=cookies)
>>> r.text
'{"cookies": {"cookies_are": "working"}}'
```

cookie 的设置。

## 状态响应码

```python
>>> r = requests.get('http://httpbin.org/get')
>>> r.status_code			#状态码
>>> r.raise_for_status()	#抛出异常
>>> r.headers				#查看响应头，服务器的
>>> r.requests.headers		#发送的
>>> r.history				#追踪重定向，看看是不是有值
```

通过在请求中加入`allow_redirects=False`来禁用重定向

通过请求中加入`timeout=0.01`读秒之后停止响应等待

## 错误与异常

* `ConnectionError`  : 遇到网络问题
*  `HTTPError`  : HTTP 请求返回了不成功的状态码
* `Timeout`  : 请求超时
* `TooManyRedirects`  : 超过了设定的最大重定向次数

## 代理

```python
import requests
proxies = {
  "http": "http://10.10.1.10:3128",			#'http': 'socks5://user:pass@host:port'
  "https": "http://10.10.1.10:1080",		#'https': 'socks5://user:pass@host:port'
}
requests.get("http://example.org", proxies=proxies)
```