---
keywords: Experience Platform；配置文件；实时客户配置文件；疑难解答；API
title: Real-Time Customer Profile疑难解答指南
topic-legacy: guide
type: Documentation
description: 本文档提供了有关实时客户资料的常见问题解答，以及使用Adobe Experience Platform处理资料数据时常见错误的疑难解答指南。
exl-id: 0b340025-093b-41e4-8053-969a8e80e889
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '1007'
ht-degree: 0%

---

# Real-Time Customer Profile疑难解答指南

本文档提供了有关实时客户资料的常见问题解答，以及常见错误的疑难解答指南。 有关Adobe Experience Platform中其他服务的相关问题和疑难解答，请参阅 [Experience Platform疑难解答指南](../landing/troubleshooting.md).

使用 [!DNL Real-Time Customer Profile]，您可以通过合并来自多个渠道（包括在线、离线、CRM和第三方）的数据，来全面了解每个客户。 这使营销人员能够跨多个渠道为客户提供协调一致的相关体验。

## 常见问题解答

以下是有关实时客户资料的常见问题解答列表。

### 实时客户资料接受哪类数据？

配置文件接受两者 **记录** 和 **时间序列** 数据，前提是相关数据至少包含一个标识值，该标识值将数据与唯一的个人相关联。

与所有Platform服务一样，配置文件要求在体验数据模型(XDM)架构下对其数据进行语义结构。 而此架构必须具有 **主标识** 定义并启用以在配置文件中使用。

如果您不熟悉XDM，请首先 [XDM概述](../xdm/home.md) 以了解更多。 接下来，请参阅XDM用户指南，以了解有关如何 [设置标识字段](../xdm/tutorials/create-schema-ui.md#identity-field) 和 [为配置文件启用架构](../xdm/tutorials/create-schema-ui.md#profile).

### 配置文件数据存储在何处？

实时客户资料维护其自己的数据存储（称为“资料存储”），它与包含其他摄取的平台数据的数据湖不同。

### 如果我已将数据摄取到Platform，是否可以将其添加到用户档案存储区？

如果已将数据摄取到非配置文件数据集，则必须将该数据重新摄取到启用了配置文件的数据集，以便该数据在配置文件存储中可用。 可以为配置文件启用现有数据集，但是在该配置之前摄取的任何数据仍将不会显示在配置文件存储中。

如果要将之前摄取的数据添加到用户档案存储，请按照 [数据集配置教程](./tutorials/dataset-configuration.md) 创建新数据集或转换要启用“配置文件”的现有数据集，然后将所需数据重新摄取到该数据集。

### 如何查看摄取的配置文件数据？

根据您使用的是API还是UI，可以使用多种查看配置文件数据的方法。

#### 使用 API

如果您知道要访问的配置文件实体的ID，则可以使用 `/entities` （配置文件访问）配置文件API中用于查找这些实体的端点。 请参阅 [实体](./api/entities.md) （详细信息）。

您还可以使用Adobe Experience Platform Segmentation Service API访问符合区段成员资格的客户的个人用户档案。 请参阅 [Segmentation Service概述](../segmentation/home.md) 以了解更多信息。

#### 使用UI

在Experience PlatformUI中， **[!UICONTROL 浏览]** 选项卡 **[!UICONTROL 用户档案]** 工作区允许您查看配置文件总数并按个人配置文件的标识值搜索各个配置文件。 请参阅 [用户档案用户指南](./ui/user-guide.md) 以了解更多信息。

您还可以在 **[!UICONTROL 浏览]** 选项卡 **[!UICONTROL 区段]** 工作区。 选择区段后，会显示符合该区段资格条件的用户档案示例。 然后，您可以选择其中任何列出的用户档案，以查看其详细信息。 请参阅 [分段UI概述](../segmentation/ui/overview.md) 以了解更多信息。

## 错误代码

以下是您在使用实时客户资料API时可能遇到的错误消息列表。 如果此处未列出您遇到的错误，您可能会在常规中找到该错误 [平台疑难解答指南](../landing/troubleshooting.md) 中。

### 无法查找提供路径的计算属性的架构

```json
{
  "code": "400",
  "message": "Could not lookup schema of the computed attribute for the provided path"
}
```

创建新的计算属性时，如果系统找不到请求有效负载中提供的架构，则会出现此错误。 确保在负载的 `path` 属性，而 `schema.name` 是有效的架构名称。

如果您不知道租户ID，可以按照 [架构注册开发人员指南](../xdm/api/getting-started.md).

### 指定架构或definedOn的函数已存在同名的函数

```json
{
  "code": "400",
  "message": "Function with the same name already exists for the specified schema or definedOn"
}
```

创建新的计算属性时，如果提供 `name` 属性已用于下面指示的架构 `schema.name`. 在重试之前，请使用唯一的名称替换值。

### 表达式的返回架构与XDM架构中计算属性的架构不同

```json
{
  "code": "400",
  "message": "Return schema of the expression is not same as the schema of the computed attribute in the XDM schema"
}
```

创建新的计算属性时，如果提供 `name` 属性已用于下面指示的架构 `schema.name`. 在重试之前，请使用唯一的名称替换值。

### 删除请求无效（配置文件系统作业）

```json
{
  "code": "400",
  "message": "Invalid delete request (Profile System Job)"
}
```

为删除系统作业提供无效有效负载时，会发生此错误。 确保在有效负载的 `dataSetID` 或 `batchID` 属性。 请参阅 [创建删除请求](./api/profile-system-jobs.md#create-a-delete-request) ，以了解更多信息。

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

当尝试为配置文件数据创建删除请求时找不到有效的批处理时，会发生此错误。 再次尝试之前，请检查您是否为启用了“配置文件”的数据集输入了正确的ID。

### 尚未创建投影目标

```json
{
  "status":404,
  "title":"The projection destination has not yet been created.",
  "type":"http://ns.adobe.com/adobecloud/problem/missing-entity"
}
```

当 `destinationId` 在 `POST /config/projections` 请求无效。 再次尝试之前，请仔细检查您是否提供了有效的目标ID。 要创建新目标，请按照 [配置文件开发人员指南](./api/edge-projections.md#create-a-destination).

### 不支持的媒体类型

```json
{
  "status": 415,
  "title": "HTTP 415 Unsupported Media Type",
  "type": "http://ns.adobe.com/adobecloud/problem/unsupported-media-type"
}
```

发送具有无效Content-Type标头的POST或PUT请求时，会发生此错误。 仔细检查您是否正在为您使用的端点提供有效的Content-Type值。

大多数配置文件端点接受其Content-Type标头为“application/json”，但有以下例外：

| 端点 | Content-Type |
| --- | --- |
| `/config/projections` | application/vnd.adobe.platform.projectionConfig+json;version=1 |
| `/config/destinations` | application/vnd.adobe.platform.projectionDestination+json;version=1 |
