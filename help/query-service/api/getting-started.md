---
keywords: Experience Platform；主页；热门主题；查询服务；查询服务；查询
solution: Experience Platform
title: 查询服务API指南
topic-legacy: query templates
description: 查询 Service API允许开发人员使用标准SQL查询其Adobe Experience Platform数据。 请按照本指南学习如何使用API执行关键操作。
exl-id: 2f4a156b-5623-419a-a9b2-72310f755708
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '395'
ht-degree: 1%

---

# [!DNL Query Service] API指南

本开发人员指南提供了在Adobe Experience Platform [!DNL Query Service] API中执行各种操作的步骤。

## 入门指南

本指南要求对与使用[!DNL Query Service]相关的各种Adobe Experience Platform服务有充分的了解。

- [[!DNL Query Service]](../home.md):提供了查询数据集并将生成的查询捕获为中的新数据集的能 [!DNL Experience Platform]力。
- [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md):组织客户体验数 [!DNL Experience Platform] 据的标准化框架。
- [[!DNL Sandboxes]](../../sandboxes/home.md): [!DNL Experience Platform] 提供将单个实例分区为单 [!DNL Platform] 独虚拟环境的虚拟沙箱，以帮助开发和发展数字体验应用程序。

以下各节提供您需要了解的其他信息，以便成功使用API [!DNL Query Service]。

### 读取示例API调用

本指南提供示例API调用，以演示如何设置请求的格式。 这包括路径、必需的标头和格式正确的请求负载。 还提供API响应中返回的示例JSON。 有关本文档中用于示例API调用的约定的信息，请参阅[!DNL Experience Platform]疑难解答指南中关于如何读取示例API调用](../../landing/troubleshooting.md#how-do-i-format-an-api-request)的部分。[

### 收集所需标题的值

要调用[!DNL Experience Platform] API，您必须首先完成[身份验证教程](https://www.adobe.com/go/platform-api-authentication-en)。 完成身份验证教程后，将为所有[!DNL Platform] API调用中每个所需标头提供值，如下所示：

- Authorization: `Bearer {ACCESS_TOKEN}`
- x-api-key:`{API_KEY}`
- x-gw-ims-org-id:`{IMS_ORG}`

[!DNL Experience Platform]中的所有资源都隔离到特定虚拟沙箱。 对[!DNL Platform] API的所有请求都需要一个头，该头指定将在其中执行操作的沙箱的名称：

- x-sandbox-name:`{SANDBOX_NAME}`

>[!NOTE]
>
>有关在[!DNL Experience Platform]中使用沙箱的详细信息，请参阅[沙箱概述文档](../../sandboxes/home.md)。

## 示例API调用

既然您了解了要使用哪些标头，就可以开始调用[!DNL Query Service] API。 以下文档将遍历您可以使用[!DNL Query Service] API进行的各种API调用。 每个示例调用都包括常规API格式、显示所需标头的示例请求和示例响应。

- [查询](queries.md)
- [连接参数](connection-parameters.md)
- [计划查询](scheduled-queries.md)
- [为计划查询运行](runs-scheduled-queries.md)
- [查询模板](query-templates.md)

## 后续步骤

既然您已经学习了如何使用[!DNL Query Service] API进行调用，您就可以创建自己的非交互式查询。 有关如何创建查询的详细信息，请阅读[ SQL参考指南](../sql/overview.md)。
