---
title: 排序Reactor API中的回應
description: 瞭解在Reactor API中列出資源時如何篩選結果。
exl-id: 49dcf0b6-4ce8-41d9-9e3a-e44f5c0ff905
source-git-commit: a8b0282004dd57096dfc63a9adb82ad70d37495d
workflow-type: tm+mt
source-wordcount: '123'
ht-degree: 0%

---

# 排序Reactor API中的回應

列出Reactor API中的端點，可讓您根據指定的屬性排序傳回的資源。 您可以透過提供 `sort` 請求路徑中的引數。

## 升序排序

資源可依屬性遞增順序排序，方法是指定要排序的屬性，並在其前面加上前置詞 `+`：

`GET /companies/:company_id/properties?sort=+name`

## 降序排序

資源可依屬性遞減順序排序，方法是指定要排序的屬性，並在其前面加上前置詞 `-`：

`GET /companies/:company_id/properties?sort=-name`

## 多重排序

若要依多個值排序，請以逗號分隔的清單形式提供排序指令：

`GET /companies/:company_id/properties?sort=+name,-org_id`
