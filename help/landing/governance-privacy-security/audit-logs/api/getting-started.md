---
title: 审核查询API快速入门
description: 审核查询API允许您检索各种Adobe Experience Platform功能的量度数据。 本文档简要介绍在尝试调用审核查询API之前需要了解的核心概念。
source-git-commit: 5b3459711f41430977f9d7b06f8b35801739207c
workflow-type: tm+mt
source-wordcount: '392'
ht-degree: 9%

---

# 审核查询API快速入门

Adobe Experience Platform允许您以审核事件日志的形式审核各种服务和功能的用户活动。 日志中记录的每个操作都包含元数据，这些元数据可指示操作类型、日期和时间、执行操作的用户的电子邮件 ID 以及与操作类型相关的其他属性。

审核查询API允许您以审核事件日志的形式审核各种服务和功能的用户活动。 本文档简要介绍在尝试调用审核查询API之前需要了解的核心概念。

## 先决条件

要管理审核事件，您必须具有 **[!UICONTROL 查看用户活动日志]** 已授予的访问控制权限(位于 [!UICONTROL 数据管理] 类别)。 要了解如何管理平台功能的各个权限，请参阅 [访问控制文档](../../../../access-control/home.md).

### 读取示例API调用

本指南提供了示例API调用，以演示如何设置请求的格式。 这包括路径、所需标头以及格式正确的请求负载。 还提供了API响应中返回的示例JSON。 有关文档中用于示例API调用的约定的信息，请参阅 [如何阅读示例API调用](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) (位于Experience Platform疑难解答指南中)。

### 收集所需标题的值

本指南要求您完成 [身份验证教程](https://www.adobe.com/go/platform-api-authentication-en) 以成功调用Platform API。 完成身份验证教程可为所有Experience PlatformAPI调用中每个所需标头的值，如下所示：

* 授权：持有者 `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{ORG_ID}`

中的所有资源 [!DNL Experience Platform] 与特定虚拟沙箱隔离。 对 [!DNL Platform] API需要一个标头来指定操作将在其中进行的沙盒的名称。 有关 [!DNL Platform]，请参阅 [沙盒概述文档](../../../../sandboxes/home.md).

* `x-sandbox-name: {SANDBOX_NAME}`

所有包含有效负载(POST、PUT和PATCH)的请求都需要额外的标头：

* Content-Type:application/json

## 后续步骤

要开始使用 [!DNL Audit Query] API，请参阅 [events endpoint指南](./events.md) 和 [导出端点指南](./export.md).
