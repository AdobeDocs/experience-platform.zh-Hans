---
keywords: Experience Platform；配置文件；实时客户配置文件；故障排除；API
title: 实时客户配置文件故障排除指南
type: Documentation
description: 本文档提供有关实时客户个人资料的常见问题解答，以及有关使用Adobe Experience Platform处理个人资料数据时常见错误的疑难解答指南。
exl-id: 0b340025-093b-41e4-8053-969a8e80e889
source-git-commit: 8ae18565937adca3596d8663f9c9e6d84b0ce95a
workflow-type: tm+mt
source-wordcount: '1007'
ht-degree: 0%

---

# 实时客户资料故障排除指南

本文档提供有关实时客户个人资料的常见问题解答，以及常见错误的故障排除指南。 有关Adobe Experience Platform中其他服务的问题和疑难解答，请参阅 [Experience Platform疑难解答指南](../landing/troubleshooting.md).

替换为 [!DNL Real-Time Customer Profile]，您可以通过组合来自多个渠道（包括在线、离线、CRM和第三方）的数据来查看每个客户的整体视图。 这使营销人员能够跨多个渠道为客户推动协调、一致且相关的体验。

## 常见问题解答

以下是有关Real-time Customer Profile的常见问题解答列表。

### Real-time Customer Profile接受哪些类型的数据？

配置文件接受两者 **记录** 和 **时间序列** 数据，只要有关数据至少包含一个标识值，将数据与唯一个人相关联。

与所有Platform服务一样，Profile要求它的数据在语义上采用Experience Data Model (XDM)架构进行结构化。 反过来，此架构必须 **主要身份** 已定义并已启用以便在配置文件中使用。

如果您不熟悉XDM，请从 [XDM概述](../xdm/home.md) 了解更多信息。 接下来，请参阅XDM用户指南，以了解操作步骤 [设置标识字段](../xdm/tutorials/create-schema-ui.md#identity-field) 和 [为配置文件启用架构](../xdm/tutorials/create-schema-ui.md#profile).

### 配置文件数据存储在何处？

Real-time Customer Profile维护其自己的数据存储（称为“配置文件存储”），独立于包含其他摄取的Platform数据的Data Lake。

### 如果我已将数据摄取到Platform，是否可以在配置文件存储区中提供该数据？

如果数据被摄取到非配置文件数据集，您必须将该数据重新摄取到启用配置文件的数据集，才能使其在配置文件存储中可用。 可以为配置文件启用现有数据集，但是在该配置之前摄取的任何数据仍将不会显示在配置文件存储中。

如果您希望将之前摄取的数据添加到配置文件存储区，请按照 [数据集配置教程](./tutorials/dataset-configuration.md) 创建新数据集或将现有数据集转换为配置文件启用的数据集，然后将所需数据重新摄取到该数据集。

### 如何查看我摄取的配置文件数据？

查看配置文件数据的方法多种多样，具体取决于您使用的是API还是UI。

#### 使用 API

如果您知道要访问的配置文件实体的ID，则可以使用 `/entities` （配置文件访问）配置文件API中的端点以查找这些实体。 请参阅以下部分： [实体](./api/entities.md) 有关更多信息，请参阅开发人员指南。

您还可以使用Adobe Experience Platform分段服务API来访问符合受众成员资格的客户的个人配置文件。 请参阅 [分段服务概述](../segmentation/home.md) 了解更多信息。

#### 使用UI

在Experience PlatformUI中， **[!UICONTROL 浏览]** 在中选项卡 **[!UICONTROL 配置文件]** 工作区允许您查看配置文件总数并按其标识值搜索各个配置文件。 请参阅 [配置文件用户指南](./ui/user-guide.md) 了解更多信息。

您还可以在 **[!UICONTROL 浏览]** 在中选项卡 **[!UICONTROL 受众]** 工作区。 选择受众后，将显示符合该受众条件的配置文件示例。 然后，您可以选择列出的任意配置文件以查看其详细信息。 请参阅 [分段UI概述](../segmentation/ui/overview.md) 了解更多信息。

## 错误代码

以下是使用Real-time Customer Profile API时可能遇到的错误消息列表。 如果此处未列出您遇到的错误，您可能会在一般情况下找到它 [平台疑难解答指南](../landing/troubleshooting.md) 而是。

### 无法查找所提供路径的计算属性的架构

```json
{
  "code": "400",
  "message": "Could not lookup schema of the computed attribute for the provided path"
}
```

创建新的计算属性时，当系统找不到请求有效负载中提供的架构时，会发生此错误。 确保您已在有效负荷的中提供正确的租户ID `path` 属性，并且其值 `schema.name` 是有效的架构名称。

如果您不知道租户ID，可以按照 [Schema Registry开发人员指南](../xdm/api/getting-started.md).

### 指定的架构或definedOn已存在同名函数

```json
{
  "code": "400",
  "message": "Function with the same name already exists for the specified schema or definedOn"
}
```

创建新的计算属性时，如果提供的是 `name` 属性已用于下所示的架构 `schema.name`. 在重试之前，请将该值替换为唯一名称。

### 表达式的返回架构与XDM架构中计算属性的架构不同

```json
{
  "code": "400",
  "message": "Return schema of the expression is not same as the schema of the computed attribute in the XDM schema"
}
```

创建新的计算属性时，如果提供的是 `name` 属性已用于下所示的架构 `schema.name`. 在重试之前，请将该值替换为唯一名称。

### 删除请求无效（配置文件系统作业）

```json
{
  "code": "400",
  "message": "Invalid delete request (Profile System Job)"
}
```

为删除系统作业提供了无效有效负载时，会发生此错误。 请确保您在有效负载下提供有效的数据集或批次ID `dataSetID` 或 `batchID` 属性。 请参阅以下部分： [创建删除请求](./api/profile-system-jobs.md#create-a-delete-request) 有关更多信息，请参阅配置文件开发人员指南。

### 未找到配置文件数据集的批次

```json
{
  "requestId":"LlTmQkhgHKFGHGHnIkmUxcIL4YTFSpQw",
  "errors":{
    "400":[
      {
        "code":"400",
        "message":"Batch not found for profile dataset '5da688d2c4e60518ad25b7b1'"
      }
    ]
  }
}
```

当尝试为配置文件数据创建删除请求时找不到有效的批次时，会发生此错误。 在重试之前，请检查您为启用配置文件的数据集输入了正确的ID。

### 尚未创建投影目标

```json
{
  "status":404,
  "title":"The projection destination has not yet been created.",
  "type":"http://ns.adobe.com/adobecloud/problem/missing-entity"
}
```

此错误发生于 `destinationId` 提供于 `POST /config/projections` 请求无效。 在重试之前，请仔细检查您是否提供了有效的目标ID。 要创建新目标，请按照 [配置文件开发人员指南](./api/edge-projections.md#create-a-destination).

### 不支持的媒体类型

```json
{
  "status": 415,
  "title": "HTTP 415 Unsupported Media Type",
  "type": "http://ns.adobe.com/adobecloud/problem/unsupported-media-type"
}
```

发送具有无效Content-Type标头的POST或PUT请求时，会发生此错误。 双击是否为您使用的端点提供有效的Content-Type值。

大多数配置文件端点都接受将“application/json”用于其Content-Type标头，但以下情况除外：

| 端点 | Content-Type |
| --- | --- |
| `/config/projections` | application/vnd.adobe.platform.projectionConfig+json； version=1 |
| `/config/destinations` | application/vnd.adobe.platform.projectionDestination+json； version=1 |
