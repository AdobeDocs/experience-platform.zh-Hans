---
keywords: Experience Platform;用户档案；实时客户用户档案；疑难解答；API
title: 实时客户用户档案疑难解答指南
topic-legacy: guide
type: Documentation
description: 本文档提供有关实时客户用户档案的常见问题解答，以及使用Adobe Experience Platform处理用户档案数据时常见错误的疑难解答指南。
exl-id: 0b340025-093b-41e4-8053-969a8e80e889
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1003'
ht-degree: 0%

---

# 实时客户用户档案疑难解答指南

此文档提供有关实时用户档案的常见问题解答，以及常见错误的疑难解答指南。 有关与Adobe Experience Platform中其他服务相关的问题和疑难解答，请参阅[Experience Platform疑难解答指南](../landing/troubleshooting.md)。

通过[!DNL Real-time Customer Profile]，您可以通过组合来自多个渠道（包括联机、脱机、CRM和第三方）的数据，了解每个客户的整体视图。 这使营销人员能够跨多个渠道为客户提供协调、一致和相关的体验。

## 常见问题解答

以下是有关实时客户用户档案的常见问题解答列表。

### 实时客户用户档案接受哪类数据？

用户档案接受&#x200B;**record**&#x200B;和&#x200B;**time-series**&#x200B;数据，只要所述数据包含至少一个将数据与唯一个人关联的标识值。

与所有平台服务一样，用户档案要求其数据在体验数据模型(XDM)模式下进行语义结构化。 反过来，此模式必须定义&#x200B;**主标识**，并启用以在用户档案中使用。

如果您不熟悉XDM，请开始[ XDM概述](../xdm/home.md)以了解更多信息。 接下来，请参见XDM用户指南，了解有关如何[设置标识字段](../xdm/tutorials/create-schema-ui.md#identity-field)和[启用用户档案模式](../xdm/tutorials/create-schema-ui.md#profile)的步骤。

### 用户档案数据存储在何处？

实时客户用户档案维护其自己的用户档案存储（称为“客户存储”），与包含其他摄取的平台数据的数据湖相分离。

### 如果我已将数据引入平台，是否可以在用户档案存储中提供它？

如果数据已被引入非用户档案数据集，则必须将该数据重新引入启用用户档案的数据集中，以便在用户档案存储中可用。 可以启用现有用户档案集，但在配置之前摄取的任何数据仍不会显示在用户档案存储中。

如果要向用户档案存储中添加以前摄取的数据，请按照[数据集配置教程](./tutorials/dataset-configuration.md)创建新数据集或转换要启用用户档案的现有数据集，然后将所需数据重新收录到该数据集中。

### 如何视图我摄取的用户档案数据？

查看用户档案数据的方法有多种，具体取决于您使用的是API还是UI。

#### 使用API

如果您知道要访问的用户档案实体的ID，则可以使用用户档案 API中的`/entities`(用户档案访问)端点查找这些实体。 有关详细信息，请参阅开发人员指南中关于[entities](./api/entities.md)的部分。

您还可以使用Adobe Experience Platform Segmentation Service API访问符合细分会员资格的客户的各个用户档案。 有关详细信息，请参阅[分段服务概述](../segmentation/home.md)。

#### 使用UI

在Experience PlatformUI中，使用&#x200B;**[!UICONTROL Profiles]**&#x200B;工作区中的&#x200B;**[!UICONTROL Browse]**&#x200B;选项卡可以视图用户档案总数，并按单个用户档案的标识值搜索其中的数据。 有关详细信息，请参阅[用户档案用户指南](./ui/user-guide.md)。

您还可以在&#x200B;**[!UICONTROL Segments]**&#x200B;工作区的&#x200B;**[!UICONTROL Browse]**&#x200B;选项卡下视图区段的列表。 选择区段后，将显示符合该区段的用户档案示例。 然后，您可以选择其中任何列出的用户档案来视图其详细信息。 有关详细信息，请参阅[分段UI概述](../segmentation/ui/overview.md)。

## 错误代码

以下是您在使用实时客户用户档案API时可能遇到的一列表错误消息。 如果此处未列出您遇到的错误，您可以在常规[平台疑难解答指南](../landing/troubleshooting.md)中找到它。

### 无法查找所提供路径的计算属性的模式

```json
{
  "code": "400",
  "message": "Could not lookup schema of the computed attribute for the provided path"
}
```

创建新计算属性时，当系统找不到在请求有效负荷中提供的模式时，会发生此错误。 请确保在有效负荷的`path`属性中提供了正确的租户ID，并且`schema.name`的值是有效的模式名。

如果您不知道您的租户ID，可以按照[模式注册表开发人员指南](../xdm/api/getting-started.md)中的步骤检索它。

### 对于指定的模式或definedOn，已存在同名的函数

```json
{
  "code": "400",
  "message": "Function with the same name already exists for the specified schema or definedOn"
}
```

创建新计算属性时，当提供的`name`属性已用于`schema.name`下指示的模式时，会发生此错误。 在重试之前，请用唯一名称替换该值。

### 表达式的返回模式与XDM模式中计算属性的模式不同

```json
{
  "code": "400",
  "message": "Return schema of the expression is not same as the schema of the computed attribute in the XDM schema"
}
```

创建新计算属性时，当提供的`name`属性已用于`schema.name`下指示的模式时，会发生此错误。 在重试之前，请用唯一名称替换该值。

### 删除请求无效(用户档案系统作业)

```json
{
  "code": "400",
  "message": "Invalid delete request (Profile System Job)"
}
```

当为删除系统作业提供无效的有效负荷时，会发生此错误。 请确保您分别在有效负荷的`dataSetID`或`batchID`属性下提供有效的数据集或批处理ID。 有关详细信息，请参阅《用户档案开发人员指南》中关于[创建删除请求](./api/profile-system-jobs.md#create-a-delete-request)的部分。

### 找不到用户档案数据集的批

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

当尝试为用户档案数据创建删除请求时找不到有效批时，会发生此错误。 再次尝试之前，请检查您是否为启用用户档案的数据集输入了正确的ID。

### 尚未创建投影目标

```json
{
  "status":404,
  "title":"The projection destination has not yet been created.",
  "type":"http://ns.adobe.com/adobecloud/problem/missing-entity"
}
```

当`POST /config/projections`请求中提供的`destinationId`无效时，会发生此错误。 多次检查您在重试之前是否提供了有效的目标ID。 要创建新目标，请按照[用户档案开发人员指南](./api/edge-projections.md#create-a-destination)中概述的步骤操作。

### 不支持的媒体类型

```json
{
  "status": 415,
  "title": "HTTP 415 Unsupported Media Type",
  "type": "http://ns.adobe.com/adobecloud/problem/unsupported-media-type"
}
```

在发送具有无效Content-Type头的POST或PUT请求时，会发生此错误。 多次检查您是否正在为所使用的端点提供有效的Content-Type值。

大多数用户档案端点接受其Content-Type头的“application/json”，但以下情况除外：

| 端点 | Content-Type |
| --- | --- |
| `/config/projections` | application/vnd.adobe.platform.projectionConfig+json;version=1 |
| `/config/destinations` | application/vnd.adobe.platform.projectionDestination+json;version=1 |
