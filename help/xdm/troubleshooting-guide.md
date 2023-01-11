---
keywords: Experience Platform；热门主题；XDM;XDM系统；XDM个人配置文件；XDM ExperienceEvent;XDM体验事件；体验事件；体验事件；XDM体验事件；体验数据模型；体验数据模型；体验数据模型；数据模型；数据模型；模式；故障诊断；FAQ;FAQ；联盟配置文件；联合配置文件；http://ns.adobe.com/aep/errors/XDM-1010-404;http://ns.adobe.com/aep/errors/XDM-1011-404;http://ns.adobe.com/aep/errors/XDM-1012-404;http://ns.adobe.com/aep/errors/XDM-1013-404;http://ns.adobe.com/aep/errors/XDM-1014-404;http://ns.adobe.com/aep/errors/XDM-1015-404;http://ns.adobe.com/aep/errors/XDM-1016-404;http://ns.adobe.com/aep/errors/XDM-1017-404;http://ns.adobe.com/aep/errors/XDM-1521-400;http://ns.adobe.com/aep/errors/XDM-1020-400;http://ns.adobe.com/aep/errors/XDM-1021-400;http://ns.adobe.com/aep/errors/XDM-1022-400;http://ns.adobe.com/aep/errors/XDM-1023-400;http://ns.adobe.com/aep/errors/XDM-1024-400;http://ns.adobe.com/aep/errors/XDM-1006-400;http://ns.adobe.com/aep/errors/XDM-1007-400;http://ns.adobe.com/aep/errors/XDM-1008-400;http://ns.adobe.com/aep/errors/XDM-1009-400;http://ns.adobe.com/aep/errors/XDM-1526-400;http://ns.adobe.com/aep/errors/XDM-1527-400;http://ns.adobe.com/aep/errors/XDM-1528-400;XDM-1010-404;XDM-1011-404;XDM-1012-404;XDM-1013-404;XDM-1014-404;XDM-1015-404;XDM-1016-404;XDM-1017-404;XDM-1521-400;XDM-1020-400;XDM-1021-400;XDM-1022-400;XDM-1023-400;XDM-1024-400;XDM-1006-400;XDM-1007-400;XDM-1008-400;XDM-1009-400;XDM-1413-400;XDM-1526-400;XDM-1527-400;XDM-1528-400;
solution: Experience Platform
title: XDM系统疑难解答指南
description: 查找有关Experience Data Model(XDM)的常见问题解答，包括解决常见API错误的步骤。
exl-id: a0c7c661-bee8-4f66-ad5c-f669c52c9de3
source-git-commit: 983682489e2c0e70069dbf495ab90fc9555aae2d
workflow-type: tm+mt
source-wordcount: '2060'
ht-degree: 0%

---

# XDM系统疑难解答指南

本文档提供了有关 [!DNL Experience Data Model] (XDM)和Adobe Experience Platform中的XDM系统，包括常见错误的疑难解答指南。 有关其他平台服务的相关问题和疑难解答，请参阅 [Experience Platform疑难解答指南](../landing/troubleshooting.md).

**[!DNL Experience Data Model](XDM)** 是一种开源规范，用于定义客户体验管理的标准化架构。 方法 [!DNL Experience Platform] 是建的， **XDM系统**，操作 [!DNL Experience Data Model] 供使用的架构 [!DNL Platform] 服务。 的 **[!DNL Schema Registry]** 提供用户界面和RESTful API来访问 **[!DNL Schema Library]** within [!DNL Experience Platform]. 请参阅 [XDM文档](home.md) 以了解更多信息。

## 常见问题解答

以下是有关XDM系统和使用的常见问题解答列表 [!DNL Schema Registry] API。

### 如何向架构添加字段？

您可以使用架构字段组向架构添加字段。 每个字段组都与一个或多个类兼容，从而允许在实现这些兼容类之一的任何架构中使用字段组。 虽然Adobe Experience Platform为多个行业字段组提供了其自己的预定义字段，但您可以通过使用API或用户界面创建自定义字段组，将自己的字段添加到架构中。

有关在 [!DNL Schema Registry] API，请参阅 [字段组终结点指南](api/field-groups.md#create). 如果您使用的是UI，请参阅 [模式编辑器教程](./tutorials/create-schema-ui.md).

### 字段组与数据类型的最佳用法是什么？

[字段组](./schema/composition.md#field-group) 是在架构中定义一个或多个字段的组件。 字段组强制执行其字段在架构层次结构中的显示方式，因此在每个架构中显示的结构都与其中包含的结构相同。 字段组仅与特定类兼容，这些类由其标识 `meta:intendedToExtend` 属性。

[数据类型](./schema/composition.md#data-type) 还可以为架构提供一个或多个字段。 但是，与字段组不同，数据类型不受特定类的限制。 这使数据类型成为一种更灵活的选项，用于描述在具有潜在不同类的多个架构中可重复使用的常用数据结构。

### 架构的唯一ID是什么？

全部 [!DNL Schema Registry] 资源（架构、字段组、数据类型、类）具有一个URI，该URI充当用于引用和查找的唯一ID。 在API中查看架构时，可在顶级中找到该架构 `$id` 和 `meta:altId` 属性。

有关更多信息，请参阅 [资源标识](api/getting-started.md#resource-identification) 部分 [!DNL Schema Registry] API指南。

### 架构何时开始阻止中断更改？

只要架构从未在创建数据集时使用过或启用以供在中使用，就可以对其进行重大更改 [[!DNL Real-Time Customer Profile]](../profile/home.md). 在数据集创建中使用架构或启用架构以与结合使用后 [!DNL Real-Time Customer Profile]，规则 [模式演变](schema/composition.md#evolution) 被制度严格执行。

### 长字段类型的最大大小是多少？

长字段类型是一个最大大小为53(+1)位的整数，它赋予它一个介于 — 9007199254740992和9007199254740992之间的潜在范围。 这是由于JSON的JavaScript实施如何表示长整数存在限制。

有关字段类型的详细信息，请参阅 [XDM字段类型约束](./schema/field-constraints.md).

### 如何为架构定义标识？

在 [!DNL Experience Platform]，则无论解释的数据源如何，均会使用身份来标识主题（通常是个人）。 在架构中，可通过将键字段标记为“标识”来定义这些字段。 标识的常用字段包括电子邮件地址、电话号码、 [[!DNL Experience Cloud ID (ECID)]](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=zh-Hans)、CRM ID和其他唯一ID字段。

字段可以使用API或用户界面标记为标识。

#### 在API中定义标识

在API中，通过创建身份描述符来建立身份。 标识描述符表示模式的特定属性是唯一标识符。

身份描述符由对/descriptors端点的POST请求创建。 如果成功，您将收到HTTP状态201（已创建）和包含新描述符详细信息的响应对象。

有关在API中创建身份描述符的更多详细信息，请参阅 [描述符](api/descriptors.md) 部分 [!DNL Schema Registry] 开发人员指南。

#### 在UI中定义标识

在架构编辑器中打开架构，选择 **[!UICONTROL 结构]** 作为标识的编辑器部分。 在 **[!UICONTROL 字段属性]** 在右侧，选择 **[!UICONTROL 身份]** 复选框。

有关在UI中管理身份的更多详细信息，请参阅 [定义标识字段](./tutorials/create-schema-ui.md#identity-field) 章节。

### 我的架构是否需要主标识？

主标识是可选的，因为架构可能具有零个或其中一个标识。 但是，架构必须具有主标识，才能在中启用该架构 [!DNL Real-Time Customer Profile]. 请参阅 [身份](./tutorials/create-schema-ui.md#identity-field) 章节，以了解更多信息。

### 如何启用在中使用的架构 [!DNL Real-Time Customer Profile]?

已启用架构以用于 [[!DNL Real-Time Customer Profile]](../profile/home.md) 通过在 `meta:immutableTags` 架构的属性。 启用模式以便与 [!DNL Profile] 可以使用API或用户界面完成。

#### 为启用现有模式 [!DNL Profile] 使用API

发出PATCH请求以更新架构并添加 `meta:immutableTags` 属性作为包含值“union”的数组。 如果更新成功，则响应将显示更新的架构，该架构现在包含并集标记。

有关使用API启用架构以在中使用的更多信息 [!DNL Real-Time Customer Profile]，请参阅 [工会](./api/unions.md) 文档 [!DNL Schema Registry] 开发人员指南。

#### 为启用现有模式 [!DNL Profile] 使用UI

在 [!DNL Experience Platform]，选择 **[!UICONTROL 模式]** 在左侧导航中，从架构列表中选择要启用的架构的名称。 然后，在编辑器右侧的 **[!UICONTROL 架构属性]**，选择 **[!UICONTROL 用户档案]** 以将其打开。


有关更多信息，请参阅 [在实时客户用户档案中使用](./tutorials/create-schema-ui.md#profile) 在 [!UICONTROL 架构编辑器] 教程。

### 能否直接编辑并集架构？

并集架构是只读的，并由系统自动生成。 无法直接编辑它们。 将“并集”标记添加到实现该类的架构时，会为特定类创建并集架构。

有关XDM中工会的更多信息，请参阅 [工会](./api/unions.md) 部分 [!DNL Schema Registry] API指南。

### 如何设置数据文件格式，以将数据摄取到我的架构中？

[!DNL Experience Platform] 在任一位置接受数据文件 [!DNL Parquet] 或JSON格式。 这些文件的内容必须符合数据集引用的架构。 有关数据文件摄取最佳实践的详细信息，请参阅 [批量摄取概述](../ingestion/home.md).

## 错误和疑难解答

以下是使用时可能遇到的错误消息列表 [!DNL Schema Registry] API。

### 未找到资源

```json
{
    "type": "http://ns.adobe.com/aep/errors/XDM-1010-404",
    "title": "Resource not found",
    "status": 404,
    "report": {
        "registryRequestId": "a15996b5-5133-4cec-9bf7-7d1207904ae3",
        "timestamp": "06-01-2021 04:11:06",
        "detailed-message": "The requested class resource https://ns.adobe.com/{TENANT_ID}/classes/11447bb484d4599d2cd9b0aseefff78b463cbbde1527f498 with version 1 is not found.",
        "sub-errors": []
    },
    "detail": "The requested class resource https://ns.adobe.com/{TENANT_ID}/classes/11447bb484d4599d2cd9b0aseefff78b463cbbde1527f498 with version 1 is not found."
}
```

当系统找不到特定资源时，将显示此错误。 资源可能已删除，或API调用中的路径无效。 再次尝试之前，请确保您为API调用输入了有效路径。 您可能需要检查是否已为资源输入正确的ID，以及路径是否与相应的容器（全局或租户）正确命名。

>[!NOTE]
>
>根据检索的资源类型，此错误可能使用以下任一内容 `type` URI:
>
>* `http://ns.adobe.com/aep/errors/XDM-1010-404`
>* `http://ns.adobe.com/aep/errors/XDM-1011-404`
>* `http://ns.adobe.com/aep/errors/XDM-1012-404`
>* `http://ns.adobe.com/aep/errors/XDM-1013-404`
>* `http://ns.adobe.com/aep/errors/XDM-1014-404`
>* `http://ns.adobe.com/aep/errors/XDM-1015-404`
>* `http://ns.adobe.com/aep/errors/XDM-1016-404`
>* `http://ns.adobe.com/aep/errors/XDM-1017-404`


有关在API中构建查找路径的更多信息，请参阅 [容器](./api/getting-started.md#container) 和 [资源标识](api/getting-started.md#resource-identification) 部分 [!DNL Schema Registry] 开发人员指南。

### 标题不唯一

```json
{
    "type": "http://ns.adobe.com/aep/errors/XDM-1521-400",
    "title": "Title not unique",
    "status": 400,
    "report": {
        "registryRequestId": "a15996b5-5133-4cec-9bf7-7d1207904ae3",
        "timestamp": "06-01-2021 04:11:06",
        "detailed-message": "Object titles must be unique. An object https://ns.adobe.com/{TENANT_ID}/classes/11447bb484d4599d2cd9b0aseefff78b463cbbde1527f498 already exists with the same title",
        "sub-errors": []
    },
    "detail": "Object titles must be unique. An object https://ns.adobe.com/{TENANT_ID}/classes/11447bb484d4599d2cd9b0aseefff78b463cbbde1527f498 already exists with the same title"
}
```

当您尝试创建标题已被其他资源使用的资源时，会显示此错误消息。 标题在所有资源类型中必须是唯一的。 例如，如果您尝试创建的字段组的标题已经由架构使用，则会收到此错误。

### 命名空间验证错误

```json
{
    "type": "http://ns.adobe.com/aep/errors/XDM-1021-400",
    "title": "Namespace validation error",
    "status": 400,
    "report": {
        "registryRequestId": "a15996b5-5133-4cec-9bf7-7d1207904ae3",
        "timestamp": "06-01-2021 04:11:06",
        "detailed-message": "A custom field is defined under an invalid namespace. All custom fields must be defined under a top-level field named {TENANT_ID}.",
        "sub-errors": []
    },
    "detail": "A custom field is defined under an invalid namespace. All custom fields must be defined under a top-level field named {TENANT_ID}."
}
```

当您尝试创建名称不正确的字段的资源，或向现有资源添加名称不正确的字段时，会显示此错误消息。

由IMS组织定义的资源必须在租户ID下命名其字段的命名空间，以避免与其他行业和供应商资源发生冲突。 在使用标准字段组构建架构时，您在这些字段组结构中添加的任何自定义字段也必须与租户ID下的名称同步。

>[!NOTE]
>
>根据命名空间错误的特定性质，此错误可能使用以下任一内容 `type` URI以及不同的消息详细信息：
>
>* `http://ns.adobe.com/aep/errors/XDM-1020-400`
>* `http://ns.adobe.com/aep/errors/XDM-1021-400`
>* `http://ns.adobe.com/aep/errors/XDM-1022-400`
>* `http://ns.adobe.com/aep/errors/XDM-1023-400`
>* `http://ns.adobe.com/aep/errors/XDM-1024-400`


有关XDM资源正确数据结构的详细示例，请参阅架构注册API指南：

* [创建自定义类](./api/classes.md#create)
* [创建自定义字段组](./api/field-groups.md#create)
* [创建自定义数据类型](./api/data-types.md#create)

### 接受标头无效

```json
{
    "type": "http://ns.adobe.com/aep/errors/XDM-1006-400",
    "title": "Accept header invalid",
    "status": 400,
    "report": {
        "registryRequestId": "a15996b5-5133-4cec-9bf7-7d1207904ae3",
        "timestamp": "06-01-2021 04:11:06",
        "detailed-message": "The supplied Accept header is not valid: application/vnd.adobe.xed+json;version=1 - A valid Accept value should look like application/vnd.adobe.{xed|xdm}+json",
        "sub-errors": []
    },
    "detail": "The supplied Accept header is not valid: application/vnd.adobe.xed+json;version=1 - A valid Accept value should look like application/vnd.adobe.{xed|xdm}+json"
}
```

GET请求 [!DNL Schema Registry] API需要 `Accept` 标头，以便系统确定如何设置响应的格式。 当需要 `Accept` 标头无效或缺失。

根据您使用的端点， `detailed-message` 属性指示有效值 `Accept` 标头应类似于成功响应的样子。 确保已正确输入 `Accept` 与您尝试在重试之前发出的API请求兼容的标头。

>[!NOTE]
>
>根据所使用的端点，此错误可能会使用以下任一内容 `type` URI:
>
>* `http://ns.adobe.com/aep/errors/XDM-1006-400`
>* `http://ns.adobe.com/aep/errors/XDM-1007-400`
>* `http://ns.adobe.com/aep/errors/XDM-1008-400`
>* `http://ns.adobe.com/aep/errors/XDM-1009-400`


有关不同API请求的兼容Accept标头列表，请参阅 [架构注册开发人员指南](./api/overview.md).

### [!DNL Real-Time Customer Profile] 错误

以下错误消息与启用架构中涉及的操作相关联 [!DNL Real-Time Customer Profile]. 请参阅 [工会](./api/unions.md) 部分 [!DNL Schema Registry] API指南以了解更多信息。

#### 必须有引用标识描述符

```json
{
    "type": "http://ns.adobe.com/aep/errors/XDM-1526-400",
    "title": "Union descriptor validation error",
    "status": 400,
    "report": {
        "registryRequestId": "a15996b5-5133-4cec-9bf7-7d1207904ae3",
        "timestamp": "06-01-2021 04:11:06",
        "detailed-message": "If a schema contains properties that are associated with an xdm:descriptorOneToOne descriptor, those properties must also have a xdm:descriptorReferenceIdentity descriptor for that schema to participate in a union.",
        "sub-errors": []
    },
    "detail": "If a schema contains properties that are associated with an xdm:descriptorOneToOne descriptor, those properties must also have a xdm:descriptorReferenceIdentity descriptor for that schema to participate in a union."
}
```

当您尝试为 [!DNL Profile] 并且其一个属性包含没有引用标识描述符的关系描述符。 将引用标识描述符添加到相关架构字段以解决此错误。

#### 引用标识描述符字段和目标架构的命名空间必须匹配

```json
{
    "type": "http://ns.adobe.com/aep/errors/XDM-1527-400",
    "title": "Union descriptor validation error",
    "status": 400,
    "report": {
        "registryRequestId": "a15996b5-5133-4cec-9bf7-7d1207904ae3",
        "timestamp": "06-01-2021 04:11:06",
        "detailed-message": "If both schemas from an existing xdm:descriptorOneToOne descriptor are promoted to union, and one of those schemas contains a primary identity, the xdm:identityNamespace of the source schema's descriptorReferenceIdentity field must match the xdm:namespace field of destination schema's xdm:descriptorIdentity field.",
        "sub-errors": []
    },
    "detail": "If both schemas from an existing xdm:descriptorOneToOne descriptor are promoted to union, and one of those schemas contains a primary identity, the xdm:identityNamespace of the source schema's descriptorReferenceIdentity field must match the xdm:namespace field of destination schema's xdm:descriptorIdentity field."
}
```

为了启用包含关系描述符的架构以便在中使用 [!DNL Profile]，源字段的命名空间和目标字段的主命名空间必须相同。 当您尝试启用某个架构，该架构的引用标识描述符包含不匹配的命名空间时，将显示此错误消息。 确保 `xdm:namespace` 目标架构的identity字段的值与 `xdm:identityNamespace` 用于解决此问题的源字段引用标识描述符中的属性。

有关标准身份命名空间代码的列表，请参阅 [标准命名空间](../identity-service/namespaces.md) 在身份命名空间概述中。

#### 架构必须包含identityMap或主标识

```json
{
    "type": "http://ns.adobe.com/aep/errors/XDM-1528-400",
    "title": "Union descriptor validation error",
    "status": 400,
    "report": {
        "registryRequestId": "a15996b5-5133-4cec-9bf7-7d1207904ae3",
        "timestamp": "06-01-2021 04:11:06",
        "detailed-message": "To participate in a union, a schema must include an identityMap fieldgroup or a primary identity descriptor.",
        "sub-errors": []
    },
    "detail": "To participate in a union, a schema must include an identityMap fieldgroup or a primary identity descriptor."
}
```

在为用户档案启用架构之前，必须先 [创建主标识描述符](./api/descriptors.md#create) ，或者包括一个标识映射字段，以改为以主标识操作。

#### 无法合并不兼容的数据类型

```json
{
    "type": "http://ns.adobe.com/aep/errors/XDM-1413-400",
    "title": "Merge Schema Error",
    "status": 400,
    "report": {
        "registryRequestId": "a15996b5-5133-4cec-9bf7-7d1207904ae3",
        "timestamp": "06-01-2021 04:11:06",
        "detailed-message": "Cannot merge incompatible data types. The path /person/name has already been defined in schema (id=0238be93d3e7a06aec5e0655955901ec) using a different data type. Types: string, object",
        "sub-errors": []
    },
    "detail": "Cannot merge incompatible data types. The path /person/name has already been defined in schema (id=0238be93d3e7a06aec5e0655955901ec) using a different data type. Types: string, object"
}
```

属于同一类的所有启用了用户档案的架构必须能够合并在一起，才能为该类构建并集架构。 当您尝试向某个架构添加一个字段，而该架构的路径由另一个启用了用户档案的架构共享，且数据类型与原始架构不同时，会显示此错误。 由于架构均启用了用户档案并包含相同的字段路径，因此在构建并集架构时，用户档案会尝试将这两个字段合并为一个字段。 由于不同数据类型不能合并在一起，因此这会被视为合并冲突，不允许。

要解决此问题，请为字段选择其他名称或将其嵌套在唯一名称进度对象下，以避免与具有相似字段的同一类下其他启用配置文件的架构合并冲突。
