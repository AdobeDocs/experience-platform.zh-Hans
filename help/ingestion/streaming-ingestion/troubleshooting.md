---
keywords: Experience Platform；主页；热门主题；流；流摄取；故障排除；流摄取故障排除；流摄取常见问题解答；常见问题解答；
solution: Experience Platform
title: 流摄取疑难解答指南
description: 本文档提供了有关Adobe Experience Platform上流式摄取的常见问题解答。
exl-id: 5d5deccf-25b8-44c9-ae27-9a4713ced274
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '1024'
ht-degree: 0%

---

# 流摄取疑难解答指南

本文档提供了有关Adobe Experience Platform上流式摄取的常见问题解答。 有关其他方面的问题和疑难解答 [!DNL Platform] 服务，包括所有体验中的服务 [!DNL Platform] API，请参阅 [Experience Platform疑难解答指南](../../landing/troubleshooting.md).

Adobe Experience Platform [!DNL Data Ingestion] 提供可用于将数据摄取到的RESTful API [!DNL Experience Platform]. 摄取的数据用于近乎实时地更新各个客户配置文件，允许您跨多个渠道提供个性化、相关的体验。 请阅读 [数据引入概述](../home.md) 以了解有关服务和不同摄取方法的更多信息。 有关如何使用流摄取API的步骤，请阅读 [流式摄取概述](../streaming-ingestion/overview.md).

## 常见问题解答

以下是有关流式摄取的常见问题解答列表。

### 如何确认我发送的有效负载的格式正确？

[!DNL Data Ingestion] 利用 [!DNL Experience Data Model] (XDM)架构来验证传入数据的格式。 发送不符合预定义XDM架构的数据将导致摄取失败。 有关XDM及其在 [!DNL Experience Platform]，请参见 [XDM系统概述](../../xdm/home.md).

流式摄取支持两种验证模式：同步和异步。 每个验证方法处理失败数据的方式各不相同。

**同步验证** 应在开发过程中使用。 验证失败的记录将被丢弃，并返回一条错误消息，说明失败的原因（例如：“无效的XDM消息格式”）。

**异步验证** 应该在生产中使用。 任何未通过验证的格式错误的数据都会发送到 [!DNL Data Lake] 作为失败的批处理文件，以后可以在其中检索该文件以供进一步分析。

有关同步和异步验证的详细信息，请参见 [流验证概述](../quality/streaming-validation.md). 有关如何查看未通过验证的批处理的步骤，请参阅以下指南中的 [检索失败的批次](../quality/retrieve-failed-batches.md).

### 我是否可以在将请求有效负载发送到之前对其进行验证 [!DNL Platform]？

请求有效负载只有在发送到之后才能评估 [!DNL Platform]. 执行同步验证时，有效负载会返回填充的JSON对象，而无效负载会返回错误消息。 在异步验证期间，该服务会检测任何格式错误的数据并将其发送给 [!DNL Data Lake] 可在其中检索数据以供分析。 请参阅 [流验证概述](../quality/streaming-validation.md) 了解更多信息。

### 在不支持同步验证的边缘上请求同步验证时，会发生什么情况？

当请求的位置不支持同步验证时，将返回501错误响应。 请查看 [流验证概述](../quality/streaming-validation.md) 有关同步验证的详细信息。

### 如何确保仅从可信来源收集数据？

[!DNL Experience Platform] 支持安全的数据收集。 启用经过身份验证的数据收集后，客户端必须发送JSON Web令牌(JWT)及其组织ID作为请求标头。 有关如何将经过身份验证的数据发送到的详细信息 [!DNL Platform]，请参阅指南，网址为 [经过身份验证的数据收集](../tutorials/create-authenticated-streaming-connection.md).

### 流数据到达“ ”的延迟是多少 [!DNL Real-Time Customer Profile]？

流式处理事件通常反映在 [!DNL Real-Time Customer Profile] 在60秒内。 实际延迟可能因数据量、消息大小和带宽限制而异。

### 我是否可以在同一API请求中包含多条消息？

您可以在单个请求有效负载中对多个消息进行分组，并将它们流式传输到 [!DNL Platform]. 正确使用时，在单个请求中对多个消息进行分组是优化数据操作的绝佳方法。 请阅读以下教程： [在请求中发送多条消息](../tutorials/streaming-multiple-messages.md) 了解更多信息。

### 如何知道我发送的数据是否正在接收？

所有发送到的数据 [!DNL Platform] （成功或不成功）存储为批处理文件，然后保留在数据集中。 批次的处理状态将显示在它们所发送的数据集中。

您可以使用检查数据集活动，以验证是否已成功摄取数据 [Experience Platform用户界面](https://platform.adobe.com). 单击 **[!UICONTROL 数据集]** 在左侧导航中显示数据集列表。 从显示的列表中选择要流式处理的数据集以打开其 **[!UICONTROL 数据集活动]** 页，显示在选定时间段发送的所有批次。 有关使用的更多信息 [!DNL Experience Platform] 要监视数据流，请参阅上的指南 [监控流数据流](../quality/monitor-data-ingestion.md).

如果您的数据无法摄取，并且您想从中恢复它 [!DNL Platform]，您可以通过将ID发送至 [!DNL Data Access API]. 请参阅指南，网址为 [检索失败的批次](../quality/retrieve-failed-batches.md) 了解更多信息。

### 为什么我的流数据在数据湖中不可用？

批量摄取可能无法达到的原因有很多 [!DNL Data Lake]，例如格式无效、缺少数据或系统错误。 要确定批次失败的原因，您必须使用 [!DNL Data Ingestion Service API] 并查看其详细信息。 有关检索失败的批次的详细步骤，请参阅以下指南中的 [检索失败的批次](../quality/retrieve-failed-batches.md).

### 如何解析为API请求返回的响应？

您可以通过首先检查服务器响应代码来确定您的请求是否被接受，来解析响应。 如果返回了成功的响应代码，则可以查看 `responses` 数组对象，用于确定摄取任务的状态。

成功的单消息API请求返回状态代码200。 成功（或部分成功）的批处理消息API请求返回状态代码207。

以下JSON是API请求的示例响应对象，其中包含两条消息：一条成功一条失败。 成功流式传输的消息返回 `xactionId` 属性。 无法流式处理的消息将返回 `statusCode` 属性和响应 `message` 提供更多信息。

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

### 为什么我的已发送消息没有被 [!DNL Real-Time Customer Profile]？

如果 [!DNL Real-Time Customer Profile] 拒绝消息，这很可能是由于身份信息不正确所致。 这可能是由于为标识提供无效值或命名空间所导致。

有两种类型的身份命名空间：默认和自定义。 使用自定义命名空间时，请确保命名空间已在中注册 [!DNL Identity Service]. 请参阅 [身份命名空间概述](../../identity-service/namespaces.md) 有关使用默认命名空间和自定义命名空间的更多信息。

您可以使用 [[!DNL Experience Platform UI]](https://platform.adobe.com) 查看有关消息引入失败原因的更多信息。 单击 **[!UICONTROL 监测]** 然后，在左侧导航中查看 **[!UICONTROL 端到端的流式传输]** 制表符，以查看在选定时间段内流式处理的消息批次。
