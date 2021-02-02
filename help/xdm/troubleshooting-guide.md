---
keywords: Experience Platform；主题；XDM;XDM系统；XDM个人用户档案;XDM体验事件；XDM体验事件；体验事件；体验体验事件;XDM体验事件；体验数据模型；体验数据模型；数据模型模型；模式；疑难解答；常见问题解答；常见问题；合并模式;合并用户档案;合并用户档案
solution: Experience Platform
title: 体验数据模型(XDM)系统疑难解答指南
description: 本文档提供有关体验数据模型(XDM)系统的常见问题解答，以及常见错误的疑难解答指南。
topic: troubleshooting
translation-type: tm+mt
source-git-commit: 2dbd92efbd992b70f4f750b09e9d2e0626e71315
workflow-type: tm+mt
source-wordcount: '1873'
ht-degree: 0%

---


# [!DNL Experience Data Model] (XDM)系统故障排除指南

本文档提供有关[!DNL Experience Data Model](XDM)系统的常见问题解答，以及常见错误的疑难解答指南。 有关与Adobe Experience Platform其他服务相关的问题和疑难解答，请参阅[Experience Platform疑难解答指南](../landing/troubleshooting.md)。

**[!DNL Experience Data Model](XDM)是** 一种开放源码规范，它为客户体验管理定义了标准化模式。构建[!DNL Experience Platform]的方法，**XDM系统**，操作[!DNL Experience Data Model]模式以供[!DNL Platform]服务使用。 **[!DNL Schema Registry]**&#x200B;提供一个用户界面和一个RESTful API，用于访问[!DNL Experience Platform]中的&#x200B;**[!DNL Schema Library]**。 有关详细信息，请参阅[XDM文档](home.md)。

## 常见问题解答

以下是有关XDM系统和[!DNL Schema Registry] API使用的常见问题的列表解答。

### 如何向模式添加字段？

您可以使用混音将字段添加到模式。 每个混音符与一个或多个类兼容，允许混音符用于实现这些兼容类之一的任何模式。 Adobe Experience Platform提供多个行业混音及其自己的预定义字段，您可以通过使用API或用户界面创建新混音，将您自己的字段添加到模式。

有关在[!DNL Schema Registry] API中创建新混音的详细信息，请参阅[mixin端点指南](api/mixins.md#create)。 如果您使用的是UI，请参阅[模式编辑器教程](./tutorials/create-schema-ui.md)。

### 混音与数据类型的最佳用途是什么？

[密](./schema/composition.md#mixin) 信是定义模式中一个或多个字段的组件。Mixins强制其字段在模式层次结构中的显示方式，因此在每个模式中都显示其包含的相同结构。 Mixin只与特定类兼容，由其`meta:intendedToExtend`属性标识。

[数](./schema/composition.md#data-type) 据类型还可以为模式提供一个或多个字段。但是，与混音不同，数据类型不限于特定类。 这使得数据类型成为描述可跨具有潜在不同类的多个模式重用的常见数据结构的更灵活的选项。

### 模式的唯一ID是什么？

所有[!DNL Schema Registry]资源(模式、混合、数据类型、类)都有一个URI，它充当唯一ID，用于引用和查找。 在API中查看模式时，可以在顶级`$id`和`meta:altId`属性中找到它。

有关详细信息，请参阅[!DNL Schema Registry] API开发人员指南中的[资源标识](api/getting-started.md#resource-identification)部分。

### 模式开始何时阻止中断更改？

只要模式从未在创建数据集时使用过或在[[!DNL Real-time Customer Profile]](../profile/home.md)中启用过，就可以对其进行中断更改。 在模式集创建中使用或启用与[!DNL Real-time Customer Profile]一起使用后，系统将严格执行[模式演化](schema/composition.md#evolution)的规则。

### 长字段类型的最大大小是多少？

长场类型是一个最大大小为53(+1)位的整数，它的势范围为-9007199254740992和9007199254740992。 这是由于JSON的JavaScript实现如何表示长整数存在限制。

有关字段类型的详细信息，请参阅[XDM字段类型约束](./schema/field-constraints.md)的文档。

### 如何定义模式的身份？

在[!DNL Experience Platform]中，身份用于标识主体（通常是个人），而不管解释的数据来源如何。 通过将键字段标记为“Identity”，在模式中定义这些字段。 常用的标识字段包括电子邮件地址、电话号码、[[!DNL Experience Cloud ID (ECID)]](https://experienceleague.adobe.com/docs/id-service/using/home.html)、CRM ID和其他唯一ID字段。

字段可以使用API或用户界面标记为标识。

#### 在API中定义身份

在API中，通过创建标识描述符来建立标识。 标识描述符表示模式的特定属性是唯一标识符。

标识描述符由POST请求创建到/descriptors端点。 如果成功，您将收到一个HTTP状态201（已创建）和一个包含新描述符详细信息的响应对象。

有关在API中创建标识描述符的详细信息，请参阅[!DNL Schema Registry]开发人员指南中[描述符](api/descriptors.md)部分的文档。

#### 在UI中定义标识

在模式编辑器中打开模式后，在编辑器的&#x200B;**[!UICONTROL 结构]**&#x200B;部分选择要标记为标识的字段。 在右侧的&#x200B;**[!UICONTROL 字段属性]**&#x200B;下，选中&#x200B;**[!UICONTROL 标识]**&#x200B;复选框。

有关在UI中管理身份的详细信息，请参阅模式编辑器教程中[定义身份字段](./tutorials/create-schema-ui.md#identity-field)一节。

### 我的模式需要主要身份吗？

主身份是可选的，因为模式可能有0或1个身份。 但是，模式必须具有主标识，才能启用模式在[!DNL Real-time Customer Profile]中使用。 有关详细信息，请参阅模式编辑器教程的[identity](./tutorials/create-schema-ui.md#identity-field)部分。

### 如何启用模式以在[!DNL Real-time Customer Profile]中使用？

模式可通过添加“合并”标签在`meta:immutableTags`模式的属性中使用。 [[!DNL Real-time Customer Profile]](../profile/home.md)可以使用API或用户界面启用与[!DNL Profile]一起使用的模式。

#### 使用API为[!DNL Profile]启用现有模式

发出PATCH请求以更新模式，并将`meta:immutableTags`属性添加为包含值“合并”的数组。 如果更新成功，则响应将显示更新的模式，该合并现在包含该更新标记。

有关使用API启用模式以在[!DNL Real-time Customer Profile]中使用的详细信息，请参阅[!DNL Schema Registry]开发人员指南的[合并](./api/unions.md)文档。

#### 使用UI为[!DNL Profile]启用现有模式

在[!DNL Experience Platform]中，在左侧导航中选择&#x200B;**[!UICONTROL 模式]**，并从模式列表中选择要启用的模式的名称。 然后，在编辑器右侧的&#x200B;**[!UICONTROL 模式属性]**&#x200B;下，选择&#x200B;**[!UICONTROL 用户档案]**&#x200B;将其打开。


有关详细信息，请参阅[!UICONTROL 模式编辑器]教程中关于[在实时客户用户档案](./tutorials/create-schema-ui.md#profile)中使用的部分。

### 能否直接编辑合并模式?

合并模式是只读的，由系统自动生成。 不能直接编辑。 合并模式是在将“合并”标签添加到实现该类的模式时为特定类创建的。

有关XDM中合并的详细信息，请参阅[!DNL Schema Registry] API开发人员指南中的[合并](./api/unions.md)部分。

### 如何格式化数据文件以将数据引入模式?

[!DNL Experience Platform] 接受JSON格式 [!DNL Parquet] 或JSON格式的数据文件。这些文件的内容必须符合数据集引用的模式。 有关数据文件摄取的最佳实践的详细信息，请参阅[批处理摄取概述](../ingestion/home.md)。

## 错误和疑难解答

以下是使用[!DNL Schema Registry] API时可能遇到的一列表错误消息。

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

有关在API中构建查找路径的详细信息，请参阅[!DNL Schema Registry]开发人员指南中的[容器](./api/getting-started.md#container)和[资源标识](api/getting-started.md#resource-identification)部分。

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

当您尝试创建名称不正确的字段的新混音时，会显示此错误消息。 IMS组织定义的混音必须用`TENANT_ID`命名空间其字段，以避免与其他行业和供应商资源发生冲突。 在[mixins端点指南](./api/mixins.md#create)中可以找到混合的正确数据结构的详细示例。


### [!DNL Real-time Customer Profile] 错误

以下错误消息与为[!DNL Real-time Customer Profile]启用模式所涉及的操作相关。 有关详细信息，请参阅[!DNL Schema Registry] API开发人员指南中的[合并](./api/unions.md)部分。

#### 要启用用户档案数据集，模式应有效

```json
{
    "type": "/placeholder/type/uri",
    "status": 400,
    "title": "BadRequestError",
    "detail": "To enable profile datasets the schema should be valid"
}
```

当您尝试为尚未为[!DNL Real-time Customer Profile]启用的用户档案启用模式数据集时，将显示此错误消息。 在启用模式集之前，请确保该合并包含一个数据标记。

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

当您尝试为[!DNL Profile]启用模式时，会显示此错误消息，其其中一个属性包含没有引用标识描述符的关系描述符。 将引用标识描述符添加到相关模式字段以解决此错误。

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

要启用包含关系描述符的模式以在[!DNL Profile]中使用，源字段的命名空间和目标字段的主命名空间必须相同。 当您尝试启用包含引用标识描述符的不匹配模式的命名空间时，将显示此错误消息。 确保目标模式的标识字段的`xdm:namespace`值与源字段的引用标识描述符中的`xdm:identityNamespace`属性的值相匹配，以解决此问题。

有关受支持身份命名空间代码的列表，请参阅身份命名空间概述中[标准命名空间](../identity-service/namespaces.md)的一节。

### 接受标题错误

[!DNL Schema Registry] API中的大多数GET请求都需要一个Accept头，以便系统确定如何格式化响应。 以下是与“接受”标题关联的常见错误列表。 有关不同API请求的一列表兼容的接受标头，请参阅[模式注册表开发人员指南](api/getting-started.md)中的相应部分。

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

在查找描述符时，如果Accept头提供不正确，则显示此错误消息。 在重试之前，请确保已正确输入了描述符](./api/descriptors.md)支持的[接受标头之一。

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

有关受支持的接受头的列表，请参阅[!DNL Schema Registry]开发人员指南中的[接受头](api/getting-started.md#accept)部分。

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