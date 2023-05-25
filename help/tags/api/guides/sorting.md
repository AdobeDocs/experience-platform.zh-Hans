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

列出Reactor API中的端点，可让您根据指定的属性对返回的资源进行排序。 您可以通过提供 `sort` 请求路径中的参数。

## 升序排序

资源可以按属性升序排序，方法是指定要排序的属性，并在该属性前面加上 `+`：

`GET /companies/:company_id/properties?sort=+name`

## 降序排序

资源可以按属性降序排序，方法是指定要排序的属性，并在该属性前面加上 `-`：

`GET /companies/:company_id/properties?sort=-name`

## 多种排序

要按多个值排序，请以逗号分隔列表的形式提供排序指令：

`GET /companies/:company_id/properties?sort=+name,-org_id`
