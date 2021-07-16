---
title: 在Reactor API中对响应进行排序
description: 了解在Reactor API中列出资源时如何过滤结果。
source-git-commit: 6a1728bd995137a7cd6dc79313762ae6e665d416
workflow-type: tm+mt
source-wordcount: '123'
ht-degree: 0%

---

# 在Reactor API中对响应进行排序

通过在Reactor API中列出端点，您可以根据指定的属性对返回的资源进行排序。 通过在请求路径中提供`sort`参数，可以配置响应的排序顺序。

## 升序排序

通过指定
属性，并在其前面添加`+`:

`GET /companies/:company_id/properties?sort=+name`

## 降序排序

通过指定
属性，并在其前面添加`-`:

`GET /companies/:company_id/properties?sort=-name`

## 多重排序

要按多个值排序，请以逗号分隔的形式提供排序指令
列表：

`GET /companies/:company_id/properties?sort=+name,-org_id`
