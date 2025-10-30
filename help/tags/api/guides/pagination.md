---
title: 在Reactor API中分页响应
description: 了解在Reactor API中列出资源时如何分页结果。
exl-id: bccb6e78-4ac8-4786-b398-6e55109d99dd
source-git-commit: be2ad7a02d4bdf5a26a0847c8ee7a9a93746c2ad
workflow-type: tm+mt
source-wordcount: '102'
ht-degree: 0%

---

# 在Reactor API中分页响应

Reactor API返回的响应将分页。 默认页面大小为25个元素。 在API响应对象的`meta.pagination`部分中报告有关分页的详细信息：

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

获取特定页面：

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
