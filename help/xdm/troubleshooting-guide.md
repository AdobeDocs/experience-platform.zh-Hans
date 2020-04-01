---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 体验数据模型(XDM)系统疑难解答指南
topic: troubleshooting
translation-type: tm+mt
source-git-commit: f7c87cc86bfc5017ec5c712d05e39be5c14a7147

---


# 体验数据模型(XDM)系统疑难解答指南

本文档提供有关体验数据模型(XDM)系统的常见问题解答以及常见错误的疑难解答指南。 有关Adobe Experience Platform中其他服务的相关问题和疑难解答，请参阅 [Experience Platform疑难解答指南](../landing/troubleshooting.md)。

**Experience Data Model(XDM)** 是一个开放源代码规范，它为客户体验管理定义了标准化模式。 构建Experience Platform的方法( **XDM System**)可操作Experience Data Model模式，以供平台服务使用。 模式 **注册表提供用户界面** ，并提供一个RESTful API，用于访问Experience Platform中 **的模式库** 。 See the [XDM documentation](home.md) for more information.

## 常见问题解答

以下是关于XDM系统和模式注册表API使用的常见问题解答列表。

### 如何向模式添加字段？

您可以使用混音将字段添加到模式。 每个混音与一个或多个类兼容，允许混音在实现这些兼容类之一的任何模式中使用。 虽然Adobe Experience Platform提供了多个行业混音以及它们自己的预定义字段，但您可以通过使用API或用户界面创建新混音来将您自己的字段添加到模式。

有关在API中创建新混音的详细信息，请参 [阅模式注册表](api/create-mixin.md) API开发人员指南中的创建混音文档。 如果您使用的是UI，请参阅 [模式编辑器教程](./tutorials/create-schema-ui.md)。

### 混音与数据类型的最佳用途是什么？

[Mixin](./schema/composition.md#mixin) 是定义模式中一个或多个字段的组件。 Mixin强制其字段在模式层次结构中的显示方式，因此在每个模式中显示的结构与包含在其中的结构相同。 Mixin只与特定类兼容，由其属性标识 `meta:intendedToExtend` 出来。

[数据类型](./schema/composition.md#data-type) ，还可以为模式提供一个或多个字段。 但是，与混音不同，数据类型不限于特定类。 这使得数据类型成为描述可跨具有潜在不同类的多个模式重用的常见数据结构的更灵活的选项。

### 模式的唯一ID是什么？

所有模式注册表资源(模式、混音、数据类型、类)都有一个URI，它用作唯一ID以用于引用和查找目的。 在API中查看模式时，可以在顶级和属性中找 `$id` 到 `meta:altId` 它。

有关详细信息，请参阅 [模式注册](api/getting-started.md#schema-identification) API开发人员指南中的模式标识部分。

### 模式开始何时防止更改中断？

只要从未在创建数据集中使用过或在实时客户模式中启用过，就可以对用户档案进行突破性更改 [](../profile/home.md)。 在数据集创建中使用模式或启用实时客户用户档案后，系统将严格执行 [](schema/composition.md#evolution) 模式演化规则。

### 长字段类型的最大大小是多少？

长字段类型是一个最大大小为53(+1)位的整数，它的电位范围为-9007199254740992和9007199254740992。 这是由于JSON的JavaScript实现如何表示长整数存在限制。

有关字段类型的详细信息，请参 [阅模式注册API开发人员指南中的](api/appendix.md#field-types) “定义XDM字段类型”一节。

### 如何为我的模式定义身份？

在Experience Platform中，身份用于标识主体（通常是个人），而不管解释的数据来源如何。 在模式中通过将键字段标记为“标识”来定义这些字段。 常用的标识字段包括电子邮件地址、电话号码、 [Experience Cloud ID(ECID)](https://marketing.adobe.com/resources/help/en_US/mcvid/)、CRM ID和其他唯一ID字段。

字段可以使用API或用户界面标为身份。

#### 在API中定义身份

在API中，通过创建标识描述符来建立标识。 标识描述符表示模式的特定属性是唯一标识符。

标识描述符是由到/descriptors端点的POST请求创建的。 如果成功，您将收到HTTP状态201（已创建）和包含新描述符详细信息的响应对象。

有关在API中创建标识描述符的更多详细信息，请参阅文档注册 [表开发人员指南](api/descriptors.md) “描述符”一节。

#### 在UI中定义身份

在模式编辑器中打开模式后，单击要标记为标识的编辑器的“结构 **** ”部分中的字段。 在右 **侧的“字段属性** ”下，单击“标识” **复选框** 。

有关在UI中管理身份的更多详细信息，请参阅模式编辑器教 [程中的定义身份字段](./tutorials/create-schema-ui.md#identity-field) 一节。

### 我的模式需要主要身份吗？

主要身份是可选的，因为模式可能有0或1个身份。 但是，模式必须具有主要身份，才能启用模式以在实时客户用户档案中使用。 有关详细 [信息](./tutorials/create-schema-ui.md#identity-field) ，请参阅模式编辑器教程的标识部分。

### 如何启用模式以用于实时客户用户档案?

模式通过添加“ [合并](../profile/home.md) ”标签(位于模式属性中)，可以在实时客户 `meta:immutableTags` 用户档案中使用。 可以使用API或用户界面启用与用户档案一起使用的模式。

#### 使用API启用现有模式进行用户档案

发出PATCH请求以更新模式，并将属 `meta:immutableTags` 性添加为包含值“合并”的数组。 如果更新成功，则响应将显示更新的模式，该合并现在包含该更新标记。

有关使用API启用模式以用于实时客户用户档案的更多信息，请参阅模式注册开发人员指南的 [合并](./api/unions.md) 文档。

#### 使用UI启用现有模式进行用户档案

在Experience Platform中，单击左 **侧导航中的模式** ，然后从列表中选择要启用的模式的名称。 然后，在编辑器的右侧的“ **模式属性**”下，单击 **** 用户档案以将其打开。


有关详细信息，请参阅用户档案编 [辑器教程中有关在实时客户模式中使](./tutorials/create-schema-ui.md#profile) 用的部分。

### 是否可以直接编辑合并模式?

合并模式是只读的，由系统自动生成。 不能直接编辑。 合并模式是在将“合并”标签添加到实现该类的模式时为特定类创建的。

有关XDM中合并的详细信息，请参阅 [合并注册](./api/unions.md) API开发人员指南中的“模式”部分。

### 如何格式化数据文件以将数据收录到我的模式?

Experience Platform接受Parke或JSON格式的数据文件。 这些文件的内容必须符合数据集引用的模式。 有关数据文件摄取的最佳实践的详细信息，请参阅批 [量摄取概述](../ingestion/home.md)。

## 错误和疑难解答

以下是一列表错误消息，在使用模式注册表API时可能会遇到这些错误消息。

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

当系统无法找到特定资源时，将显示此错误。 该资源可能已被删除，或API调用中的路径无效。 在再次尝试之前，请确保您已为API调用输入了有效路径。 您可能希望检查您是否为资源输入了正确的ID，以及路径是否与相应的容器（全局或租户）正确命名。

有关在API中构建查找路径的详细信息，请参阅 [容器](./api/getting-started.md#container)[](api/getting-started.md#schema-identification) 和模式标识部分(在模式注册表开发人员指南中)。

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

当您尝试创建标题已被其他资源使用的资源时，会显示此错误消息。 标题在所有资源类型中必须是唯一的。 例如，如果尝试创建标题已被模式使用的混音，您将收到此错误。

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

当您尝试创建名称不正确的字段的新混音时，将显示此错误消息。 IMS组织定义的混音必须用a命名空间其字段，以 `TENANT_ID` 避免与其他行业和供应商资源发生冲突。 有关混合的正确数据结构的详细示例，请参阅文档注册API开发 [人员指南中有关创建混合](api/create-mixin.md) 的模式部分。


### 实时客户用户档案错误

以下错误消息与启用实时客户用户档案的模式所涉及的操作相关。 有关详细 [信息](./api/unions.md) ，请参阅模式注册API开发人员指南中的“合并”部分。

#### 要启用用户档案数据集，模式应有效

```json
{
    "type": "/placeholder/type/uri",
    "status": 400,
    "title": "BadRequestError",
    "detail": "To enable profile datasets the schema should be valid"
}
```

当您尝试为尚未启用“实时客户”用户档案的模式启用用户档案数据集时，将显示此错误消息。 在启用数据集之前，请确保模式包含合并标记。

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

当您尝试为用户档案启用模式时，此错误消息会显示，其中一个属性包含没有引用标识描述符的关系描述符。 将引用标识描述符添加到相关的模式字段以解决此错误。

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

为了使包含关系描述符的模式能够在用户档案中使用，源字段的命名空间和目标字段的主命名空间必须相同。 当您尝试启用包含引用标识描述符的不匹配命名空间的模式时，将显示此错误消息。 确保目 `xdm:namespace` 标模式的标识字段的值与源字段的引用标识描述符中 `xdm:identityNamespace` 的属性的值相匹配，以解决此问题。

有关受支持身份命名空间代码的列表，请参阅标 [识命名空间概述中](../identity-service/namespaces.md) “标准命名空间”一节。

### 接受标题错误

模式注册表API中的大多数GET请求都需要一个“接受”头，以便系统确定如何设置响应的格式。 以下是与Accept头相关的一列表常见错误。 有关不同API请求的一列表兼容接受标题，请参阅模式注册表开发人员指南中 [的相应章节](api/getting-started.md)。

#### Accept header参数是必需的

```json
{
    "type": "/placeholder/type/uri",
    "status": 406,
    "title": "NotAcceptableError",
    "detail": "Accept header parameter is required"
}
```

当API请求中缺少Accept头时，将显示此错误消息。 在再次尝试之前，请确保包含“接受”标题。

#### 未知接受提供的介质

```json
{
    "type": "/placeholder/type/uri",
    "status": 406,
    "title": "NotAcceptableError",
    "detail": "Unknown Accept media supplied: xed+json"
}
```

当Accept头无效时，将显示此错误消息。 在再次尝试之前，请确保您已正确输入了与您尝试发出的API请求兼容的“接受”标题。

#### 可用的未知接受格式

```json
{
    "type": "/placeholder/type/uri",
    "status": 406,
    "title": "NotAcceptableError",
    "detail": "Unknown Accept format available "
}
```

在查找描述符时，当Accept头提供不正确时，将显示此错误消息。 在再次尝试之前，请确保已为描述符 [正确输入了支持的接受标头](./api/descriptors.md) 之一。

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

当版本号未包含在“接受”标题中时，将显示此错误消息。 某些元素(如模式)需要在查找单个实例时指定版本。 包含版本号的“接受”标题将类似于以下内容：

```plaintext
application/vnd.adobe.xed+json; version=1
```

有关受支持的“接受”标题的列表，请参阅“ [模式注册表”开发人员指南中的“接受](api/getting-started.md#accept) ”标题部分。

#### 版本不得在“接受”标题中提供

```json
{
    "type": "/placeholder/type/uri",
    "status": 400,
    "title": "BadRequestError",
    "detail": "version must not be supplied in the accept header. Example: 
      application/vnd.adobe.xed-full+json"
}
```

如果在列出(GET)资源时尝试在Accept头中包含某个版本，您将收到此错误。 版本仅在尝试对单个资源执行查找请求时才是必需的。 从“接受”标题中删除版本以解决错误。