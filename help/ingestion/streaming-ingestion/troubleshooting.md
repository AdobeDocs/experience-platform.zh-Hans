---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 流摄取疑难解答
topic: troubleshooting
translation-type: tm+mt
source-git-commit: 0eecd802fc8d0ace3a445f3f188a7f095b97d0c8
workflow-type: tm+mt
source-wordcount: '1046'
ht-degree: 0%

---


# 流式摄取疑难解答指南

此文档提供有关Adobe Experience Platform上流式摄取的常见问题的解答。 有关其他平台服务（包括所有平台API中遇到的服务）的问题和疑难解答，请参阅Experience Platform [疑难解答指南](../../landing/troubleshooting.md)。

Adobe Experience Platform Data Ingestion提供REST风格的API，可用于将数据引入Experience Platform。 摄取的数据用于几乎实时地更新个别客户用户档案，使您能够跨多个渠道提供个性化的相关体验。 请阅读数 [据摄取概述](../home.md) ，了解有关服务和不同摄取方法的更多信息。 有关如何使用流式摄取API的步骤，请阅读流式摄 [取概述](../streaming-ingestion/overview.md)。

## 常见问题解答

以下是有关流摄取的常见问题的一列表解答。

### 如何知道我发送的有效负荷格式正确？

数据摄取利用体验数据模型(XDM)模式验证传入数据的格式。 发送不符合预定义XDM模式结构的数据将导致摄取失败。 有关XDM及其在Experience Platform中的使用的更多信息，请参 [阅XDM系统概述](../../xdm/home.md)。

流摄取支持两种验证模式： 同步和异步。 每个验证方法处理失败数据的方式都不同。

**在开发过程中** ，应使用同步验证。 失败验证的记录将被删除，并返回错误消息，说明失败的原因(例如： “XDM消息格式无效”)。

**应在生产** 中使用异步验证。 任何未通过验证的格式错误的数据都将作为失败的批处理文件发送到数据湖，稍后可以检索它以进一步分析。

有关同步和异步验证的更多信息，请参阅流 [验证概述](../quality/streaming-validation.md)。 有关如何视图验证失败的批的步骤，请参阅检索失败批 [的指南](../quality/retrieve-failed-batches.md)。

### 我是否可以在将请求有效负荷发送到平台之前验证它？

请求有效负载只有在发送到平台后才能进行评估。 执行同步验证时，有效负载返回已填充的JSON对象，而无效负载返回错误消息。 在异步验证期间，服务会检测任何格式错误的数据并将其发送到数据湖，以后可以在该数据湖中检索它以进行分析。 有关更多 [信息，请参见](../quality/streaming-validation.md) “流验证”概述。

### 当在不支持同步验证的边缘上请求同步验证时，会出现什么情况？

当请求的位置不支持同步验证时，将返回501错误响应。 有关同步验证 [的更多信息](../quality/streaming-validation.md) ，请参阅流验证概述。

### 如何确保仅从可信源收集数据？

Experience Platform支持安全的数据收集。 启用身份验证数据收集后，客户端必须发送JSON Web令牌(JWT)及其IMS组织ID作为请求标头。 有关如何将验证数据发送到平台的更多信息，请参阅验证数据 [收集指南](../tutorials/create-authenticated-streaming-connection.md)。

### 流化数据到实时客户用户档案的延迟是什么？

流式事件通常在60秒内即可反映在实时客户用户档案中。 实际延迟可能因数据量、消息大小和带宽限制而有所不同。

### 我是否可以在同一API请求中包含多条消息？

您可以在单个请求有效负荷内对多个消息进行分组，并将它们流化到平台。 正确使用时，在单个请求中对多个消息进行分组是优化数据操作的最佳方式。 请阅读教程，了 [解有关在请求中发送多条消息](../tutorials/streaming-multiple-messages.md) 。

### 如何知道我发送的数据是否被接收？

发送到平台的所有数据（成功或以其他方式）在保留到数据集中之前作为批处理文件存储。 批处理状态显示在发送到的数据集中。

您可以使用Experience Platform用户界面检查数据集活动以验证数据 [是否已成功摄取](https://platform.adobe.com)。 单击 **左侧导航** 中的“数据集”以显示数据集列表。 从显示的列表中选择要流式传送到的数据集以打开其“ *数据集活动* ”页，显示选定时间段内发送的所有批。 有关使用Experience Platform监视数据流的更多信息，请参阅《监视流 [数据流的指南》](../quality/monitor-data-flows.md)。

如果数据未能摄取，并且要从平台中恢复，则可以通过将失败的批次的ID发送到数据访 [问API来检索它们][Data Access Service API]。 有关详细信息，请 [参阅检索失败批](../quality/retrieve-failed-batches.md) “指南”。

### 为什么我的流数据在数据湖中不可用？

批处理摄取可能无法到达数据湖的原因有多种，如格式无效、缺少数据或系统错误。 要确定批处理失败的原因，您必须使用Data Ingestion Service API检 [索批处理并视图][Data Ingestion Service] 其详细信息。 有关检索失败批的详细步骤，请参阅检索失败 [批的指南](../quality/retrieve-failed-batches.md)。

### 如何分析为API请求返回的响应？

您可以首先检查服务器响应代码，确定您的请求是否被接受，从而解析响应。 如果返回成功的响应代码，则可以查看 `responses` 数组对象以确定摄取任务的状态。

成功的单消息API请求返回状态代码200。 成功（或部分成功）的批处理消息API请求返回状态代码207。

以下JSON是包含两条消息的API请求的示例响应对象： 一个成功，一个失败。 成功流化的消息返回 `xactionId` 属性。 无法流化的消息将返回一 `statusCode` 个属性和包含更多 `message` 信息的响应。

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
                imsOrgId: [{IMS_ORG}] 
                Message has unknown xdm format"
        }
    ]
}
```

### 为什么实时客户用户档案未收到我的发送消息？

如果实时客户用户档案拒绝消息，则很可能是由于身份信息不正确所致。 这可能是为身份提供无效值或命名空间的结果。

有两种身份命名空间: 默认和自定义。 使用自定义命名空间时，请确保命名空间已在Identity Service中注册。 有关使用 [默认命名空间和自定义](../../identity-service/namespaces.md) ，请参阅标识命名空间概述。

您可以使用Experience [Platform UI](https://platform.adobe.com) ，查看有关消息失败接收原因的更多信息。 单击 **左侧导航** 中的“监视”，然后视图“ _流式端到端”选项卡_ ，以查看在选定时间段内流化的消息批。