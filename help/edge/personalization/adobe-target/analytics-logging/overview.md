---
title: Platform Web SDK中的Adobe Analytics for Target (A4T)記錄
description: 瞭解如何使用Experience PlatformWeb SDK控制Adobe Analytics for Target (A4T)資料的收集。
seo-title: Adobe Analytics for Target (A4T) Logging in the Platform Web SDK
seo-description: Learn how to control the collection of Adobe Analytics for Target (A4T) data using the Experience Platform Web SDK.
keywords: a4t；記錄；analytics；sdk；web sdk；
exl-id: f1c90ccd-48a9-4668-b2ac-eacd5bec0b91
source-git-commit: fb0d8aedbb88aad8ed65592e0b706bd17840406b
workflow-type: tm+mt
source-wordcount: '284'
ht-degree: 2%

---

# Platform Web SDK中的Adobe Analytics for Target (A4T)記錄

使用Adobe Target進行個人化時，您可以選擇要使用哪個系統進行效能測量。 每個 [Target活動](https://experienceleague.adobe.com/docs/target/using/activities/target-activities-guide.html) 可讓您在Target報表和Adobe Analytics報表之間選取。

如果您使用Analytics報表，Adobe Target必須向Analytics傳達下列內容：

* 訪客已進入哪個Adobe Target活動
* 他們已看過的體驗
* 已達到哪個轉換

Adobe Experience Platform Web SDK支援兩種型別的Analytics Logging for Target (A4T)使用案例：

| 記錄方法 | 描述 |
| --- | --- |
| 伺服器端Analytics記錄 | 所有透過Edge Network傳送的Analytics點選，都可在伺服器端以Target詳細資料強化，不必經過點選拼接程式。 |
| 客户端分析日志记录 | Target資料會傳回使用者端，讓您能夠手動增加，並使用將資料傳送至Analytics [資料插入API](https://experienceleague.adobe.com/docs/analytics/import/c-data-insertion-api.html). |

記錄方法取決於您已設定的是否啟用Adobe Analytics [資料串流](../../../datastreams/overview.md)：

![記錄方法決定流程](../assets/analytics-logging.png)

## 后续步骤

本檔案簡要介紹Web SDK中A4T資料的不同記錄方法。 如需上述各方法的詳細資訊，請參閱下列檔案：

* [Platform Web SDK中A4T資料的伺服器端記錄](./server-side.md)
* [Platform Web SDK中A4T資料的使用者端記錄](./client-side.md)
