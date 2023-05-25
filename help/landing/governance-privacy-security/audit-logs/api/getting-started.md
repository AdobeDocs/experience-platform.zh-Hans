---
title: 审计查询API快速入门
description: 利用审核查询API，可检索各种Adobe Experience Platform功能的量度数据。 本文档介绍了在尝试调用“审核查询API”之前需要了解的核心概念。
exl-id: 20eab0a8-98f7-4fee-8f91-88324e54ab18
source-git-commit: c2c5778e0a3fff7f488ad7a672123c813cca59f1
workflow-type: tm+mt
source-wordcount: '392'
ht-degree: 9%

---

# 审计查询API快速入门

Adobe Experience Platform允许您以审核事件日志的形式审核各种服务和功能的用户活动。 日志中记录的每个操作都包含元数据，这些元数据可指示操作类型、日期和时间、执行操作的用户的电子邮件 ID 以及与操作类型相关的其他属性。

审计查询API允许您以审计事件日志的形式审计各种服务和功能的用户活动。 本文档介绍了在尝试调用“审核查询API”之前需要了解的核心概念。

## 先决条件

要管理审核事件，您必须拥有 **[!UICONTROL 查看用户活动日志]** 已授予访问控制权限(可在 [!UICONTROL 数据管理] 类别)。 要了解如何管理Platform功能的各个权限，请参阅 [访问控制文档](../../../../access-control/home.md).

### 正在读取示例API调用

本指南提供了示例API调用，以演示如何设置请求的格式。 这些资源包括路径、必需的标头和格式正确的请求负载。 此外，还提供了在API响应中返回的示例JSON。 有关示例API调用文档中使用的约定的信息，请参阅 [如何读取示例API调用](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) 在Experience Platform疑难解答指南中。

### 收集所需标题的值

本指南要求您已完成 [身份验证教程](https://www.adobe.com/go/platform-api-authentication-en) 才能成功调用平台API。 完成身份验证教程将为所有Experience PlatformAPI调用中的每个所需标头提供值，如下所示：

* 授权：持有者 `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{ORG_ID}`

中的所有资源 [!DNL Experience Platform] 与特定的虚拟沙盒隔离。 的所有请求 [!DNL Platform] API需要一个标头，用于指定将在其中执行操作的沙盒的名称。 有关中沙箱的详细信息 [!DNL Platform]，请参见 [沙盒概述文档](../../../../sandboxes/home.md).

* `x-sandbox-name: {SANDBOX_NAME}`

包含有效负载(POST、PUT和PATCH)的所有请求都需要额外的标头：

* Content-Type： application/json

## 后续步骤

要开始使用 [!DNL Audit Query] API，请参阅 [事件端点指南](./events.md) 和 [导出端点指南](./export.md).
