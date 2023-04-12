---
keywords: Experience Platform；主页；热门主题；流；流摄取；故障诊断；流摄取故障诊断；流摄取常见问题解答；FAQ;
solution: Experience Platform
title: 流摄取疑难解答指南
description: 本文档提供了有关在Adobe Experience Platform上流式引入的常见问题解答。
exl-id: 5d5deccf-25b8-44c9-ae27-9a4713ced274
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '1024'
ht-degree: 0%

---

# 流摄取疑难解答指南

本文档提供了有关在Adobe Experience Platform上流式引入的常见问题解答。 有关与其他 [!DNL Platform] 服务，包括在所有 [!DNL Platform] API，请参阅 [Experience Platform疑难解答指南](../../landing/troubleshooting.md).

Adobe Experience Platform [!DNL Data Ingestion] 提供可用于将数据摄取到 [!DNL Experience Platform]. 摄取的数据用于近乎实时地更新单个客户用户档案，从而跨多个渠道提供个性化的相关体验。 请阅读 [数据摄取概述](../home.md) 以了解有关服务和不同摄取方法的更多信息。 有关如何使用流摄取API的步骤，请阅读 [流摄取概述](../streaming-ingestion/overview.md).

## 常见问题解答

以下是有关流摄取的常见问题解答列表。

### 如何知道我发送的有效负载的格式正确？

[!DNL Data Ingestion] 利用 [!DNL Experience Data Model] (XDM)架构来验证传入数据的格式。 发送不符合预定义XDM架构结构的数据将导致摄取失败。 有关XDM及其在 [!DNL Experience Platform]，请参阅 [XDM系统概述](../../xdm/home.md).

流摄取支持两种验证模式：同步和异步。 每种验证方法处理失败数据的方式不同。

**同步验证** 应在开发过程中使用。 验证失败的记录会被删除，并返回一条错误消息，说明失败的原因(例如：“XDM消息格式无效”)。

**异步验证** 应用于生产。 任何未通过验证的格式错误的数据都会发送到 [!DNL Data Lake] 作为失败的批处理文件，稍后可在其中检索该文件以供进一步分析。

有关同步和异步验证的更多信息，请参阅 [流式验证概述](../quality/streaming-validation.md). 有关如何查看验证失败批次的步骤，请参阅 [检索失败批次](../quality/retrieve-failed-batches.md).

### 我能否在将请求有效负载发送到之前验证它 [!DNL Platform]?

只有在请求负载被发送到之后，才能对其进行评估 [!DNL Platform]. 执行同步验证时，有效负载会返回填充的JSON对象，而无效负载会返回错误消息。 在异步验证期间，服务会检测任何格式错误的数据，并将其发送到 [!DNL Data Lake] 以供日后检索以进行分析。 请参阅 [流式验证概述](../quality/streaming-validation.md) 以了解更多信息。

### 如果在不支持同步验证的边缘上请求同步验证，会出现什么情况？

当请求的位置不支持同步验证时，将返回501错误响应。 请参阅 [流式验证概述](../quality/streaming-validation.md) 以了解有关同步验证的详细信息。

### 如何确保仅从可信来源收集数据？

[!DNL Experience Platform] 支持安全数据收集。 启用经过身份验证的数据收集后，客户端必须发送JSON Web令牌(JWT)及其组织ID作为请求标头。 有关如何将经过身份验证的数据发送到的更多信息 [!DNL Platform]，请参阅 [经过验证的数据收集](../tutorials/create-authenticated-streaming-connection.md).

### 将数据流式传输到的滞后时间是多少 [!DNL Real-Time Customer Profile]?

流式处理事件通常反映在 [!DNL Real-Time Customer Profile] 在60秒内。 实际延迟可能会因数据量、消息大小和带宽限制而有所不同。

### 我是否可以在同一API请求中包含多条消息？

您可以在单个请求负载内对多个消息进行分组，并将它们流传输到 [!DNL Platform]. 正确使用时，在单个请求内对多个消息进行分组是优化数据操作的绝佳方式。 请阅读 [在请求中发送多条消息](../tutorials/streaming-multiple-messages.md) 以了解更多信息。

### 如何知道我发送的数据是否被接收？

发送到的所有数据 [!DNL Platform] （成功或其他情况下）在作为批处理文件存储，然后再保留在数据集中。 批次的处理状态显示在发送到的数据集中。

您可以通过使用 [Experience Platform用户界面](https://platform.adobe.com). 单击 **[!UICONTROL 数据集]** 在左侧导航中，显示数据集列表。 从显示列表中选择要流式处理到的数据集以打开其 **[!UICONTROL 数据集活动]** 页面，显示选定时间段内发送的所有批次。 有关使用的更多信息 [!DNL Experience Platform] 要监视数据流，请参阅 [监控流数据流](../quality/monitor-data-ingestion.md).

如果您的数据未能摄取，并且您希望从 [!DNL Platform]，则可以通过将失败的批次的ID发送到 [!DNL Data Access API]. 请参阅 [检索失败批次](../quality/retrieve-failed-batches.md) 以了解更多信息。

### 为什么我的流数据在数据湖中不可用？

批量摄取可能无法达到的原因有多种 [!DNL Data Lake]，例如格式无效、缺少数据或系统错误。 要确定批处理失败的原因，您必须使用 [!DNL Data Ingestion Service API] 并查看其详细信息。 有关检索失败批次的详细步骤，请参阅 [检索失败批次](../quality/retrieve-failed-batches.md).

### 如何解析为API请求返回的响应？

您可以通过首先检查服务器响应代码来确定您的请求是否被接受来解析响应。 如果返回了成功的响应代码，则可以查看 `responses` 数组对象来确定摄取任务的状态。

成功的单消息API请求返回状态代码200。 成功（或部分成功）的批量消息API请求返回状态代码207。

以下JSON是包含两条消息的API请求的示例响应对象：一个成功，一个失败。 成功流的消息将返回 `xactionId` 属性。 无法流传输的消息将返回 `statusCode` 属性和响应 `message` 以获取更多信息。

```JSON
{
    "inletId": "9b0cb233972f3b0092992284c7353f5eead496218e8441a79b25e9421ea127f5",
    "batchId": "1565638336649:1750:244",
    "receivedTimeMs": 1565638336705,
    "responses": [
        {
            "xactionId": "1565650704337:2124:92:3"
        },
        {
            "statusCode": 400,
            "message": "inletId: [9b0cb233972f3b0092992284c7353f5eead496218e8441a
                79b25e9421ea127f5] 
                imsOrgId: [{ORG_ID}] 
                Message has unknown xdm format"
        }
    ]
}
```

### 为什么我的已发送消息未被 [!DNL Real-Time Customer Profile]?

如果 [!DNL Real-Time Customer Profile] 拒绝消息，很可能是因为身份信息不正确。 这可能是为身份提供无效值或命名空间的结果。

身份命名空间有两种类型：默认和自定义。 使用自定义命名空间时，请确保命名空间已在中注册 [!DNL Identity Service]. 请参阅 [身份命名空间概述](../../identity-service/namespaces.md) 有关使用默认和自定义命名空间的更多信息。

您可以使用 [[!DNL Experience Platform UI]](https://platform.adobe.com) ，以了解有关消息摄取失败原因的更多信息。 单击 **[!UICONTROL 监控]** 在左侧导航中，查看 **[!UICONTROL 流式处理端到端]** 选项卡，以查看在选定时间段内流式处理的消息批次。
