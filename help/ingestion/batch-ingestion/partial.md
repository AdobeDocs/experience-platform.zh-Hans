---
keywords: Experience Platform；主题；热门话题；批摄取；批摄取；部分摄取；部分摄取；检索错误；检索错误；部分批摄取；部分批摄取；部分摄取；部分摄取；
solution: Experience Platform
title: 部分批摄取概述
topic: overview
description: 此文档提供了管理部分批摄取的教程。
translation-type: tm+mt
source-git-commit: 089a4d517476b614521d1db4718966e3ebb13064
workflow-type: tm+mt
source-wordcount: '945'
ht-degree: 0%

---


# 部分批摄取

部分批量摄取是指能够摄取包含错误的数据，最高可达到某个阈值。 借助此功能，用户可以成功将其所有正确数据引入Adobe Experience Platform，同时单独对其所有错误数据进行分组，并详细说明其无效原因。

此文档提供了管理部分批摄取的教程。

## 入门指南

本教程需要对涉及部分批量摄取的Adobe Experience Platform各项服务有一定的工作知识。 在开始本教程之前，请查看以下服务的相关文档：

- [批量摄取](./overview.md):从数据文 [!DNL Platform] 件（如CSV和Parke）中摄取和存储数据的方法。
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md):组织客户体验数 [!DNL Platform] 据的标准化框架。

以下各节提供了成功调用[!DNL Platform] API所需了解的其他信息。

### 读取示例API调用

本指南提供示例API调用，以演示如何格式化请求。 这包括路径、必需的标头和格式正确的请求负载。 还提供API响应中返回的示例JSON。 有关示例API调用文档中使用的约定的信息，请参见[!DNL Experience Platform]疑难解答指南中关于如何阅读示例API调用](../../landing/troubleshooting.md#how-do-i-format-an-api-request)的一节。[

### 收集所需标题的值

要调用[!DNL Platform] API，您必须先完成[身份验证教程](https://www.adobe.com/go/platform-api-authentication-en)。 完成身份验证教程后，将为所有[!DNL Experience Platform] API调用中每个所需标头提供值，如下所示：

- 授权：载体`{ACCESS_TOKEN}`
- x-api-key:`{API_KEY}`
- x-gw-ims-org-id:`{IMS_ORG}`

[!DNL Experience Platform]中的所有资源都隔离到特定虚拟沙箱。 对[!DNL Platform] API的所有请求都需要一个标头，它指定操作将在以下位置进行的沙箱的名称：

- x-sandbox-name:`{SANDBOX_NAME}`

>[!NOTE]
>
>有关[!DNL Platform]中沙箱的详细信息，请参阅[沙箱概述文档](../../sandboxes/home.md)。

## 在API {#enable-api}中启用批处理以进行部分批摄取

>[!NOTE]
>
>本节介绍如何使用API启用批处理以进行部分批处理获取。 有关使用UI的说明，请阅读[在UI](#enable-ui)步骤中启用批以进行部分批摄取。

您可以创建启用了部分摄取的新批。

要创建新批，请按照[批摄取开发人员指南](./api-overview.md)中的步骤操作。 到达&#x200B;**[!UICONTROL 创建batch]**&#x200B;步骤后，在请求主体中添加以下字段：

```json
{
    "enableErrorDiagnostics": true,
    "partialIngestionPercentage": 5
}
```

| 属性 | 描述 |
| -------- | ----------- |
| `enableErrorDiagnostics` | 允许[!DNL Platform]生成有关批处理的详细错误消息的标志。 |
| `partialIngestionPercentage` | 整个批处理失败之前可接受错误的百分比。 因此，在本示例中，最多5%的批可能是错误，然后才会失败。 |


## 在UI {#enable-ui}中启用批以进行部分批摄取

>[!NOTE]
>
>本节介绍如何使用UI启用批以进行部分批摄取。 如果已使用API启用批处理以进行部分批摄取，则可跳到下一节。

要通过[!DNL Platform] UI启用批处理以进行部分摄取，您可以通过源连接创建新批处理，在现有数据集中创建新批处理，或通过“[!UICONTROL 将CSV映射到XDM流]”创建新批处理。

### 新建源连接{#new-source}

要创建新的源连接，请按照[源概述](../../sources/home.md)中列出的步骤操作。 到达&#x200B;**[!UICONTROL 数据流详细信息]**&#x200B;步骤后，请注意&#x200B;**[!UICONTROL 部分摄取]**&#x200B;和&#x200B;**[!UICONTROL 错误诊断]**&#x200B;字段。

![](../images/batch-ingestion/partial-ingestion/configure-batch.png)

通过&#x200B;**[!UICONTROL 部分摄取]**&#x200B;切换，可启用或禁用部分批摄取。

**[!UICONTROL 错误诊断]**&#x200B;切换仅在&#x200B;**[!UICONTROL 部分摄取]**&#x200B;切换关闭时显示。 此功能允许[!DNL Platform]生成有关所摄取批的详细错误消息。 如果&#x200B;**[!UICONTROL 部分摄取]**&#x200B;切换打开，将自动实施增强的错误诊断。

![](../images/batch-ingestion/partial-ingestion/configure-batch-partial-ingestion-focus.png)

**[!UICONTROL 错误阈值]**&#x200B;允许您在整个批处理失败之前设置可接受错误的百分比。 默认情况下，此值设置为5%。

### 使用现有数据集{#existing-dataset}

要使用现有数据集，请通过选择开始集进行。 右侧的提要栏会填充有关数据集的信息。

![](../images/batch-ingestion/partial-ingestion/monitor-dataset.png)

通过&#x200B;**[!UICONTROL 部分摄取]**&#x200B;切换，可启用或禁用部分批摄取。

**[!UICONTROL 错误诊断]**&#x200B;切换仅在&#x200B;**[!UICONTROL 部分摄取]**&#x200B;切换关闭时显示。 此功能允许[!DNL Platform]生成有关所摄取批的详细错误消息。 如果&#x200B;**[!UICONTROL 部分摄取]**&#x200B;切换打开，将自动实施增强的错误诊断。

![](../images/batch-ingestion/partial-ingestion/monitor-dataset-partial-ingestion-focus.png)

**[!UICONTROL 错误阈值]**&#x200B;允许您在整个批处理失败之前设置可接受错误的百分比。 默认情况下，此值设置为5%。

现在，您可以使用&#x200B;**添加数据**&#x200B;按钮上传数据，并将使用部分摄取来摄取数据。

### 使用“[!UICONTROL 将CSV映射到XDM模式]”流{#map-flow}

要使用“[!UICONTROL 将CSV映射到XDM模式]”流，请按照[映射CSV文件教程](../tutorials/map-a-csv-file.md)中列出的步骤操作。 到达&#x200B;**[!UICONTROL 添加数据]**&#x200B;步骤后，请注意&#x200B;**[!UICONTROL 部分摄取]**&#x200B;和&#x200B;**[!UICONTROL 错误诊断]**&#x200B;字段。

![](../images/batch-ingestion/partial-ingestion/xdm-csv-workflow.png)

通过&#x200B;**[!UICONTROL 部分摄取]**&#x200B;切换，可启用或禁用部分批摄取。

**[!UICONTROL 错误诊断]**&#x200B;切换仅在&#x200B;**[!UICONTROL 部分摄取]**&#x200B;切换关闭时显示。 此功能允许[!DNL Platform]生成有关所摄取批的详细错误消息。 如果&#x200B;**[!UICONTROL 部分摄取]**&#x200B;切换打开，将自动实施增强的错误诊断。

![](../images/batch-ingestion/partial-ingestion/xdm-csv-workflow-partial-ingestion-focus.png)

**[!UICONTROL 错误]** 阈值允许您在整个批处理失败之前设置可接受错误的百分比。默认情况下，此值设置为5%。

## 后续步骤 {#next-steps}

本教程介绍了如何创建或修改数据集以启用部分批量摄取。 有关批量摄取的详细信息，请阅读[批量摄取开发人员指南](./api-overview.md)。

有关监视部分摄取错误的信息，请阅读[批量摄取错误诊断指南](../quality/error-diagnostics.md)。
