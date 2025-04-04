---
title: 开始使用审计查询API
description: 利用审核查询API，可检索各种Adobe Experience Platform功能的量度数据。 本文档介绍了在尝试调用“审核查询API”之前需要了解的核心概念。
role: Developer
feature: Audits, API
exl-id: 20eab0a8-98f7-4fee-8f91-88324e54ab18
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '391'
ht-degree: 11%

---

# 审计查询API快速入门

Adobe Experience Platform允许您以审核事件日志的形式审核各种服务和功能的用户活动。 日志中记录的每个操作都包含元数据，这些元数据指示操作类型、日期和时间、执行操作的用户的电子邮件ID以及与操作类型相关的其他属性。

审计查询API允许您以审计事件日志的形式审计各种服务和功能的用户活动。 本文档介绍了在尝试调用“审核查询API”之前需要了解的核心概念。

## 先决条件

为了管理审核事件，您必须已授予&#x200B;**[!UICONTROL 查看用户活动日志]**&#x200B;访问控制权限（可在[!UICONTROL 数据管理]类别下找到）。 要了解如何管理Experience Platform功能的各个权限，请参阅[访问控制文档](../../../../access-control/home.md)。

### 正在读取示例 API 调用

本指南提供了示例 API 调用来演示如何格式化请求。这些包括路径、必需的标头和格式正确的请求负载。还提供了在 API 响应中返回的示例 JSON。有关示例API调用文档中使用的约定的信息，请参阅Experience Platform疑难解答指南中有关[如何读取示例API调用](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request)的部分。

### 收集所需标头的值

本指南要求您完成[身份验证教程](https://www.adobe.com/go/platform-api-authentication-en)，才能成功调用Experience Platform API。 完成身份验证教程将为所有Experience Platform API调用中的每个所需标头提供值，如下所示：

* 授权：持有人`{ACCESS_TOKEN}`
* x-api-key： `{API_KEY}`
* x-gw-ims-org-id： `{ORG_ID}`

[!DNL Experience Platform]中的所有资源都被隔离到特定的虚拟沙盒中。 对[!DNL Experience Platform] API的所有请求都需要一个标头，用于指定将在其中执行操作的沙盒的名称。 有关[!DNL Experience Platform]中沙盒的更多信息，请参阅[沙盒概述文档](../../../../sandboxes/home.md)。

* `x-sandbox-name: {SANDBOX_NAME}`

所有包含有效负载(POST、PUT和PATCH)的请求都需要额外的标头：

* Content-Type： application/json

## 后续步骤

要开始使用[!DNL Audit Query] API进行调用，请参阅[事件端点指南](./events.md)和[导出端点指南](./export.md)。
