---
title: 审核查询API指南
description: 审核查询是一个RESTful API，它允许开发人员查看谁在Adobe Experience Platform中执行了哪些操作。
role: Developer
feature: Audits, API
exl-id: 9ed291c6-ff8b-4d9b-9fed-d1e3fa8f92fb
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '172'
ht-degree: 1%

---

# [!DNL Audit Query] API指南

[!DNL Audit Query] API提供了端点，允许您以编程方式检索和监视各种Adobe Experience Platform功能的事件数据。 端点概述如下。 请访问[快速入门指南](./getting-started.md)，了解有关所需标头、读取示例API调用等的重要信息。

要查看所有可用的端点和CRUD操作，请访问[[!DNL Audit Query] API swagger](https://www.adobe.io/experience-platform-apis/references/audit-query/)。

## 活动

审核事件提供对Experience Platform中用户操作的见解，包括操作类型、日期和时间、执行操作的用户的电子邮件ID，以及与Adobe Experience Platform各种功能的操作类型相关的其他属性。 要了解如何使用API检索量度，请参阅[事件端点指南](./events.md)。

## 导出

“审核导出”允许您通过指定要在有效负载中检索的事件来检索事件数据。 要了解如何使用API检索指标，请参阅[导出端点指南](./export.md)。
