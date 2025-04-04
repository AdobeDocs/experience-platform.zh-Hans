---
keywords: Experience Platform；主页；热门主题；流；流式摄取；疑难解答；流式摄取疑难解答；流式摄取常见问题解答；常见问题解答；
solution: Experience Platform
title: 流摄取疑难解答指南
description: 本文档提供了有关Adobe Experience Platform上的流式摄取的常见问题解答。
exl-id: 5d5deccf-25b8-44c9-ae27-9a4713ced274
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '1026'
ht-degree: 0%

---

# 流摄取疑难解答指南

本文档提供了有关Adobe Experience Platform上的流式摄取的常见问题解答。 有关其他[!DNL Experience Platform]服务（包括在所有[!DNL Experience Platform] API中遇到的服务）的问题和疑难解答，请参阅[Experience Platform疑难解答指南](../../landing/troubleshooting.md)。

Adobe Experience Platform [!DNL Data Ingestion]提供可用于将数据摄取到[!DNL Experience Platform]的RESTful API。 摄取的数据用于近乎实时地更新各个客户配置文件，使您能够跨多个渠道提供个性化、相关的体验。 请阅读[数据引入概述](../home.md)，了解有关该服务和不同引入方法的更多信息。 有关如何使用流式引入API的步骤，请阅读[流式引入概述](../streaming-ingestion/overview.md)。

## 常见问题解答

以下是有关流式摄取的常见问题解答列表。

### 如何确认我发送的有效负载的格式正确？

[!DNL Data Ingestion]利用[!DNL Experience Data Model] (XDM)架构来验证传入数据的格式。 发送与预定义XDM架构结构不符的数据将导致摄取失败。 有关XDM及其在[!DNL Experience Platform]中的使用的更多信息，请参阅[XDM系统概述](../../xdm/home.md)。

流式摄取支持两种验证模式：同步和异步。 每个验证方法处理失败数据的方式各不相同。

在开发过程中应使用&#x200B;**同步验证**。 未通过验证的记录将被丢弃，并返回一条错误消息，说明它们失败的原因（例如：“无效的XDM消息格式”）。

**应在生产中使用异步验证**。 任何未通过验证的格式错误的数据将作为失败的批处理文件发送到[!DNL Data Lake]，稍后可以在其中检索该数据以供进一步分析。

有关同步和异步验证的详细信息，请参阅[流式验证概述](../quality/streaming-validation.md)。 有关如何查看验证失败的批次的步骤，请参阅有关[检索失败的批次](../quality/retrieve-failed-batches.md)的指南。

### 能否先验证请求有效负荷，然后再将其发送至[!DNL Experience Platform]？

请求有效负载只能在发送到[!DNL Experience Platform]后评估。 执行同步验证时，有效负载会返回填充的JSON对象，而无效负载会返回错误消息。 在异步验证期间，服务会检测任何格式错误的数据并将其发送给[!DNL Data Lake]，以便稍后检索这些数据进行分析。 有关详细信息，请参阅[流式验证概述](../quality/streaming-validation.md)。

### 在不支持同步验证的边缘上请求同步验证时，会发生什么情况？

当请求的位置不支持同步验证时，将返回501错误响应。 有关同步验证的更多信息，请参阅[流式验证概述](../quality/streaming-validation.md)。

### 如何确保仅从可信来源收集数据？

[!DNL Experience Platform]支持安全的数据收集。 启用经过身份验证的数据收集后，客户端必须发送JSON Web令牌(JWT)及其组织ID作为请求标头。 有关如何将经过身份验证的数据发送到[!DNL Experience Platform]的更多信息，请参阅[经过身份验证的数据收集](../tutorials/create-authenticated-streaming-connection.md)指南。

### 将数据流式传输到[!DNL Real-Time Customer Profile]的延迟是多少？

流式处理事件通常在60秒内反映在[!DNL Real-Time Customer Profile]中。 实际延迟可能因数据量、消息大小和带宽限制而异。

### 我是否可以在同一API请求中包含多条消息？

您可以在单个请求有效负荷中对多个消息进行分组，并将它们流式传输到[!DNL Experience Platform]。 正确使用时，在一个请求中对多个消息进行分组是优化数据操作的绝佳方法。 请阅读有关[在请求中发送多条消息](../tutorials/streaming-multiple-messages.md)的教程，以了解更多信息。

### 如何知道我发送的数据是否正在接收？

发送到[!DNL Experience Platform]的所有数据（无论成功还是否）在保留到数据集之前都作为批处理文件存储。 批次的处理状态将显示在它们所发送的数据集内。

通过使用[Experience Platform用户界面](https://platform.adobe.com)检查数据集活动，您可以验证是否已成功摄取数据。 单击左侧导航中的&#x200B;**[!UICONTROL 数据集]**&#x200B;以显示数据集列表。 从显示的列表中选择要流式处理的数据集，以打开其&#x200B;**[!UICONTROL 数据集活动]**&#x200B;页面，其中显示选定时间段内发送的所有批次。 有关使用[!DNL Experience Platform]监视数据流的详细信息，请参阅[监视流式数据流](../quality/monitor-data-ingestion.md)指南。

如果数据未能摄取，并且要从[!DNL Experience Platform]中恢复它，可以通过将失败批次的ID发送到[!DNL Data Access API]来检索它们。 有关详细信息，请参阅[检索失败的批次](../quality/retrieve-failed-batches.md)指南。

### 为什么我的流数据在数据湖中不可用？

批量摄取可能无法达到[!DNL Data Lake]的原因有很多，例如格式无效、缺少数据或系统错误。 要确定批次失败的原因，您必须使用[!DNL Data Ingestion Service API]检索批次并查看其详细信息。 有关检索失败批次的详细步骤，请参阅[检索失败批次](../quality/retrieve-failed-batches.md)指南。

### 如何解析针对API请求返回的响应？

您可以通过首先检查服务器响应代码来确定您的请求是否被接受，来解析响应。 如果返回成功的响应代码，则可以查看`responses`数组对象以确定摄取任务的状态。

成功的单消息API请求返回状态代码200。 成功（或部分成功）的批量消息API请求返回状态代码207。

以下JSON是包含两条消息的API请求的示例响应对象：一条成功一条失败。 成功流式处理的消息返回`xactionId`属性。 未能流化的消息返回`statusCode`属性和包含更多信息的响应`message`。

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

### 为什么[!DNL Real-Time Customer Profile]未接收我的已发送消息？

如果[!DNL Real-Time Customer Profile]拒绝消息，则很可能是由于标识信息不正确所致。 这可能是由于为标识提供无效值或命名空间而导致的结果。

有两种类型的身份命名空间：默认和自定义。 使用自定义命名空间时，请确保命名空间已在[!DNL Identity Service]内注册。 有关使用默认和自定义命名空间的更多信息，请参阅[身份命名空间概述](../../identity-service/features/namespaces.md)。

您可以使用[[!DNL Experience Platform UI]](https://platform.adobe.com)查看有关消息引入失败原因的更多信息。 在左侧导航中单击&#x200B;**[!UICONTROL 监视]**，然后查看&#x200B;**[!UICONTROL 流端到端]**&#x200B;选项卡，以查看在选定时间段内流式传输的消息批次。
