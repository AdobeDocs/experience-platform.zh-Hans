---
keywords: Experience Platform;用户档案；实时客户用户档案；疑难解答；API
title: 实时客户用户档案疑难解答指南
topic: guide
type: Documentation
description: 此文档提供有关实时客户用户档案的常见问题解答，以及使用Adobe Experience Platform处理用户档案数据时常见错误的疑难解答指南。
translation-type: tm+mt
source-git-commit: e6ecc5dac1d09c7906aa7c7e01139aa194ed662b
workflow-type: tm+mt
source-wordcount: '1007'
ht-degree: 0%

---


# 实时客户用户档案疑难解答指南

此文档提供有关实时客户用户档案的常见问题解答以及常见错误的疑难解答指南。 有关与Adobe Experience Platform其他服务相关的问题和疑难解答，请参阅[Experience Platform疑难解答指南](../landing/troubleshooting.md)。

通过[!DNL Real-time Customer Profile]，您可以通过组合来自多个视图（包括联机、脱机、CRM和第三方）的数据，了解每位客户的整体渠道。 这使营销人员能够跨多个渠道为客户提供协调、一致和相关的体验。

## 常见问题解答

以下是有关实时客户用户档案的常见问题的列表解答。

### 实时客户用户档案接受哪些类型的数据？

用户档案接受&#x200B;**记录**&#x200B;和&#x200B;**时间序列**&#x200B;数据，只要所述数据包含至少一个将数据与唯一个人相关联的标识值。

与所有平台服务一样，用户档案要求其数据在体验数据模型(XDM)模式下进行语义结构化。 反过来，此模式必须定义&#x200B;**主标识**，并启用该标识以在用户档案中使用。

如果您不熟悉XDM，请开始[ XDM概述](../xdm/home.md)以了解更多。 接下来，请参见XDM用户指南，了解有关如何[设置标识字段](../xdm/tutorials/create-schema-ui.md#identity-field)和[启用用户档案模式的步骤](../xdm/tutorials/create-schema-ui.md#profile)。

### 用户档案数据存储在何处？

实时客户用户档案维护其自己的数据存储(称为“用户档案存储”)，与包含其他摄取的平台数据的数据湖相分离。

### 如果我已将数据引入平台，是否可以在用户档案商店中提供它？

如果数据已被收录到非用户档案数据集中，则必须将该数据重新收录到启用用户档案的数据集中，以便在用户档案存储中提供。 可以启用现有数据集进行用户档案，但在配置之前摄取的任何数据仍不会显示在用户档案存储中。

如果要向用户档案商店添加以前摄取的数据，请按照[数据集配置教程](./tutorials/dataset-configuration.md)创建新数据集或转换要启用用户档案的现有数据集，然后将所需数据重新收录到该数据集中。

### 如何视图我的摄取的用户档案数据？

查看用户档案数据的方法有多种，具体取决于您使用的是API还是UI。

#### 使用API

如果您知道要访问的用户档案实体的ID，则可以使用用户档案API中的`/entities`(用户档案访问)端点查找这些实体。 有关详细信息，请参见开发人员指南中的[entities](./api/entities.md)一节。

您还可以使用Adobe Experience Platform细分服务API访问符合细分会员资格的单个用户档案客户。 有关详细信息，请参阅[分段服务概述](../segmentation/home.md)。

#### 使用UI

在Experience PlatformUI中，使用&#x200B;**[!UICONTROL 用户档案]**&#x200B;工作区中的&#x200B;**[!UICONTROL 浏览]**&#x200B;选项卡，可以视图用户档案总数，并按其标识值搜索各个用户档案。 有关详细信息，请参阅[用户档案用户指南](./ui/user-guide.md)。

您还可以在&#x200B;**[!UICONTROL 区段]**&#x200B;工作区的&#x200B;**[!UICONTROL 浏览]**&#x200B;选项卡下视图区段的列表。 选择区段后，将显示符合该区段条件的用户档案示例。 然后，您可以选择其中任何列出的用户档案来视图其详细信息。 有关详细信息，请参阅[分段UI概述](../segmentation/ui/overview.md)。

## 错误代码

以下是您在使用实时客户用户档案API时可能遇到的一列表错误消息。 如果此处未列出您遇到的错误，您可以在常规的[平台故障排除指南](../landing/troubleshooting.md)中找到该错误。

### 无法查找所提供路径的计算属性的模式

```json
{
  "code": "400",
  "message": "Could not lookup schema of the computed attribute for the provided path"
}
```

创建新计算属性时，当系统找不到请求有效负荷中提供的模式时，会发生此错误。 请确保在有效负荷的`path`属性中提供了正确的租户ID，并且`schema.name`的值是有效的模式名。

如果您不知道您的租户ID，可以按照[模式注册表开发人员指南](../xdm/api/getting-started.md)中的步骤检索它。

### 指定模式或definedOn已存在同名函数

```json
{
  "code": "400",
  "message": "Function with the same name already exists for the specified schema or definedOn"
}
```

创建新计算属性时，当提供的`name`属性已用于`schema.name`下指示的模式时，会发生此错误。 请用唯一名称替换该值，然后再次尝试。

### 表达式的返回模式与XDM模式中计算属性的模式不同

```json
{
  "code": "400",
  "message": "Return schema of the expression is not same as the schema of the computed attribute in the XDM schema"
}
```

创建新计算属性时，当提供的`name`属性已用于`schema.name`下指示的模式时，会发生此错误。 请用唯一名称替换该值，然后再次尝试。

### 删除请求无效(用户档案系统作业)

```json
{
  "code": "400",
  "message": "Invalid delete request (Profile System Job)"
}
```

为删除系统作业提供无效有效负荷时，会发生此错误。 请确保分别在有效负荷的`dataSetID`或`batchID`属性下提供有效数据集或批ID。 有关详细信息，请参阅用户档案开发人员指南中有关创建删除请求的部分。[](./api/profile-system-jobs.md#create-a-delete-request)

### 找不到用户档案数据集的批处理

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

当尝试创建用户档案数据的删除请求时找不到有效批时，会发生此错误。 再次尝试之前，请检查您是否为启用用户档案的数据集输入了正确的ID。

### 尚未创建投影目标

```json
{
  "status":404,
  "title":"The projection destination has not yet been created.",
  "type":"http://ns.adobe.com/adobecloud/problem/missing-entity"
}
```

当`POST /config/projections`请求中提供的`destinationId`无效时，会发生此错误。 多次检查您是否已提供有效的目标ID，然后再次尝试。 要创建新目标，请按照[用户档案开发人员指南](./api/edge-projections.md#create-a-destination)中概述的步骤操作。

### 不支持的媒体类型

```json
{
  "status": 415,
  "title": "HTTP 415 Unsupported Media Type",
  "type": "http://ns.adobe.com/adobecloud/problem/unsupported-media-type"
}
```

在发送具有无效Content-Type头的POST或PUT请求时，会发生此错误。 多次-检查您是否正在为您所使用的端点提供有效的Content-Type值。

大多数用户档案端点接受其Content-Type头的“application/json”，但以下情况除外：

| 端点 | 内容类型 |
| --- | --- |
| `/config/projections` | application/vnd.adobe.platform.projectionConfig+json;version=1 |
| `/config/destinations` | application/vnd.adobe.platform.projectionDestination+json;version=1 |