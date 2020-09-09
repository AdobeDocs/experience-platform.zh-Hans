---
keywords: Experience Platform;home;popular topics;;XDM;XDM system;XDM individual profile;XDM ExperienceEvent;XDM Experience Event;experienceEvent;experience eventExperience event;XDM Experience Event;XDM ExperienceEvent;;experience data model;Experience data model;Experience Data Model;data model;Data Model;schema;troubleshooting;FAQ;faq;Union schema;UNION PROFILE;union profile
solution: Experience Platform
title: 体验数据模型(XDM)系统疑难解答指南
description: 本文档提供有关体验数据模型(XDM)系统的常见问题解答，以及常见错误的疑难解答指南。
topic: troubleshooting
translation-type: tm+mt
source-git-commit: 2a528c705a7aa610f57047be39be1ce9886ce44c
workflow-type: tm+mt
source-wordcount: '1862'
ht-degree: 0%

---


# [!DNL Experience Data Model] (XDM)系统故障排除指南

此文档提供有关(XDM)系统的常 [!DNL Experience Data Model] 见问题的解答，以及常见错误的疑难解答指南。 有关与Adobe Experience Platform其他服务相关的问题和疑难解答，请参阅 [Experience Platform疑难解答指南](../landing/troubleshooting.md)。

**[!DNL Experience Data Model](XDM)是一种开放源** ，它为客户体验管理定义了标准化模式。 构建XDM系统 [!DNL Experience Platform] 的方法 **将模式运**&#x200B;行，供服务 [!DNL Experience Data Model][!DNL Platform] 使用。 提供 **[!DNL Schema Registry]** 一个用户界面和一个REST风格的API，用于访问 **[!DNL Schema Library]** 内部 [!DNL Experience Platform]。 See the [XDM documentation](home.md) for more information.

## 常见问题解答

以下是有关XDM系统和API使用的常见问题的一列表解 [!DNL Schema Registry] 答。

### 如何向模式添加字段？

您可以使用混音将字段添加到模式。 每个混音符与一个或多个类兼容，允许混音符用于实现这些兼容类之一的任何模式。 Adobe Experience Platform提供多个行业混音及其自己的预定义字段，您可以通过使用API或用户界面创建新混音，将您自己的字段添加到模式。

有关在API中创建新混音的详细信息，请参 [阅API开发人员指南](api/create-mixin.md) 中的“创 [!DNL Schema Registry] 建混音”文档。 如果您使用的是UI，请参阅 [模式编辑器教程](./tutorials/create-schema-ui.md)。

### 混音与数据类型的最佳用途是什么？

[混合](./schema/composition.md#mixin) 是定义模式中一个或多个字段的组件。 Mixins强制其字段在模式层次结构中的显示方式，因此在每个模式中都显示其包含的相同结构。 Mixin只与特定类兼容，由其属性标 `meta:intendedToExtend` 识。

[数据类型](./schema/composition.md#data-type) 还可以为模式提供一个或多个字段。 但是，与混音不同，数据类型不限于特定类。 这使得数据类型成为描述可跨具有潜在不同类的多个模式重用的常见数据结构的更灵活的选项。

### 模式的唯一ID是什么？

所 [!DNL Schema Registry] 有资源(模式、混音、数据类型、类)都有一个URI，它充当唯一ID，用于引用和查找目的。 在API中查看模式时，可以在顶级和属性中找 `$id` 到 `meta:altId` 它。

有关详细信息，请参 [阅API开发](api/getting-started.md#schema-identification) 人员指南 [!DNL Schema Registry] 中的模式标识部分。

### 模式开始何时阻止中断更改？

只要模式从未在创建数据集时使用过或在[!DNL实时用户档案中启用过，就可以对其进行 [中断更改]](../profile/home.md)。 一旦模式被用于数据集创建或启用与一起使 [!DNL Real-time Customer Profile]用，模式进化规 [则就会被系](schema/composition.md#evolution) 统严格执行。

### 长字段类型的最大大小是多少？

长场类型是一个最大大小为53(+1)位的整数，它的势范围为-9007199254740992和9007199254740992。 这是由于JSON的JavaScript实现如何表示长整数存在限制。

有关字段类型的详细信息，请参 [阅API开发人员指南](api/appendix.md#field-types) 中的定 [!DNL Schema Registry] 义XDM字段类型部分。

### 如何定义模式的身份？

在 [!DNL Experience Platform]中，无论被解释的数据来源如何，都使用身份来标识主体（通常是个人）。 通过将键字段标记为“Identity”，在模式中定义这些字段。 常用标识字段包括电子邮件地址、电 [话号码、[!DNLExperience CloudID(ECID)]](https://docs.adobe.com/content/help/zh-Hans/id-service/using/home.html)、CRM ID和其他唯一ID字段。

字段可以使用API或用户界面标记为标识。

#### 在API中定义身份

在API中，通过创建标识描述符来建立标识。 标识描述符表示模式的特定属性是唯一标识符。

标识描述符由POST请求创建到/descriptors端点。 如果成功，您将收到一个HTTP状态201（已创建）和一个包含新描述符详细信息的响应对象。

有关在API中创建标识描述符的更多详细信息，请参阅开发人 [员指南](api/descriptors.md) “描述符 [!DNL Schema Registry] 文档”部分。

#### 在UI中定义标识

在模式编辑器中打开模式后，单击该编辑器的“结 **[!UICONTROL 构]** ”部分中要标记为标识的字段。 在 **[!UICONTROL 右侧的]** “字段属性”下，单击“标识” **[!UICONTROL 复选框]** 。

有关在UI中管理身份的更多详细信息，请参阅模式编 [辑器教程中](./tutorials/create-schema-ui.md#identity-field) “定义身份字段”一节。

### 我的模式需要主要身份吗？

主身份是可选的，因为模式可能有0或1个身份。 但是，模式必须具有主标识，才能启用模式在中使用 [!DNL Real-time Customer Profile]。 有关详细 [信息](./tutorials/create-schema-ui.md#identity-field) ，请参阅模式编辑器教程的标识部分。

### 如何启用模式以在中使用 [!DNL Real-time Customer Profile]?

通过添加“模式”标 [签(位于合并的属性中)](../profile/home.md) ,模式可以在实时客户 `meta:immutableTags` 用户档案中使用。 可以使用API或 [!DNL Profile] 用户界面启用模式以与一起使用。

#### 启用现有模式 [!DNL Profile] 以使用API

发出PATCH请求以更新模式，并将属 `meta:immutableTags` 性添加为包含值“合并”的数组。 如果更新成功，则响应将显示更新的模式，该合并现在包含该更新标记。

有关使用API启用模式以在中使用的详细信 [!DNL Real-time Customer Profile]息，请参 [阅开发人](./api/unions.md) 员指南的 [!DNL Schema Registry] 合并文档。

#### 启用现有模式 [!DNL Profile] 以使用UI

在 [!DNL Experience Platform]中，单 **[!UICONTROL 击左侧导航]** 中的模式，并从模式列表中选择要启用的模式的名称。 然后，在编辑器的右侧的“模式属性 **[!UICONTROL ”下]**，单击 **[!UICONTROL 用户档案]** ，以将其打开。


有关详细信息，请参阅 [模式编辑器教程中的“实时用户档案](./tutorials/create-schema-ui.md#profile) ”中 [!UICONTROL 的使用部分] 。

### 能否直接编辑合并模式?

合并模式是只读的，由系统自动生成。 不能直接编辑。 合并模式是在将“合并”标签添加到实现该类的模式时为特定类创建的。

有关XDM中合并的更多信息，请参 [阅](./api/unions.md) API开发人 [!DNL Schema Registry] 员指南中的合并部分。

### 如何格式化数据文件以将数据引入模式?

[!DNL Experience Platform] 接受或JSON格 [!DNL Parquet] 式的数据文件。 这些文件的内容必须符合数据集引用的模式。 有关数据文件摄取的最佳实践的详细信息，请参 [阅批处理摄取概述](../ingestion/home.md)。

## 错误和疑难解答

以下是您在使用API时可能遇到的一列表错误 [!DNL Schema Registry] 消息。

### 找不到对象

```json
{
    "type": "/placeholder/type/uri",
    "status": 404,
    "title": "NotFoundError",
    "detail": "Object https://ns.adobe.com/incorrectTenantId/schemas/ee067e31b08514d21e2b82577813409d 
      with version 1 not found"
}
```

系统找不到特定资源时显示此错误。 资源可能已被删除，或API调用中的路径无效。 在再次尝试之前，请确保已为API调用输入有效路径。 您可能需要检查是否已为资源输入了正确的ID，以及路径是否以适当的容器（全局或租户）命名。

有关在API中构建查找路径的详细信息，请参 [阅开发](./api/getting-started.md#container) 人员指 [南中](api/getting-started.md#schema-identification)[!DNL Schema Registry] 的容器和模式识别部分。

### 标题必须唯一

```json
{
    "type": "/placeholder/type/uri",
    "status": 400,
    "title": "BadRequestError",
    "detail": "Title must be unique. An object 
      https://ns.adobe.com/{TENANT_ID}/schemas/26f6833e55db1dd8308aa07a64f2042d 
      already exists with the same title."
}
```

当您尝试创建标题已被其他资源使用的资源时，会显示此错误消息。 标题在所有资源类型中必须是唯一的。 例如，如果您尝试创建标题已被模式使用的混音，您将收到此错误。

### 自定义字段必须使用顶级字段

```json
{
    "type": "/placeholder/type/uri",
    "status": 400,
    "title": "BadRequestError",
    "detail": "For custom fields, you must use a top level field named _{TENANT_ID}
       and all the other fields must be defined under it"
}
```

当您尝试创建名称不正确的字段的新混音时，会显示此错误消息。 IMS组织定义的混音必须用a命名空间其字段，以 `TENANT_ID` 避免与其他行业和供应商资源发生冲突。 有关混合的正确文档结构的详细示例，请参阅API开发 [人员指南中](api/create-mixin.md) “创建混合 [!DNL Schema Registry] ”一节。


### [!DNL Real-time Customer Profile] 错误

以下错误消息与启用模式时涉及的操作相关 [!DNL Real-time Customer Profile]。 有关更 [多信息](./api/unions.md) ，请参 [!DNL Schema Registry] 阅API开发人员指南中的“合并”部分。

#### 要启用用户档案数据集，模式应有效

```json
{
    "type": "/placeholder/type/uri",
    "status": 400,
    "title": "BadRequestError",
    "detail": "To enable profile datasets the schema should be valid"
}
```

当您尝试为尚未启用的用户档案启用模式数据集时，将显示此错误消息 [!DNL Real-time Customer Profile]。 在启用模式集之前，请确保该合并包含一个数据标记。

#### 必须有引用标识描述符

```json
{
    "type": "/placeholder/type/uri",
    "status": 400,
    "title": "BadRequestError",
    "detail": "For a schema to be able to participate in union, if any of its 
      property is associated with a xdm:descriptorOneToOne descriptor, there must 
      be a xdm:descriptorReferenceIdentity descriptor for that property"
}
```

当您尝试为模式启用时，将显示此错误 [!DNL Profile] 消息，其其中一个属性包含没有引用标识描述符的关系描述符。 将引用标识描述符添加到相关模式字段以解决此错误。

#### 引用标识描述符字段的命名空间和目标模式必须匹配

```json
{
    "type": "/placeholder/type/uri",
    "status": 400,
    "title": "BadRequestError",
    "detail": "If both schemas from an already defined xdm:descriptorOneToOne 
      descriptor are promoted to union, and if there is a primary identity on one of 
      the schemas from the xdm:descriptorOneToOne descriptor, the 
      xdm:identityNamespace of the sourceSchema's descriptorReferenceIdentity and the 
      xdm:namespace field of the xdm:descriptorIdentity for the destinationSchema must 
      match"
}
```

为了使包含关系描述符的模式能够 [!DNL Profile]在中使用，源字段的命名空间和目标字段的主命名空间必须相同。 当您尝试启用包含引用标识描述符的不匹配模式的命名空间时，将显示此错误消息。 确保目 `xdm:namespace` 标模式的标识字段的值与源字段的引用标 `xdm:identityNamespace` 识描述符中的属性的值相匹配，以解决此问题。

有关受支持身份命名空间代码的列表，请参阅标 [识命名空间概](../identity-service/namespaces.md) 述中“标准命名空间”一节。

### 接受标题错误

API中的大多数GET [!DNL Schema Registry] 请求都需要一个“接受”头，以便系统确定如何格式化响应。 以下是与“接受”标题关联的常见错误列表。 有关不同API请求的一列表兼容的“接受”标头，请参阅“模式注册表开发人 [员指南”中的相应部分](api/getting-started.md)。

#### 需要接受头参数

```json
{
    "type": "/placeholder/type/uri",
    "status": 406,
    "title": "NotAcceptableError",
    "detail": "Accept header parameter is required"
}
```

当API请求中缺少Accept头时，将显示此错误消息。 再次尝试之前，请确保包含“接受”头。

#### 未知接受提供的媒体

```json
{
    "type": "/placeholder/type/uri",
    "status": 406,
    "title": "NotAcceptableError",
    "detail": "Unknown Accept media supplied: xed+json"
}
```

当接受标头无效时，将显示此错误消息。 在再次尝试之前，请确保已正确输入与您尝试发出的API请求兼容的“接受”标头。

#### 可用的未知接受格式

```json
{
    "type": "/placeholder/type/uri",
    "status": 406,
    "title": "NotAcceptableError",
    "detail": "Unknown Accept format available "
}
```

在查找描述符时，如果Accept头提供不正确，则显示此错误消息。 在重试之前，请确保已正确输入 [了支持的描述符的](./api/descriptors.md) “接受”标头。

#### 必须在“接受”标题中提供版本

```json
{
    "type": "/placeholder/type/uri",
    "status": 400,
    "title": "BadRequestError",
    "detail": "version must be supplied in the accept header. Example: 
      application/vnd.adobe.xed-full-notext+json; version=1"
}
```

当版本号未包含在“接受”标题中时，将显示此错误消息。 某些元素(如模式)在查找单个实例时需要指定版本。 包含版本号的Accept头的外观将类似于：

```plaintext
application/vnd.adobe.xed+json; version=1
```

有关受支持的接受标头的列表，请参 [阅开发人员指南](api/getting-started.md#accept) 中的接 [!DNL Schema Registry] 受标头部分。

#### Accept头中不能提供版本

```json
{
    "type": "/placeholder/type/uri",
    "status": 400,
    "title": "BadRequestError",
    "detail": "version must not be supplied in the accept header. Example: 
      application/vnd.adobe.xed-full+json"
}
```

如果在列出(GET)资源时尝试在“接受”标题中包含版本，您将收到此错误。 版本仅在尝试查找单个资源时才是必需的。 从“接受”标题中删除版本以解决错误。
