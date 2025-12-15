---
keywords: Experience Platform；热门主题；XDM；XDM系统；XDM个人资料；XDM ExperienceEvent；XDM体验事件；experienceEvent；experienceEvent；XDM体验事件；XDM ExperienceEvent；体验数据模型；体验数据模型；数据模型；数据模型；架构；疑难解答；FAQ；Union架构；UNION资料；union资料；http://ns.adobe.com/aep/errors/XDM-1010-404;http://ns.adobe.com/aep/errors/XDM-1011-404;http://ns.adobe.com/aep/errors/XDM-1012-404;http://ns.adobe.com/aep/errors/XDM-1013-404;http://ns.adobe.com/aep/errors/XDM-1014-404;http://ns.adobe.com/aep/errors/XDM-1015-404;http://ns.adobe.com/aep/errors/XDM-1016-404;http://ns.adobe.com/aep/errors/XDM-1017-404;http://ns.adobe.com/aep/errors/XDM-1521-400;http://ns.adobe.com/aep/errors/XDM-1020-400;http://ns.adobe.com/aep/errors/XDM-1021-400;http://ns.adobe.com/aep/errors/XDM-1022-400;http://ns.adobe.com/aep/errors/XDM-1023-400;http://ns.adobe.com/aep/errors/XDM-1024-400;http://ns.adobe.com/aep/errors/XDM-1006-400;http://ns.adobe.com/aep/errors/XDM-1007-400;http://ns.adobe.com/aep/errors/XDM-1008-400;http://ns.adobe.com/aep/errors/XDM-1009-400;http://ns.adobe.com/aep/errors/XDM-1526-400;http://ns.adobe.com/aep/errors/XDM-1527-400;http://ns.adobe.com/aep/errors/XDM-1528-400;XDM-1010-404;XDM-1011-404;XDM-1012-404;XDM-1013-404;XDM-1014-404;XDM-1015-404;XDM-1016-404;XDM-1017-404;XDM-1521-400;XDM-1020-400;XDM-1021-400;XDM-1022-400;XDM-1023-400;XDM-1024-400;XDM-1006-400;XDM-1007-400;XDM-1008-400;XDM-1009-400;XDM-1413-400;XDM-1526-400;XDM-1527-400;XDM-1528-400；
solution: Experience Platform
title: XDM系统故障排除指南
description: 查找有关Experience Data Model (XDM)的常见问题解答，包括解决常见API错误的步骤。
exl-id: a0c7c661-bee8-4f66-ad5c-f669c52c9de3
source-git-commit: 8ba80a1cc4529f9d4693e3f7cbd7584193915410
workflow-type: tm+mt
source-wordcount: '2368'
ht-degree: 0%

---

# XDM系统故障排除指南

本文档提供有关Adobe Experience Platform中[!DNL Experience Data Model] (XDM)和XDM系统的常见问题解答，包括常见错误的疑难解答指南。 有关其他Experience Platform服务的问题和疑难解答，请参阅[Experience Platform疑难解答指南](../landing/troubleshooting.md)。

**[!DNL Experience Data Model] (XDM)**&#x200B;是一个开源规范，它定义了用于客户体验管理的标准化架构。 生成[!DNL Experience Platform]的方法&#x200B;**XDM系统**&#x200B;可使[!DNL Experience Data Model]架构可操作以供[!DNL Experience Platform]服务使用。 **[!DNL Schema Registry]**&#x200B;提供用户界面和RESTful API以访问&#x200B;**[!DNL Schema Library]**&#x200B;中的[!DNL Experience Platform]。 有关详细信息，请参阅[XDM文档](home.md)。

## 常见问题

以下是有关XDM系统和[!DNL Schema Registry] API用法的常见问题解答列表。

## 架构基础知识

在此部分中，您可以找到有关XDM系统中的架构结构、字段使用和标识的基本问题的答案。

### 如何将字段添加到架构？

您可以使用架构字段组向架构添加字段。 每个字段组都与一个或多个类兼容，允许字段组用于实现这些兼容类之一的任何架构中。 虽然Adobe Experience Platform为多个行业字段组提供了自己的预定义字段，但您可以通过使用API或用户界面创建自定义字段组，将自己的字段添加到架构中。

有关在[!DNL Schema Registry] API中创建字段组的详细信息，请参阅[字段组终结点指南](api/field-groups.md#create)。 如果您使用的是用户界面，请参阅[架构编辑器教程](./tutorials/create-schema-ui.md)。

### 与数据类型相比，字段组的最佳用途是什么？

[字段组](./schema/composition.md#field-group)是定义架构中一个或多个字段的组件。 字段组强制实施其字段在架构层次结构中的显示方式，因此它们包含的每个架构都具有相同的结构。 字段组仅与由其`meta:intendedToExtend`属性标识的特定类兼容。

[数据类型](./schema/composition.md#data-type)还可以为架构提供一个或多个字段。 但是，与字段组不同，数据类型不受特定类的约束。 这使得数据类型成为描述通用数据结构的更灵活的选项，这些结构可以在具有不同类的多个架构中重用。

### 架构的唯一ID是什么？

所有[!DNL Schema Registry]资源（架构、字段组、数据类型、类）都有一个URI，该URI用作唯一ID以供参考和查找。 在API中查看架构时，可在顶级`$id`和`meta:altId`属性中找到该架构。

有关详细信息，请参阅[&#x200B; API指南中的](api/getting-started.md#resource-identification)资源标识[!DNL Schema Registry]部分。

### 长字段类型的最大大小是多少？

长字段类型是一个整数，最大大小为53(+1)位，其潜在范围介于 — 9007199254740992和9007199254740992之间。 这是由于JavaScript的JSON实施表示长整数的方式存在限制。

有关字段类型的详细信息，请参阅有关[XDM字段类型约束](./schema/field-constraints.md)的文档。

### 什么是meta:AltId？

`meta:altId`是架构的唯一标识符。 `meta:altId`提供了一个易于引用的ID以用于API调用。 此ID可避免在每次与JSON URI格式一起使用时进行编码/解码。
<!-- (Needs clarification - How do I retrieve it INCOMPLETE) ... -->

<!-- ### How can I generate a sample payload for a schema? -->

<!-- No Answer available.  -->
<!-- INCOMPLETE ... -->

### 地图数据类型的使用限制是什么？

XDM对此数据类型的使用施加以下限制：

- 映射类型必须是`object`类型。
- 映射类型不能定义属性（换句话说，它们定义“空”对象）。
- 映射类型必须包含描述可以放置在映射中的值的`additionalProperties.type`字段，即`string`或`integer`。
- 多实体分段只能基于映射键而不是值定义。
- 帐户受众不支持映射。
- 在自定义XDM对象中定义的映射被限制在单个级别。 无法创建嵌套映射。 此限制不适用于标准XDM对象中定义的映射。
- 不支持映射数组。

有关更多详细信息，请参阅映射对象的[使用限制](./ui/fields/map.md#restrictions)。

>[!NOTE]
>
>不支持多级别映射或映射映射。

<!-- You cannot create a complex map object. However, you can define map fields in the Schema Editor. See the guide on [defining map fields in the UI](./ui/fields/map.md) for more information. -->

<!-- ### How do I create a complex map object using APIs? -->

<!-- You cannot create a complex map object. -->

<!-- ### How can I manage schema inheritance in Adobe Experience Platform? -->

<!-- No Answer available.  -->
<!-- INCOMPLETE ... -->

## 架构Identity Management

此部分包含有关在架构中定义和管理标识的常见问题解答。

### 如何定义架构的身份？

在[!DNL Experience Platform]中，无论解释的数据源如何，标识都用于标识主题（通常是个人）。 它们通过在架构中将关键字段标记为“标识”来定义。 身份识别的常用字段包括电子邮件地址、电话号码、[[!DNL Experience Cloud ID (ECID)]](https://experienceleague.adobe.com/docs/id-service/using/home.html)、CRM ID和其他唯一ID字段。

可使用API或用户界面将字段标记为标识。

### 在API中定义身份

在API中，身份是通过创建身份描述符来建立的。 身份描述符发出信号，表明模式的特定属性是唯一标识符。

标识描述符是由POST请求创建到/descriptors端点。 如果成功，您将收到HTTP状态201（已创建）和一个包含新描述符详细信息的响应对象。

有关在API中创建身份描述符的更多详细信息，请参阅[开发人员指南中](api/descriptors.md)描述符[!DNL Schema Registry]部分的文档。

### 在UI中定义身份

在架构编辑器中打开架构后，选择该编辑器的&#x200B;**[!UICONTROL Structure]**&#x200B;部分中要标记为标识的字段。 在右侧的&#x200B;**[!UICONTROL Field Properties]**&#x200B;下，选中&#x200B;**[!UICONTROL Identity]**&#x200B;复选框。

有关在UI中管理标识的更多详细信息，请参阅架构编辑器教程中[定义标识字段](./tutorials/create-schema-ui.md#identity-field)部分的相关部分。

### 我的架构是否需要主身份？

主身份是可选的，因为架构可能为零个或一个。 但是，架构必须具有主标识，才能启用架构以在[!DNL Real-Time Customer Profile]中使用。 有关详细信息，请参阅架构编辑器教程中的[标识](./tutorials/create-schema-ui.md#identity-field)部分。

## 架构配置文件启用

此部分提供有关启用架构以用于Real-time Customer Profile的指南。

### 如何启用架构以在[!DNL Real-Time Customer Profile]中使用？

通过在架构的[[!DNL Real-Time Customer Profile]](../profile/home.md)属性中添加“union”标记，启用架构以便在`meta:immutableTags`中使用。 可以使用API或用户界面启用用于[!DNL Profile]的架构。

### 使用API启用[!DNL Profile]的现有架构

发出PATCH请求以更新架构，并将`meta:immutableTags`属性添加为包含值“union”的数组。 如果更新成功，响应将显示更新的架构，该架构现在包含合并标记。

有关使用API启用架构以在[!DNL Real-Time Customer Profile]中使用的详细信息，请参阅[开发人员指南的](./api/unions.md)联合[!DNL Schema Registry]文档。

### 正在使用用户界面启用[!DNL Profile]的现有架构

在[!DNL Experience Platform]中，在左侧导航中选择&#x200B;**[!UICONTROL Schemas]**，然后从架构列表中选择要启用的架构的名称。 然后，在编辑器右侧的&#x200B;**[!UICONTROL Schema Properties]**&#x200B;下，选择&#x200B;**[!UICONTROL Profile]**&#x200B;以将其打开。

有关详细信息，请参阅[教程中有关](./tutorials/create-schema-ui.md#profile)在实时客户个人资料中使用[!UICONTROL Schema Editor]的部分。

### 将Adobe Analytics数据作为源导入时，是否为配置文件启用自动创建的架构？

架构未自动为实时客户配置文件启用。 您需要根据为配置文件启用的架构，为配置文件明确启用数据集。 请参阅文档，了解启用数据集以在Real-Time Customer Profile[中使用所需的](../catalog/datasets/user-guide.md#enable-profile)步骤和要求。

### 我是否可以删除启用配置文件的架构？ {#delete-profile-enabled}

为实时客户配置文件启用架构后，您无法删除该架构。 为配置文件启用架构后，无法禁用或删除该架构，并且无法从架构中删除字段。 因此，在为配置文件启用架构配置之前，仔细规划和验证架构配置至关重要。 但是，您可以删除启用了配置文件的数据集。 在此处找到信息： <https://experienceleague.adobe.com/en/docs/experience-platform/catalog/datasets/user-guide#delete-a-profile-enabled-dataset>

如果您不再希望使用启用了配置文件的架构，建议将该架构重命名为包含&#x200B;**不使用**&#x200B;或&#x200B;**不活动**。

## 架构修改和限制

此部分阐明模式修改规则和防止重大更改。

### 架构何时开始阻止重大更改？

对架构进行重大更改时，前提是从未在创建数据集中使用过该架构，或者未启用该架构以便在[[!DNL Real-Time Customer Profile]](../profile/home.md)中使用。 一旦在数据集创建中使用了某个架构或启用了与[!DNL Real-Time Customer Profile]一起使用，系统就会严格实施[架构演变](schema/composition.md#evolution)的规则。

### 能否直接编辑合并架构？

合并模式是只读的，由系统自动生成。 不能直接编辑它们。 在将“union”标记添加到实现特定类的架构时，会为该类创建联合架构。

有关XDM中联合的更多信息，请参阅[&#x200B; API指南中的](./api/unions.md)联合[!DNL Schema Registry]部分。

### 如何格式化数据文件以将数据摄取到我的架构中？

[!DNL Experience Platform]接受[!DNL Parquet]或JSON格式的数据文件。 这些文件的内容必须符合数据集引用的架构。 有关数据文件引入最佳实践的详细信息，请参阅[批次引入概述](../ingestion/home.md)。

### 如何将架构转换为只读架构？

您当前无法将架构转换为只读。

## 错误和故障排除

以下是使用[!DNL Schema Registry] API时可能遇到的错误消息列表。

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
>根据正在检索的资源类型，此错误可以使用以下`type`个URI中的任意一个：
>
>- `http://ns.adobe.com/aep/errors/XDM-1010-404`
>- `http://ns.adobe.com/aep/errors/XDM-1011-404`
>- `http://ns.adobe.com/aep/errors/XDM-1012-404`
>- `http://ns.adobe.com/aep/errors/XDM-1013-404`
>- `http://ns.adobe.com/aep/errors/XDM-1014-404`
>- `http://ns.adobe.com/aep/errors/XDM-1015-404`
>- `http://ns.adobe.com/aep/errors/XDM-1016-404`
>- `http://ns.adobe.com/aep/errors/XDM-1017-404`

有关在API中构造查找路径的更多信息，请参阅[开发人员指南中的](./api/getting-started.md#container)容器[和](api/getting-started.md#resource-identification)资源标识[!DNL Schema Registry]部分。

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
>根据命名空间错误的特定性质，此错误可以使用以下`type`个URI中的任意一个，以及不同的消息详细信息：
>
>- `http://ns.adobe.com/aep/errors/XDM-1020-400`
>- `http://ns.adobe.com/aep/errors/XDM-1021-400`
>- `http://ns.adobe.com/aep/errors/XDM-1022-400`
>- `http://ns.adobe.com/aep/errors/XDM-1023-400`
>- `http://ns.adobe.com/aep/errors/XDM-1024-400`

有关XDM资源的正确数据结构的详细示例，请参阅架构注册表API指南：

- [创建自定义类](./api/classes.md#create)
- [创建自定义字段组](./api/field-groups.md#create)
- [创建自定义数据类型](./api/data-types.md#create)

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

[!DNL Schema Registry] API中的GET请求需要`Accept`标头，以便系统确定如何设置响应的格式。 当必需的`Accept`标头无效或缺少时，会发生此错误。

根据您使用的端点，`detailed-message`属性指示有效的`Accept`标头应是什么样的，才能获得成功的响应。 在重试之前，请确保已正确输入与尝试发出的API请求兼容的`Accept`标头。

>[!NOTE]
>
>根据正在使用的端点，此错误可以使用以下`type`个URI中的任意一个：
>
>- `http://ns.adobe.com/aep/errors/XDM-1006-400`
>- `http://ns.adobe.com/aep/errors/XDM-1007-400`
>- `http://ns.adobe.com/aep/errors/XDM-1008-400`
>- `http://ns.adobe.com/aep/errors/XDM-1009-400`

有关不同API请求的兼容“接受”标头的列表，请参阅[架构注册表开发人员指南](./api/overview.md)中相应章节。

### [!DNL Real-Time Customer Profile]个错误

以下错误消息与启用[!DNL Real-Time Customer Profile]的架构所涉及的操作相关联。 有关详细信息，请参阅[&#x200B; API指南中的](./api/unions.md)联合[!DNL Schema Registry]部分。

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

当您尝试启用[!DNL Profile]的架构并且其中一个属性包含没有引用标识描述符的关系描述符时，将显示此错误消息。 将引用身份描述符添加到有问题的架构字段以解决此错误。

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

为了启用包含关系描述符的架构以便在[!DNL Profile]中使用，源字段的命名空间和引用字段的主命名空间必须相同。 当您尝试启用一个方案（该方案的引用标识描述符包含不匹配的命名空间）时，将显示此错误消息。

请确保引用架构标识字段的`xdm:namespace`值与源字段的引用标识描述符中的`xdm:identityNamespace`属性的值匹配以解决此问题。

有关标准身份命名空间代码的列表，请参阅身份命名空间概述中有关[标准命名空间](../identity-service/features/namespaces.md)的部分。

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

在为配置文件启用架构之前，必须首先[为该架构创建主标识描述符](./api/descriptors.md#create)，或包含标识映射字段以充当主标识。

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
