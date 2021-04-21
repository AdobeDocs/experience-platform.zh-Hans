---
keywords: Experience Platform；主页；热门主题；流；流摄取；疑难解答；流摄取疑难解答；流摄取常见问题；常见问题解答；
solution: Experience Platform
title: 流摄取疑难解答指南
topic-legacy: troubleshooting
description: 此文档提供有关Adobe Experience Platform上流式摄取的常见问题解答。
exl-id: 5d5deccf-25b8-44c9-ae27-9a4713ced274
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1019'
ht-degree: 0%

---

# 流式摄取疑难解答指南

此文档提供有关Adobe Experience Platform上流式摄取的常见问题解答。 有关其他[!DNL Platform]服务（包括所有[!DNL Platform] API中遇到的服务）的问题和疑难解答，请参阅[Experience Platform疑难解答指南](../../landing/troubleshooting.md)。

Adobe Experience Platform [!DNL Data Ingestion]提供RESTful API，您可以使用它将数据收录到[!DNL Experience Platform]中。 摄取的数据用于几乎实时地更新个别用户档案，使您能够跨多个渠道提供个性化、相关的体验。 请阅读[数据摄取概述](../home.md)，了解有关服务和不同摄取方法的详细信息。 有关如何使用流式摄取API的步骤，请阅读[流式摄取概述](../streaming-ingestion/overview.md)。

## 常见问题解答

以下是有关流摄取的常见问题的列表答案。

### 我如何知道我发送的负载格式正确？

[!DNL Data Ingestion] 利 [!DNL Experience Data Model] 用(XDM)模式验证传入数据的格式。发送不符合预定义XDM模式结构的数据将导致摄取失败。 有关XDM及其在[!DNL Experience Platform]中的使用的详细信息，请参阅[ XDM系统概述](../../xdm/home.md)。

流摄取支持两种验证模式：同步和异步。 每个验证方法处理失败数据的方式都不同。

**在开** 发过程中应使用同步验证。将删除失败验证的记录，并返回错误消息，说明失败的原因(例如：“XDM消息格式无效”)。

**生产** 中应使用异步验证。任何未通过验证的格式错误的数据将作为失败的批处理文件发送到[!DNL Data Lake]，稍后可在其中检索以进一步分析。

有关同步和异步验证的详细信息，请参阅[流验证概述](../quality/streaming-validation.md)。 有关如何视图未通过验证的批的步骤，请参阅[检索失败批](../quality/retrieve-failed-batches.md)的指南。

### 我是否可以在将请求有效负荷发送到[!DNL Platform]之前验证它？

请求负载只能在发送到[!DNL Platform]之后才能评估。 执行同步验证时，有效负载将返回已填充的JSON对象，而无效负载将返回错误消息。 在异步验证期间，服务会检测任何格式错误的数据并将其发送到[!DNL Data Lake]，以后可以在中检索它以进行分析。 有关详细信息，请参阅[流验证概述](../quality/streaming-validation.md)。

### 在不支持同步验证的边缘上请求同步验证时，会出现什么情况？

当请求的位置不支持同步验证时，将返回501错误响应。 有关同步验证的详细信息，请参阅[流验证概述](../quality/streaming-validation.md)。

### 如何确保仅从受信任的源收集数据？

[!DNL Experience Platform] 支持安全的数据收集。启用身份验证数据收集后，客户端必须将JSON Web Token(JWT)及其IMS组织ID作为请求标头发送。 有关如何向[!DNL Platform]发送已验证数据的详细信息，请参阅[已验证数据收集](../tutorials/create-authenticated-streaming-connection.md)的指南。

### 流数据到[!DNL Real-time Customer Profile]的延迟是什么？

流事件通常在60秒内反映在[!DNL Real-time Customer Profile]中。 实际延迟可能因数据量、消息大小和带宽限制而异。

### 我是否可以在同一API请求中包含多条消息？

您可以将多个消息组合到单个请求有效负荷中，并将它们流化到[!DNL Platform]。 正确使用时，在一个请求中对多个消息进行分组是优化数据操作的绝佳方式。 请阅读有关[在请求](../tutorials/streaming-multiple-messages.md)中发送多条消息的教程以了解更多信息。

### 如何知道我发送的数据是否被接收？

发送到[!DNL Platform]（成功或以其他方式）的所有数据在数据集中保留之前都会作为批处理文件存储。 批处理状态显示在发送到的数据集中。

您可以通过使用[Experience Platform用户界面](https://platform.adobe.com)检查数据集活动来验证数据是否已成功摄取。 单击左侧导航中的&#x200B;**[!UICONTROL Datasets]**&#x200B;以显示列表集。 从显示的列表中选择要流式处理的数据集以打开其&#x200B;**[!UICONTROL Dataset activity]**&#x200B;页面，显示选定时间段内发送的所有批。 有关使用[!DNL Experience Platform]监视数据流的详细信息，请参见[监视流数据流](../quality/monitor-data-ingestion.md)的指南。

如果您的数据未能摄取，并且希望从[!DNL Platform]恢复，则可以通过将失败的批次的ID发送到[!DNL Data Access API]来检索失败的批次。 有关详细信息，请参阅[检索失败批](../quality/retrieve-failed-batches.md)指南。

### 为什么我的流数据在数据湖中不可用？

批摄取可能无法到达[!DNL Data Lake]的原因有多种，如格式无效、缺少数据或系统错误。 要确定批处理失败的原因，必须使用[!DNL Data Ingestion Service API]检索批处理并视图其详细信息。 有关检索失败批的详细步骤，请参阅[检索失败批](../quality/retrieve-failed-batches.md)指南。

### 如何分析为API请求返回的响应？

您可以首先检查服务器响应代码以确定您的请求是否被接受，从而解析响应。 如果返回了成功的响应代码，则可查看`responses`数组对象以确定摄取任务的状态。

成功的单消息API请求返回状态代码200。 成功（或部分成功）的批消息API请求返回状态代码207。

以下JSON是包含两条消息的API请求的示例响应对象：一个成功，一个失败。 成功以流方式传输的消息返回`xactionId`属性。 失败的消息将返回`statusCode`属性和包含详细信息的响应`message`。

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

### 为什么我的已发送邮件未被[!DNL Real-time Customer Profile]接收？

如果[!DNL Real-time Customer Profile]拒绝消息，则最可能是由于身份信息不正确所致。 这可能是为身份提供无效值或命名空间的结果。

有两种身份命名空间:默认和自定义。 使用自定义命名空间时，请确保已在[!DNL Identity Service]中注册命名空间。 有关使用默认和自定义命名空间的详细信息，请参阅[标识命名空间概述](../../identity-service/namespaces.md)。

您可以使用[[!DNL Experience Platform UI]](https://platform.adobe.com)查看有关消息接收失败原因的更多信息。 单击左侧导航中的&#x200B;**[!UICONTROL Monitoring]**，然后视图&#x200B;**[!UICONTROL Streaming end-to-end]**&#x200B;选项卡，以查看在选定时间段内流化的消息批。
