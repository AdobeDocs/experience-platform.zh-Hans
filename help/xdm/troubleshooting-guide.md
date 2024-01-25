---
keywords: Experience Platform；热门主题；XDM；XDM系统；XDM个人资料；XDM ExperienceEvent；XDM体验事件；experienceEvent；experience eventExperienceEvent；XDM体验事件；XDM ExperienceEvent；体验数据模型；体验数据模型；数据模型；数据模型；架构；故障诊断；FAQ；FAQ；联合架构；UNION资料；联合资料；http://ns.adobe.com/aep/errors/XDM-1010-404;http://ns.adobe.com/aep/errors/XDM-1011-404;http://ns.adobe.com/aep/errors/XDM-1012-404;http://ns.adobe.com/aep/errors/XDM-1013-404;http://ns.adobe.com/aep/errors/XDM-1014-404;http://ns.adobe.com/aep/errors/XDM-1015-404;http://ns.adobe.com/aep/errors/XDM-1016-404;http://ns.adobe.com/aep/errors/XDM-1017-404;http://ns.adobe.com/aep/errors/XDM-1521-400;http://ns.adobe.com/aep/errors/XDM-1020-400;http://ns.adobe.com/aep/errors/XDM-1021-400;http://ns.adobe.com/aep/errors/XDM-1022-400;http://ns.adobe.com/aep/errors/XDM-1023-400;http://ns.adobe.com/aep/errors/XDM-1024-400;http://ns.adobe.com/aep/errors/XDM-1006-400;http://ns.adobe.com/aep/errors/XDM-1007-400;http://ns.adobe.com/aep/errors/XDM-1008-400;http://ns.adobe.com/aep/errors/XDM-1009-400;http://ns.adobe.com/aep/errors/XDM-1526-400;http://ns.adobe.com/aep/errors/XDM-1527-400;http://ns.adobe.com/aep/errors/XDM-1528-400;XDM-1010-404;XDM-1011-404;XDM-1012-404;XDM-1013-404;XDM-1014-404;XDM-1015-404;XDM-1016-404;XDM-1017-404;XDM-1521-400;XDM-1020-400;XDM-1021-400;XDM-1022-400;XDM-1023-400;XDM-1024-400;XDM-1006-400;XDM-1007-400;XDM-1008-400;XDM-1009-400;XDM-1413-400;XDM-1526-400;XDM-1527-400;XDM-1528-400；
solution: Experience Platform
title: XDM系统故障排除指南
description: 查找有关Experience Data Model (XDM)的常见问题解答，包括解决常见API错误的步骤。
exl-id: a0c7c661-bee8-4f66-ad5c-f669c52c9de3
source-git-commit: ba39f62cd77acedb7bfc0081dbb5f59906c9b287
workflow-type: tm+mt
source-wordcount: '1947'
ht-degree: 0%

---

# XDM系统故障排除指南

本文档提供有关以下内容的常见问题解答： [!DNL Experience Data Model] Adobe Experience Platform中的(XDM)和XDM系统，包括常见错误的疑难解答指南。 有关其他Platform服务的问题和疑难解答，请参阅 [Experience Platform疑难解答指南](../landing/troubleshooting.md).

**[!DNL Experience Data Model](XDM)** 是一个开源规范，为客户体验管理定义了标准化的架构。 用于以下项的方法 [!DNL Experience Platform] 已构建， **XDM系统**，可操作 [!DNL Experience Data Model] 供使用的架构 [!DNL Platform] 服务。 此 **[!DNL Schema Registry]** 提供用户界面和RESTful API以访问 **[!DNL Schema Library]** 范围 [!DNL Experience Platform]. 请参阅 [XDM文档](home.md) 以了解更多信息。

## 常见问题解答

以下是有关XDM系统和使用的常见问题解答列表。 [!DNL Schema Registry] API。

### 如何将字段添加到架构？

您可以使用架构字段组向架构添加字段。 每个字段组都与一个或多个类兼容，允许字段组用于实现这些兼容类之一的任何架构中。 虽然Adobe Experience Platform为多个行业字段组提供了自己的预定义字段，但您可以通过使用API或用户界面创建自定义字段组，将自己的字段添加到架构中。

有关在中创建字段组的详细信息 [!DNL Schema Registry] API，请参见 [字段组端点指南](api/field-groups.md#create). 如果您使用的是UI，请参阅 [架构编辑器教程](./tutorials/create-schema-ui.md).

### 与数据类型相比，字段组的最佳用途是什么？

[字段组](./schema/composition.md#field-group) 是定义架构中一个或多个字段的组件。 字段组强制实施其字段在架构层次结构中的显示方式，因此它们包含的每个架构都具有相同的结构。 字段组仅与由其标识的特定类兼容 `meta:intendedToExtend` 属性。

[数据类型](./schema/composition.md#data-type) 还可以为架构提供一个或多个字段。 但是，与字段组不同，数据类型不受特定类的约束。 这使得数据类型成为描述通用数据结构的更灵活的选项，这些结构可以在具有不同类的多个架构中重用。

### 架构的唯一ID是什么？

全部 [!DNL Schema Registry] 资源（架构、字段组、数据类型、类）具有用作唯一ID的URI，以供参考和查找。 在API中查看架构时，可以在顶级找到它 `$id` 和 `meta:altId` 属性。

欲了解更多信息，请参见 [资源识别](api/getting-started.md#resource-identification) 中的部分 [!DNL Schema Registry] API指南。

### 架构何时开始阻止重大更改？

只要从未在创建数据集中使用架构或启用架构以用于中，就可以对架构进行重大更改 [[!DNL Real-Time Customer Profile]](../profile/home.md). 在数据集创建中使用架构或启用架构以便与一起使用后 [!DNL Real-Time Customer Profile]，的规则 [架构演变](schema/composition.md#evolution) 被系统严格执行。

### 长字段类型的最大大小是多少？

长字段类型是一个整数，最大大小为53(+1)位，其潜在范围介于 — 9007199254740992和9007199254740992之间。 这是由于JSON的JavaScript实施表示长整数的方式存在限制。

有关字段类型的更多信息，请参阅文档： [XDM字段类型约束](./schema/field-constraints.md).

### 如何定义架构的身份？

在 [!DNL Experience Platform]，身份用于标识主题（通常是个人），而不管所解释的数据源是什么。 它们通过在架构中将关键字段标记为“标识”来定义。 常用的身份字段包括电子邮件地址、电话号码、 [[!DNL Experience Cloud ID (ECID)]](https://experienceleague.adobe.com/docs/id-service/using/home.html)、 CRM ID和其他唯一ID字段。

可使用API或用户界面将字段标记为标识。

#### 在API中定义身份

在API中，身份是通过创建身份描述符来建立的。 身份描述符发出信号，表明模式的特定属性是唯一标识符。

身份描述符是通过POST对/descriptors端点的请求创建的。 如果成功，您将收到HTTP状态201（已创建）和一个包含新描述符详细信息的响应对象。

有关在API中创建身份描述符的更多详细信息，请参阅上的文档 [描述符](api/descriptors.md) 中的部分 [!DNL Schema Registry] 开发人员指南。

#### 在UI中定义身份

在架构编辑器中打开架构后，选择 **[!UICONTROL 结构]** 您希望标记为标识的编辑器部分。 下 **[!UICONTROL 字段属性]** 在右侧，选择 **[!UICONTROL 标识]** 复选框。

有关在UI中管理身份的详细信息，请参阅 [定义标识字段](./tutorials/create-schema-ui.md#identity-field) 架构编辑器教程中的部分。

### 我的架构是否需要主身份？

主身份是可选的，因为架构可能为零个或一个。 但是，架构必须具有主标识，才能启用架构以便用于 [!DNL Real-Time Customer Profile]. 请参阅 [身份](./tutorials/create-schema-ui.md#identity-field) 架构编辑器教程的部分以了解更多信息。

### 如何启用架构以便在中使用 [!DNL Real-Time Customer Profile]？

已启用架构以便在 [[!DNL Real-Time Customer Profile]](../profile/home.md) 通过在 `meta:immutableTags` 模式的属性。 启用架构以用于 [!DNL Profile] 可使用API或用户界面完成。

#### 为启用现有架构 [!DNL Profile] 使用API

发出PATCH请求以更新架构并添加 `meta:immutableTags` 特性作为包含“union”值的数组。 如果更新成功，响应将显示更新的架构，该架构现在包含合并标记。

有关使用API启用架构以便在中使用的更多信息 [!DNL Real-Time Customer Profile]，请参见 [联合](./api/unions.md) 文档 [!DNL Schema Registry] 开发人员指南。

#### 为启用现有架构 [!DNL Profile] 使用UI

在 [!DNL Experience Platform]，选择 **[!UICONTROL 架构]** 在左侧导航中，从架构列表中选择要启用的架构的名称。 然后，在编辑器的右侧下 **[!UICONTROL 架构属性]**，选择 **[!UICONTROL 个人资料]** 以将其打开。


有关更多信息，请参阅以下部分： [在实时客户档案中使用](./tutorials/create-schema-ui.md#profile) 在 [!UICONTROL 架构编辑器] 教程。

### 能否直接编辑合并架构？

合并模式是只读的，由系统自动生成。 不能直接编辑它们。 在将“union”标记添加到实现特定类的架构时，会为该类创建联合架构。

有关XDM中合并的更多信息，请参见 [联合](./api/unions.md) 中的部分 [!DNL Schema Registry] API指南。

### 如何格式化数据文件以将数据摄取到我的架构中？

[!DNL Experience Platform] 接受以下任一位置的数据文件： [!DNL Parquet] 或JSON格式。 这些文件的内容必须符合数据集引用的架构。 有关数据文件摄取最佳实践的详细信息，请参阅 [批量摄取概述](../ingestion/home.md).

## 错误和故障排除

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

当系统找不到特定资源时，会显示此错误。 资源可能已被删除，或API调用中的路径无效。 在重试之前，请确保已输入API调用的有效路径。 您可能需要检查是否已为资源输入正确的ID，以及路径是否使用相应的容器（全局或租户）进行了正确的命名空间。

>[!NOTE]
>
>根据所检索的资源类型，此错误可能使用以下任一选项 `type` URI：
>
>* `http://ns.adobe.com/aep/errors/XDM-1010-404`
>* `http://ns.adobe.com/aep/errors/XDM-1011-404`
>* `http://ns.adobe.com/aep/errors/XDM-1012-404`
>* `http://ns.adobe.com/aep/errors/XDM-1013-404`
>* `http://ns.adobe.com/aep/errors/XDM-1014-404`
>* `http://ns.adobe.com/aep/errors/XDM-1015-404`
>* `http://ns.adobe.com/aep/errors/XDM-1016-404`
>* `http://ns.adobe.com/aep/errors/XDM-1017-404`

有关在API中构建查找路径的更多信息，请参阅 [容器](./api/getting-started.md#container) 和 [资源识别](api/getting-started.md#resource-identification) 中的部分 [!DNL Schema Registry] 开发人员指南。

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

当您尝试创建标题已被其他资源使用的资源时，会显示此错误消息。 标题在所有资源类型中必须是唯一的。 例如，如果您尝试创建的字段组的标题已被架构使用，您将收到此错误。

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

当您尝试使用不正确的命名空间字段创建资源，或向现有资源添加不正确的命名空间字段时，将显示此错误消息。

由您的组织定义的资源必须在其租户ID下的字段中指定命名空间，以避免与其他行业和供应商资源冲突。 使用标准字段组构建架构时，您在这些字段组的结构中添加的任何自定义字段也必须根据租户ID进行命名空间。

>[!NOTE]
>
>根据命名空间错误的特定性质，此错误可能使用以下任一选项 `type` URI以及不同的消息详细信息：
>
>* `http://ns.adobe.com/aep/errors/XDM-1020-400`
>* `http://ns.adobe.com/aep/errors/XDM-1021-400`
>* `http://ns.adobe.com/aep/errors/XDM-1022-400`
>* `http://ns.adobe.com/aep/errors/XDM-1023-400`
>* `http://ns.adobe.com/aep/errors/XDM-1024-400`

有关XDM资源的正确数据结构的详细示例，请参阅架构注册表API指南：

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

中的GET请求 [!DNL Schema Registry] API需要 `Accept` 标头，以便系统确定如何设置响应的格式。 当需要时，会发生此错误 `Accept` 标头无效或缺失。

根据您使用的端点， `detailed-message` 属性指明有效的 `Accept` 标头应看起来像是一个成功的响应。 确保您已正确输入 `Accept` 在重试之前，尝试发出的API请求兼容的标头。

>[!NOTE]
>
>根据所使用的端点，此错误可能使用以下任一项 `type` URI：
>
>* `http://ns.adobe.com/aep/errors/XDM-1006-400`
>* `http://ns.adobe.com/aep/errors/XDM-1007-400`
>* `http://ns.adobe.com/aep/errors/XDM-1008-400`
>* `http://ns.adobe.com/aep/errors/XDM-1009-400`

有关不同API请求的兼容“接受”标头的列表，请参阅 [架构注册开发人员指南](./api/overview.md).

### [!DNL Real-Time Customer Profile] 错误

以下错误消息与启用架构所涉及的操作相关联 [!DNL Real-Time Customer Profile]. 请参阅 [联合](./api/unions.md) 中的部分 [!DNL Schema Registry] API指南，以了解更多信息。

#### 必须存在引用身份描述符

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

当您尝试为以下对象启用架构时，将显示此错误消息： [!DNL Profile] 并且其中一个属性包含没有引用身份描述符的关系描述符。 将引用身份描述符添加到有问题的架构字段以解决此错误。

#### 引用身份描述符字段的命名空间与目标架构必须匹配

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

>[!NOTE]
>
>对于此错误，“目标架构”引用关系中的引用架构。

为了启用包含关系描述符的架构以便用于 [!DNL Profile]，源字段的命名空间和引用字段的主命名空间必须相同。 当您尝试启用一个方案（该方案的引用标识描述符包含不匹配的命名空间）时，将显示此错误消息。

确保 `xdm:namespace` 引用架构的标识字段的值与 `xdm:identityNamespace` 源字段的引用身份描述符中的属性以解决此问题。

有关标准身份命名空间代码的列表，请参阅 [标准命名空间](../identity-service/features/namespaces.md) 在身份命名空间概述中。

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

在为配置文件启用架构之前，必须首先 [创建主身份描述符](./api/descriptors.md#create) 用于模式，或包含身份映射字段以替代主身份。

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

属于同一类的所有启用了配置文件的架构必须能够合并在一起，才能构造该类的合并架构。 当您尝试将字段添加到架构时，如果该架构的路径由另一个启用配置文件的架构共享，并且数据类型与原始架构不同，则会显示此错误。 由于架构已启用配置文件并且包含相同的字段路径，因此配置文件在构建合并架构时会尝试将这两个字段合并为一个。 由于不同数据类型无法合并在一起，因此这将被视为合并冲突，因此是不允许的。

要解决此问题，请为该字段选择不同的名称，或将其嵌套在唯一的命名空间对象下，以避免与具有相似字段的同一类下的其他启用配置文件的架构发生合并冲突。
