---
title: 在Reactor API中分页响应
description: 了解在Reactor API中列出资源时如何分页结果。
exl-id: bccb6e78-4ac8-4786-b398-6e55109d99dd
source-git-commit: a8b0282004dd57096dfc63a9adb82ad70d37495d
workflow-type: tm+mt
source-wordcount: '101'
ht-degree: 0%

---

# 在Reactor API中分页响应

Reactor API返回的响应将分页。 默认页面大小为25个元素。 有关分页的详细信息，请参见 `meta.pagination `API响应对象的部分：

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

可以通过包含来获取特定页面并修改页面大小 `page` 查询参数。

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
