---
title: Audit Query API指南
description: 审核查询是一个RESTful API，它允许开发人员查看谁在Adobe Experience Platform中执行了哪些操作。
exl-id: 9ed291c6-ff8b-4d9b-9fed-d1e3fa8f92fb
source-git-commit: c2c5778e0a3fff7f488ad7a672123c813cca59f1
workflow-type: tm+mt
source-wordcount: '175'
ht-degree: 1%

---

# [!DNL Audit Query] API指南

此 [!DNL Audit Query] API提供了端点，允许您以编程方式检索和监控各种Adobe Experience Platform功能的事件数据。 端点概述如下。 请访问 [快速入门指南](./getting-started.md) 有关所需标头的重要信息，请阅读示例API调用等。

要查看所有可用的端点和CRUD操作，请访问 [[!DNL Audit Query] API swagger](https://www.adobe.io/experience-platform-apis/references/audit-query/).

## 事件

审核事件提供对Platform中用户操作的见解，包括操作类型、日期和时间、执行操作的用户的电子邮件ID，以及与Adobe Experience Platform各种功能的操作类型相关的其他属性。 要了解如何使用API检索量度，请参阅 [事件端点指南](./events.md).

## 导出

“审核导出”允许您通过指定要在有效负载中检索的事件来检索事件数据。 要了解如何使用API检索量度，请参阅 [导出端点指南](./export.md).
