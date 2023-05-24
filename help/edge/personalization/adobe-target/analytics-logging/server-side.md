---
title: Platform Web SDK中A4T資料的伺服器端記錄
description: 瞭解如何使用Experience PlatformWeb SDK為Adobe Analytics for Target (A4T)啟用伺服器端記錄。
seo-title: Server-side logging for A4T data in Platform Web SDK
seo-description: Learn how to enable server-side logging for Adobe Analytics for Target (A4T) using the Experience Platform Web SDK.
keywords: a4t；target；web；sdk；平台；記錄；
exl-id: 26c25f58-e43c-4147-8595-69ea85af561f
source-git-commit: 38d54b2c793c9dcb1a45ec4acbb9016d1e927d23
workflow-type: tm+mt
source-wordcount: '170'
ht-degree: 1%

---

# Platform Web SDK中A4T資料的伺服器端記錄

Adobe Experience Platform Web SDK可讓您在Platform Edge Network上實作Adobe Analytics for Target (A4T)功能。 啟用伺服器端記錄後，所有透過Edge Network傳送的Analytics點選都會在伺服器端以Target詳細資料增加，不必經過點選拼接程式。

在資料流設定中啟用Analytics時，便會啟用Analytics的伺服器端記錄：

![Analytics資料流設定已啟用](../assets/enable-analytics-datastream.png)

下圖顯示啟用伺服器端Analytics記錄時，資料如何流經系統：

![伺服器端記錄流程](../assets/analytics-server-side-logging.png)

## 后续步骤

本指南涵蓋Web SDK中A4T資料的伺服器端記錄。 請參閱指南： [使用者端記錄](./client-side.md) 有關如何在使用者端處理A4T資料的詳細資訊。
