---
keywords: Experience Platform；主页；热门主题；批量摄取；批量摄取；部分摄取；检索错误；检索错误；部分批量摄取；部分批量摄取；部分；摄取；摄取；
solution: Experience Platform
title: 部分批量摄取概述
description: 本文档提供了有关管理部分批处理摄取的教程。
exl-id: 25a34da6-5b7c-4747-8ebd-52ba516b9dc3
source-git-commit: e802932dea38ebbca8de012a4d285eab691231be
workflow-type: tm+mt
source-wordcount: '945'
ht-degree: 0%

---

# 部分批次摄取

部分批量摄取是指在一定阈值内摄取包含错误的数据的能力。 借助此功能，用户可以成功地将其所有正确数据摄取到Adobe Experience Platform，同时对其所有不正确的数据进行单独批处理，并详细了解其无效原因。

本文档提供了有关管理部分批处理摄取的教程。

## 快速入门

本教程需要了解与部分批量摄取相关的各种Adobe Experience Platform服务。 在开始本教程之前，请查看以下服务的文档：

- [批量摄取](./overview.md)：方法 [!DNL Platform] 从数据文件（如CSV和Parquet）中摄取和存储数据。
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md)：用于实现此目标的标准化框架 [!DNL Platform] 组织客户体验数据。

以下部分提供成功调用时需要了解的其他信息 [!DNL Platform] API。

### 正在读取示例API调用

本指南提供了示例API调用，以演示如何设置请求的格式。 这些资源包括路径、必需的标头和格式正确的请求负载。 此外，还提供了在API响应中返回的示例JSON。 有关示例API调用文档中使用的约定的信息，请参阅以下章节： [如何读取示例API调用](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 在 [!DNL Experience Platform] 疑难解答指南。

### 收集所需标题的值

为了调用 [!DNL Platform] API，您必须先完成 [身份验证教程](https://www.adobe.com/go/platform-api-authentication-en). 完成身份验证教程将提供所有中所有所需标头的值 [!DNL Experience Platform] API调用，如下所示：

- 授权：持有者 `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

中的所有资源 [!DNL Experience Platform] 与特定的虚拟沙盒隔离。 的所有请求 [!DNL Platform] API需要一个标头，用于指定将在其中执行操作的沙盒的名称：

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>有关中沙箱的详细信息 [!DNL Platform]，请参见 [沙盒概述文档](../../sandboxes/home.md).

## 在API中为部分批量摄取启用批次 {#enable-api}

>[!NOTE]
>
>本节介绍如何使用API为部分批量摄取启用批处理。 有关使用UI的说明，请阅读 [在UI中为部分批量摄取启用批次](#enable-ui) 步骤。

您可以创建一个启用了部分摄取的新批次。

要创建新批次，请按照 [批量摄取开发人员指南](./api-overview.md). 一旦您到达 **[!UICONTROL 创建批次]** 步骤，在请求正文中添加以下字段：

```json
{
    "enableErrorDiagnostics": true,
    "partialIngestionPercent": 5
}
```

| 属性 | 描述 |
| -------- | ----------- |
| `enableErrorDiagnostics` | 允许 [!DNL Platform] 生成有关批次的详细错误消息。 |
| `partialIngestionPercent` | 整个批次失败之前可接受的错误百分比。 因此，在此示例中，最多有5%的批次可能是错误，然后才会失败。 |


## 在UI中为部分批次摄取启用批次 {#enable-ui}

>[!NOTE]
>
>本节介绍如何使用UI为部分批量摄取启用批处理。 如果已使用API为部分批次摄取启用批次，则可以跳至下一节。

要通过为部分摄取启用批次，请执行以下操作 [!DNL Platform] UI中，您可以通过源连接创建新批处理，在现有数据集中创建新批处理，或通过&#39;&#39;创建新批处理[!UICONTROL 将CSV映射到XDM流]“。

### 创建新的源连接 {#new-source}

要创建新的源连接，请按照 [源概述](../../sources/home.md). 一旦您到达 **[!UICONTROL 数据流详细信息]** 步骤，请记下 **[!UICONTROL 部分摄取]** 和 **[!UICONTROL 错误诊断]** 字段。

![](../images/batch-ingestion/partial-ingestion/configure-batch.png)

此 **[!UICONTROL 部分摄取]** 切换允许您启用或禁用部分批量摄取。

此 **[!UICONTROL 错误诊断]** 切换仅在 **[!UICONTROL 部分摄取]** 切换已关闭。 此功能允许 [!DNL Platform] 生成有关所摄取批次的详细错误消息。 如果 **[!UICONTROL 部分摄取]** 切换功能已启用，增强错误诊断功能会自动强制执行。

![](../images/batch-ingestion/partial-ingestion/configure-batch-partial-ingestion-focus.png)

此 **[!UICONTROL 错误阈值]** 允许您在整个批处理失败之前设置可接受的错误百分比。 默认情况下，此值设置为5%。

### 使用现有数据集 {#existing-dataset}

要使用现有数据集，请从选择一个数据集开始。 右侧边栏会填充有关数据集的信息。

![](../images/batch-ingestion/partial-ingestion/monitor-dataset.png)

此 **[!UICONTROL 部分摄取]** 切换允许您启用或禁用部分批量摄取。

此 **[!UICONTROL 错误诊断]** 切换仅在 **[!UICONTROL 部分摄取]** 切换已关闭。 此功能允许 [!DNL Platform] 生成有关所摄取批次的详细错误消息。 如果 **[!UICONTROL 部分摄取]** 切换功能已启用，增强错误诊断功能会自动强制执行。

![](../images/batch-ingestion/partial-ingestion/monitor-dataset-partial-ingestion-focus.png)

此 **[!UICONTROL 错误阈值]** 允许您在整个批处理失败之前设置可接受的错误百分比。 默认情况下，此值设置为5%。

现在，您可以使用上传数据 **添加数据** 按钮，将使用部分摄取来摄取。

### 使用&quot;[!UICONTROL 将CSV映射到XDM架构]&quot;流量 {#map-flow}

要使用&quot;[!UICONTROL 将CSV映射到XDM架构]”流程，请按照 [映射CSV文件教程](../tutorials/map-csv/overview.md). 一旦您到达 **[!UICONTROL 添加数据]** 步骤，请记下 **[!UICONTROL 部分摄取]** 和 **[!UICONTROL 错误诊断]** 字段。

![](../images/batch-ingestion/partial-ingestion/xdm-csv-workflow.png)

此 **[!UICONTROL 部分摄取]** 切换允许您启用或禁用部分批量摄取。

此 **[!UICONTROL 错误诊断]** 切换仅在 **[!UICONTROL 部分摄取]** 切换已关闭。 此功能允许 [!DNL Platform] 生成有关所摄取批次的详细错误消息。 如果 **[!UICONTROL 部分摄取]** 切换功能已启用，增强错误诊断功能会自动强制执行。

![](../images/batch-ingestion/partial-ingestion/xdm-csv-workflow-partial-ingestion-focus.png)

**[!UICONTROL 错误阈值]** 允许您在整个批处理失败之前设置可接受的错误百分比。 默认情况下，此值设置为5%。

## 后续步骤 {#next-steps}

本教程介绍了如何创建或修改数据集以启用部分批量摄取。 有关批量摄取的更多信息，请阅读 [批量摄取开发人员指南](./api-overview.md).

有关监控部分摄取错误的信息，请阅读 [批量摄取错误诊断指南](../quality/error-diagnostics.md).
