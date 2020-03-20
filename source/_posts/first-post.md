---
title: Hello World Guan
---
```text
vue：
	父与子组件主要通信方式：属性传递(传递属性或回调函数)、发布订阅（EventBus）：$on / $emit
	与后代元素的通信方式：Provide / inject
	任意组件间通信：本地存储方案
		1.vuex,一刷新数据就没了，存储在虚拟内存中
		2.localStorage，持久化存储
react：
	父与子组件主要通信方式：属性传递(传递属性或回调函数)、发布订阅需要自己实现
	与后代元素的通信方式：React.createContext
	任意组件间通信：存储方案
		1.redux/react-redux、mobx、dva,一刷新数据就没了，存储在虚拟内存中
		2.localStorage，持久化存储

cookie和session的区别与关联：
	服务器设置 session，返回给客户端，在响应头中携带 Set-Cookie="connect.sid",该sid表示当前客户端与服务器建立的连接的唯一标识，往客户端种植该sid cookie且是httponly只读的。
	客户端再次发起请求会携带这个 sid cookie，服务器根据这个 sid 就可以之前存储的session信息了。
服务器设置的session过期时间就是cookie的过期时间。

本地存储常用的方案：cookies，localStorage，sessionStorage
```