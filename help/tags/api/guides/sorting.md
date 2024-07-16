---
title: 对Reactor API中的响应进行排序
description: 了解在Reactor API中列出资源时如何筛选结果。
exl-id: 49dcf0b6-4ce8-41d9-9e3a-e44f5c0ff905
source-git-commit: a8b0282004dd57096dfc63a9adb82ad70d37495d
workflow-type: tm+mt
source-wordcount: '123'
ht-degree: 0%

---

# 对Reactor API中的响应进行排序

在Reactor API中列出端点，可让您根据指定的属性对返回的资源进行排序。 通过在请求路径中提供`sort`参数，可以配置响应的排序顺序。

## 升序排序

可以通过指定
要排序的属性，并以`+`作为前缀：

`GET /companies/:company_id/properties?sort=+name`

## 降序排序

可以通过指定
要排序的属性，并以`-`作为前缀：

`GET /companies/:company_id/properties?sort=-name`

## 多种排序

要按多个值排序，请以逗号分隔的形式提供排序指令
列表：

`GET /companies/:company_id/properties?sort=+name,-org_id`
