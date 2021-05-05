[TOC]

# requests

## 基本使用

```python
import requests

r = requests.get("https://www.baidu.com")调用requests模块中的get方法
r.encoding='utf-8'指定使用的编码方式

print(r.text)以以str方式输出内容
print(type(r.text))type输出编码方式

print(r.content)不解码，需要手动解码
print(r.content.decode('utf-8'))使用手动解码，方式为utf-8编码
```

# get post headers请求

## headers就是User-Agent:

```
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/89.0.4389.114 Safari/537.36
```

```python
import requests

kw = {'wd':'图片'}kw定义变量的名字wd是因为在百度上搜索是/s?wd=搜索内容
headers = {"User-Agent" : "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/89.0.4389.114 Safari/537.36"}headers定义的头，就是浏览器的定义
r = requests.get("https://www.baidu.com/s?", params=kw, headers=headers)使用get方式定义params关键字参数 headers头部信息
with open ('shousuo.html', 'w', encoding='utf-8')as f:打开一个文件以utf-8的编码方式写入信息
    f.write(r.text)write关闭文件，写入的对象是r.text
print(r.url.encode('utf-8'))打印url地址
```

## post提交，登陆信息

```python
import requests
login_url = "http://103.45.153.29:8080/login"定义变量接收url
定义变量接收data
name_pwd= {
    "username":"Keytime21",
    "password":"123456"
}

headers = {"User-Agent":"Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/89.0.4389.114 Safari/537.36"}

response = requests.post(url=login_url, data=name_pwd, headers=headers)data返回的就是提交的值body
print(requests.status_codes)返回状态码，这里正常访问状态码就是200
print(response.url)返回url
print(response.text)返回回显
print(response.headers)查看整个请求头
print(response.headers['Accept-Encoding'])查看请求头的某一属性
print(response.requests.body)查看请求请求头body值
```

## 其他请求方法

```
put
r = requests.put("http://xxx.com/put",data={'key':'value'})
delete
r = requests.delete("http://xxx.com/delede")
head
r = requests.head("http://xxx.com/haed")
options
r = requests.options("http://xxx.com/get")
```

## 输出信息

```python
print(response.headers)查看响应头的信息
print(response.encoding)查看响应的编码
print(response.status_code)查看响应状态码
print(response.cookies)获取cookie信息
print(response.cookies["BAIDUID"])获取cookie的某个name的值
print(response.History)请求历史记录
```

## Cookis和Session区别

session在服务器端，cookis在客户端

session的运行依赖session id 而session id是存在cookie中的，也就是说浏览器禁用了cookie,session也会失效，也可以通过其他方式实现比如说在url中传递session id

cookie目的可以跟踪会话，可以保存用户密码等

sessionu用来跟踪会话

## Cookis

```python
import requests

response = requests.get("https://www.baidu.com")
print(response.cookies)输出cookies的值，但是这里输出是以<>显示并不方便看
print(response.cookies.get_dict())以字典的方式删除会{}包起来方便查看
```

Session

```

```

