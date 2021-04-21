---
keywords: Experience Platform；主页；热门主题
solution: Experience Platform
title: 导入和使用外部受众
description: 请阅读本教程，了解如何将外部受众与Adobe Experience Platform一起使用。
topic-legacy: tutorial
exl-id: 56fc8bd3-3e62-4a09-bb9c-6caf0523f3fe
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '629'
ht-degree: 0%

---

# 导入和使用外部受众

Adobe Experience Platform支持导入外部受众的功能，该功能随后可用作新区段定义的组件。 本文档提供了设置Experience Platform以导入和使用外部受众的教程。

## 入门指南

- [分段服务](../home.md):允许您根据实时受众用户档案数据构建客户细分。
- [实时客户用户档案](../../profile/home.md):根据来自多个来源的汇总数据提供统一、实时的消费者用户档案。
- [体验数据模型(XDM)](../../xdm/home.md):平台通过该标准化框架组织客户体验数据。
- [数据集](../../catalog/datasets/overview.md):存储和管理结构，用于Experience Platform中的数据持久性。
- [流摄取](../../ingestion/streaming-ingestion/overview.md):Experience Platform如何从客户端和服务器端设备实时摄取和存储数据。

## 为外部命名空间创建标识受众

使用外部受众的第一步是创建身份命名空间。 身份命名空间允许平台关联区段的来源。

要创建身份命名空间，请按照[身份命名空间指南](../../identity-service/namespaces.md#manage-namespaces)中的说明操作。 创建身份命名空间时，将源详细信息添加到身份命名空间，并将其[!UICONTROL Type]标记为&#x200B;**[!UICONTROL Non-people identifier]**。

![](../images/tutorials/external-audiences/identity-namespace-info.png)

## 为区段元数据创建模式

创建身份命名空间后，您需要为要创建的区段创建新模式。

要开始合成模式，请首先在左侧导航栏上选择&#x200B;**[!UICONTROL Schemas]**，然后在模式工作区右上角选择&#x200B;**[!UICONTROL Create schema]**。 从此处，选择&#x200B;**[!UICONTROL Browse]**&#x200B;以查看可用模式类型的完整选择。

![](../images/tutorials/external-audiences/create-schema-browse.png)

由于您正在创建区段定义（它是预定义的类），因此请选择&#x200B;**[!UICONTROL Use existing class]**。 现在，选择&#x200B;**[!UICONTROL Segment definition]**&#x200B;类，后跟&#x200B;**[!UICONTROL Assign class]**。

![](../images/tutorials/external-audiences/assign-class.png)

创建模式后，您需要指定将包含区段ID的字段。 此字段应标记为主标识并分配给您之前创建的命名空间。

![](../images/tutorials/external-audiences/mark-primary-identifier.png)

在将`_id`字段标记为主标识后，选择模式的标题，然后选择标记为&#x200B;**[!UICONTROL Profile]**&#x200B;的切换。 选择&#x200B;**[!UICONTROL Enable]**&#x200B;以启用[!DNL Real-time Customer Profile]的模式。

![](../images/tutorials/external-audiences/schema-profile.png)

现在，此模式已启用用户档案，主标识已分配给您创建的非人身标识命名空间。 因此，这意味着使用此模式导入到平台中的细分元数据将被引入用户档案中，而不会与其他与人相关的用户档案数据合并。

## 为模式创建数据集

配置模式后，您需要为区段元数据创建数据集。

要创建数据集，请按照[数据集用户指南](../../catalog/datasets/user-guide.md#create)中的说明操作。 您将希望使用之前创建的模式，按照&#x200B;**[!UICONTROL Create dataset from schema]**&#x200B;选项操作。

![](../images/tutorials/external-audiences/select-schema.png)

创建数据集后，请继续按照[数据集用户指南](../../catalog/datasets/user-guide.md#enable-profile)中的说明，启用此数据集以进行实时客户用户档案。

![](../images/tutorials/external-audiences/dataset-profile.png)

## 设置和导入受众数据

启用数据集后，现在可以通过UI或使用Experience PlatformAPI将数据发送到平台。 要将此数据引入平台，您需要创建流连接。

要创建流连接，您可以按照[API教程](../../sources/tutorials/api/create/streaming/http.md)或[UI教程](../../sources/tutorials/ui/create/streaming/http.md)中的说明进行操作。

创建流连接后，您将有权访问可将数据发送到的唯一流端点。 要了解如何将数据发送到这些端点，请阅读有关流记录数据](../../ingestion/tutorials/streaming-record-data.md#ingest-data)的[教程。

![](../images/tutorials/external-audiences/get-streaming-endpoint.png)

## 使用导入的受众构建区段

设置导入的受众后，即可将其用作分段过程的一部分。 要查找外部受众，请转到“区段生成器”，然后在&#x200B;**[!UICONTROL Fields]**&#x200B;部分选择&#x200B;**[!UICONTROL Audiences]**&#x200B;选项卡。

![](../images/tutorials/external-audiences/external-audiences.png)

## 后续步骤

现在，您可以在区段中使用外部受众，因此可以使用区段生成器创建区段。 要了解如何创建区段，请阅读[有关创建区段的教程](./create-a-segment.md)。
