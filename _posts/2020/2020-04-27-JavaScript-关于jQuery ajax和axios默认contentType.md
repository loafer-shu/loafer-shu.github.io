---
layout: post
title: "关于jQuery ajax和 Axios默认contentType"
date: 2020-03-17 11:52:35 +0800
categories: [JavaScript]
---

## 关于jQuery ajax和 Axios默认contentType

### jQueryAjax

Ajax默认为` application/x-www-form-urlencoded; charset=UTF-8 `

为表单提交，键值对格式 xxx=xxx&xxx=xxx

此时java后端直接参数名对上便自动会赋值，@RequestParam可取到值

### axios

axios默认为` application/json; charset=UTF-8 `

此时，传递数据为json对象字符串，@RequestParam无法取到值，后端controller层参数名对上也无法取值，这时需使用对象及加上@RequestBody接收，

