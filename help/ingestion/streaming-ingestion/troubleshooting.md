---
keywords: Experience Platform;home;popular topics;streaming
solution: Experience Platform
title: 流摄取疑难解答
topic: troubleshooting
translation-type: tm+mt
source-git-commit: 1b398e479137a12bcfc3208d37472aae3d6721e1
workflow-type: tm+mt
source-wordcount: '997'
ht-degree: 0%

---


# 流式摄取疑难解答指南

此文档提供有关在Adobe Experience Platform流式摄取的常见问题的解答。 有关其他服务(包括所有API [!DNL Platform] 中遇到的服务)的问题和疑难解 [!DNL Platform] 答，请参阅 [Experience Platform疑难解答指南](../../landing/troubleshooting.md)。

Adobe Experience Platform [!DNL Data Ingestion] 提供REST风格的API，您可以使用它将数据引入 [!DNL Experience Platform]中。 摄取的数据用于几乎实时地更新个别客户用户档案，使您能够跨多个渠道提供个性化的相关体验。 请阅读数 [据摄取概述](../home.md) ，了解有关服务和不同摄取方法的更多信息。 有关如何使用流式摄取API的步骤，请阅读流式摄 [取概述](../streaming-ingestion/overview.md)。

## 常见问题解答

以下是有关流摄取的常见问题的一列表解答。

### 如何知道我发送的有效负荷格式正确？

[!DNL Data Ingestion] 利 [!DNL Experience Data Model] 用(XDM)模式验证传入数据的格式。 发送不符合预定义XDM模式结构的数据将导致摄取失败。 有关XDM及其在中的使用的详细 [!DNL Experience Platform]信息，请参 [阅XDM系统概述](../../xdm/home.md)。

流摄取支持两种验证模式：同步和异步。 每个验证方法处理失败数据的方式都不同。

**在开发过程中** ，应使用同步验证。 失败验证的记录将被删除，并返回错误消息，说明失败的原因(例如：“XDM消息格式无效”)。

**应在生产** 中使用异步验证。 任何未通过验证的格式错误的数据将作为失败的批 [!DNL Data Lake] 处理文件发送到该文件，稍后可在该文件中检索以进一步分析。

有关同步和异步验证的更多信息，请参阅流 [验证概述](../quality/streaming-validation.md)。 有关如何视图验证失败的批的步骤，请参阅检索失败批 [的指南](../quality/retrieve-failed-batches.md)。

### 我是否可以在将请求有效负荷发送到之前验证它 [!DNL Platform]?

请求有效负荷只有在发送到之后才能进行评估 [!DNL Platform]。 执行同步验证时，有效负载返回已填充的JSON对象，而无效负载返回错误消息。 在异步验证期间，服务会检测任何格式错误的数据，并将其发 [!DNL Data Lake] 送到以后可以检索到的分析。 有关更多 [信息，请参见](../quality/streaming-validation.md) “流验证”概述。

### 在不支持同步验证的边缘上请求同步验证时，会出现什么情况？

当请求的位置不支持同步验证时，将返回501错误响应。 有关同步验证 [的更多信息](../quality/streaming-validation.md) ，请参阅流验证概述。

### 如何确保仅从可信源收集数据？

[!DNL Experience Platform] 支持安全的数据收集。 启用身份验证数据收集后，客户端必须发送JSON Web令牌(JWT)及其IMS组织ID作为请求标头。 有关如何将已验证的数据发送到的更 [!DNL Platform]多信息，请参阅已验证 [数据收集指南](../tutorials/create-authenticated-streaming-connection.md)。

### 流数据的延迟是什么 [!DNL Real-time Customer Profile]?

流式事件通常在60秒 [!DNL Real-time Customer Profile] 内即可反映。 实际延迟可能因数据量、消息大小和带宽限制而有所不同。

### 我是否可以在同一API请求中包含多条消息？

您可以将多个消息分组到单个请求有效负荷中，并将它们流式传 [!DNL Platform]输。 正确使用时，在单个请求中对多个消息进行分组是优化数据操作的最佳方式。 请阅读教程，了 [解有关在请求中发送多条消息](../tutorials/streaming-multiple-messages.md) 。

### 如何知道我发送的数据是否被接收？

发送到的所有数据( [!DNL Platform] 成功或以其他方式)在保留到数据集中之前都会作为批处理文件存储。 批处理状态显示在发送到的数据集中。

您可以使用活动用户界面检查数据集Experience Platform，以验证数据是否 [已成功摄取](https://platform.adobe.com)。 单击 **[!UICONTROL 左侧导航]** 中的“数据集”以显示数据集列表。 从显示的列表中选择要流式传送到的数据集以打开其“ *[!UICONTROL 数据集活动]* ”页，显示选定时间段内发送的所有批。 有关使用监视数 [!DNL Experience Platform] 据流的详细信息，请参阅监视流 [数据流的指南](../quality/monitor-data-flows.md)。

如果您的数据未能摄取，并且您希望从中恢复 [!DNL Platform]该数据，则可以通过将失败的批次的ID发送到 [!DNL Data Access API]。 有关详细信息，请 [参阅检索失败批](../quality/retrieve-failed-batches.md) “指南”。

### 为什么我的流数据在数据湖中不可用？

批摄取可能无法达到的原因有多种， [!DNL Data Lake]如格式无效、缺少数据或系统错误。 要确定批处理失败的原因，您必须使用和视图其详细 [!DNL Data Ingestion Service API] 信息来检索批处理。 有关检索失败批的详细步骤，请参阅检索失败 [批的指南](../quality/retrieve-failed-batches.md)。

### 如何分析为API请求返回的响应？

您可以首先检查服务器响应代码，确定您的请求是否被接受，从而解析响应。 如果返回成功的响应代码，则可以查看 `responses` 数组对象以确定摄取任务的状态。

成功的单消息API请求返回状态代码200。 成功（或部分成功）的批处理消息API请求返回状态代码207。

以下JSON是包含两条消息的API请求的示例响应对象：一个成功，一个失败。 成功流化的消息返回 `xactionId` 属性。 无法流化的消息将返回一 `statusCode` 个属性和包含更多 `message` 信息的响应。

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

### 为什么我的已发送邮件未被接收 [!DNL Real-time Customer Profile]?

如果 [!DNL Real-time Customer Profile] 拒绝某条消息，则很可能是因为身份信息不正确。 这可能是为身份提供无效值或命名空间的结果。

有两种身份命名空间:默认和自定义。 使用自定义命名空间时，请确保命名空间已在中注册 [!DNL Identity Service]。 有关使用 [默认命名空间和自定义](../../identity-service/namespaces.md) ，请参阅标识命名空间概述。

您可以使用 [[!DNLExperience PlatformUI]](https://platform.adobe.com) ，查看有关消息失败接收原因的更多信息。 单击 **[!UICONTROL 左侧导航]** 中的“监视”，然后视图“ _[!UICONTROL 流式端到端”选项卡]_ ，以查看在选定时间段内流化的消息批。