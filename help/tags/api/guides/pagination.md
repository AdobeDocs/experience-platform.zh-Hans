---
title: 在Reactor API中对响应进行分页
description: 了解在Reactor API中列出资源时如何对结果进行分页。
source-git-commit: 6a1728bd995137a7cd6dc79313762ae6e665d416
workflow-type: tm+mt
source-wordcount: '101'
ht-degree: 0%

---

# 在Reactor API中对响应进行分页

Reactor API返回的响应将进行分页。 默认页面大小为25个元素。 有关分页的详细信息，请参阅API响应对象的`meta.pagination `部分：

```json
"meta": {
  "pagination": {
      "current_page": 1,
      "next_page": 2,
      "prev_page": null,
      "total_pages": 4,
      "total_count": 90
  }
}
```

可以通过在请求路径中包含`page`查询参数来获取特定页面并修改页面大小。

## 检索特定页面

要获取特定页面，请执行以下操作：

```http
GET /{RESOURCE_TYPE}/{RESOURCE_ID}?page[number]={PAGE_NUMBER}
```

## 更改页面大小

要更改页面大小，请执行以下操作：

```http
GET /{RESOURCE_TYPE}/{RESOURCE_ID}?page[size]={PAGE_SIZE}
```

不同的选项可以组合在一起：

```http
GET /{RESOURCE_TYPE}/{RESOURCE_ID}?page[size]={PAGE_SIZE}&page[number]={PAGE_NUMBER}
```
