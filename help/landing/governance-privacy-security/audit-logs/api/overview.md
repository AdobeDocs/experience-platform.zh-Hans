---
title: 审核查询API指南
description: 审核查询是一个RESTful API，它允许开发人员查看谁在Adobe Experience Platform中执行了哪些操作。
source-git-commit: 5b3459711f41430977f9d7b06f8b35801739207c
workflow-type: tm+mt
source-wordcount: '175'
ht-degree: 1%

---

# [!DNL Audit Query] API指南

的 [!DNL Audit Query] API提供了端点，允许您以编程方式检索和监视各种Adobe Experience Platform功能的事件数据。 端点概述如下。 请访问 [入门指南](./getting-started.md) 有关所需标头、读取示例API调用等的重要信息。

要查看所有可用的端点和CRUD操作，请访问 [[!DNL Audit Query] API Swagger](https://www.adobe.io/experience-platform-apis/references/audit-query/).

## 事件

审核事件可提供对Platform中用户操作的分析，包括操作类型、日期和时间、执行操作的用户的电子邮件ID，以及与Adobe Experience Platform中各项功能的操作类型相关的其他属性。 要了解如何使用API检索量度，请参阅 [events endpoint指南](./events.md).

## 导出

审核导出允许您通过指定要在有效负载中检索的事件来检索事件数据。 要了解如何使用API检索量度，请参阅 [导出端点指南](./export.md).
