---
keywords: Experience Platform;home;popular topics;schema;Schema;enum;mixin;Mixin;Mixins;mixins;data type;data types;Data types;Data type;primary identity;primary idenity;XDM individual profile;XDM fields;enum datatype;Experience event;XDM Experience Event;XDM ExperienceEvent;experienceEvent;experienceevent;XDM Experienceevenet;schema design;class;Class;classes;Classes;datatype;Datatype;data type;Data type;schemas;Schemas;identityMap;identity map;Identity map;Schema design;map;Map;union schema;union
solution: Experience Platform
title: 模式合成基础
topic: overview
description: 本文档介绍了体验数据模型(XDM)模式，以及构成要在Adobe Experience Platform使用的模式的构件、原则和最佳做法。
translation-type: tm+mt
source-git-commit: f7abccb677294e1595fb35c27e03c30eb968082a
workflow-type: tm+mt
source-wordcount: '2839'
ht-degree: 0%

---


# 模式合成基础

本文档介绍(XDM) [!DNL Experience Data Model] 模式，以及构成将在Adobe Experience Platform使用的模式的构件、原则和最佳做法。 有关XDM及其使用方式的一般信息， [!DNL Platform]请参阅XDM [系统概述](../home.md)。

## 了解模式

模式是表示和验证数据结构和格式的一组规则。 从高度讲，模式提供了真实对象（如人）的抽象定义，并勾勒出该对象的每个实例（如名、姓、生日等）中应包含哪些数据。

除了描述数据结构外，模式还对数据应用约束和期望，这样当数据在系统之间移动时，就可以验证数据。 这些标准定义允许一致地解释数据，而不管来源如何，并且无需跨应用程序进行翻译。

[!DNL Experience Platform] 通过使用模式来保持这种语义规范化。 模式是描述中数据的标准方法，它允 [!DNL Experience Platform]许所有符合模式的数据可重复使用，而不会在组织内发生冲突，甚至可以在多个组织之间共享。

### 关系表与嵌入式对象

在使用关系数据库时，最佳实践包括将数据标准化，或将实体划分为离散部分，然后在多个表中显示。 为了将数据作为一个整体读取或更新实体，必须使用JOIN对多个单独的表执行读写操作。

XDM模式通过嵌入式对象的使用，可以直接表示复杂的数据并存储在具有分层结构的自包含文档中。 此结构的主要优点之一是它允许您查询数据，而无需通过昂贵的连接到多个非规范化表来重建实体。

### 模式和大数据

现代数字系统产生大量行为信号（交易数据、网络日志、物联网、显示等）。 这些大数据优惠了优化体验的绝佳机会，但由于数据的规模和种类，使用起来极具挑战。 为了从数据中获得价值，必须对其结构、格式和定义进行标准化，以便能够一致、高效地处理数据。

模式通过允许从多个来源集成数据、通过通用结构和定义进行标准化并跨解决方案共享数据来解决这一问题。 这允许后续过程和服务回答任何类型的数据问题，从传统的数据建模方法转向数据建模方法，在该方法中，将要询问数据的所有问题都预先知道，并且数据被建模以符合这些期望。

### 模式工作流 [!DNL Experience Platform]

标准化是背后的一个关键概念 [!DNL Experience Platform]。 XDM由Adobe驱动，旨在实现客户体验数据标准化并为客户体验管理定义标准模式。

所构建的基 [!DNL Experience Platform] 础结构( [!DNL XDM System]称为模式)方便了基于的工作流，并包括 [!DNL Schema Registry]、 [!DNL Schema Editor]模式元数据和服务消耗模式。 See the [XDM System overview](../home.md) for more information.

## 规划模式

构建模式的第一步是确定您试图在模式中捕获的概念或真实对象。 一旦您确定了要描述的概念，您就可以开始规划模式，思考诸如数据类型、潜在身份域以及模式在未来的演变。

### 数据行为 [!DNL Experience Platform]

计划用于的数据 [!DNL Experience Platform] 分为两种行为类型：

* **记录数据**:提供有关主题属性的信息。 主题可以是组织或个人。
* **时间序列数据**:提供记录主体直接或间接采取操作时系统的快照。

所有XDM模式都描述可以分类为记录或时间序列的数据。 模式的行为由模式的类定 **义**，该类在模式首次创建时分配给。 本文档后面对XDM类进行了更详细的介绍。

记录和时间序列模式都包含身份映射(`xdm:identityMap`)。 此字段包含主题的标识表示形式，该表示形式取自标为“标识”的字段，如下一节所述。

### [!UICONTROL 身份] {#identity}

模式用于将数据引入 [!DNL Experience Platform]。 此视图可跨多个服务使用，以创建单个实体的单一统一数据。 因此，考虑模式时，必须考虑客户身份以及哪些字段可用于识别主题，无论数据来自何处。

为了帮助处理此过程，您的模式中的关键字段可以标记为身份。 在获取数据时，这些字段中的数据将插入该个[!UICONTROL 人的]“身份图”中。 然后，[!DNL实时客户用户档案] [和其他服务可以访问图表](../../profile/home.md) , [!DNL Experience Platform] 以为每个单独的客户提供拼接视图。

通常标为“Identity”的[!UICONTROL 字段]包括：电子邮件地址、电 [话号码、[!DNLExperience CloudID(ECID)]](https://docs.adobe.com/content/help/zh-Hans/id-service/using/home.html)、CRM ID或其他唯一ID字段。 您还应考虑特定于您组织的所有唯一标识符，因为它们可能也是[!UICONTROL 好的]“身份”字段。

在模式规划阶段考虑客户身份非常重要，这有助于确保整合数据以构建尽可能最可靠的用户档案。 请参阅Adobe Experience Platform [身份服务概述](../../identity-service/home.md) ，进一步了解身份信息如何帮助您向客户提供数字体验。

#### xdm:identityMap {#identityMap}

`xdm:identityMap` 是一个映射类型字段，它描述个人的各种身份值及其关联命名空间。 此字段可用于为模式提供身份信息，而不是在模式本身的结构中定义身份值。

简单标识映射的示例如下所示：

```json
"identityMap": {
  "email": [
    {
      "id": "jsmith@example.com",
      "primary": false
    }
  ],
  "ECID": [
    {
      "id": "87098882279810196101440938110216748923",
      "primary": false
    },
    {
      "id": "55019962992006103186215643814973128178",
      "primary": false
    }
  ],
  "loyaltyId": [
    {
      "id": "2e33192000007456-0365c00000000000",
      "primary": true
    }
  ]
}
```

如上例所示，对象中的每个键都 `identityMap` 表示一个身份命名空间。 每个键的值是对象的数组，表示各个命名空间的`id`标识值()。 有关列表标 [!DNL Identity Service] 识命名空间的 [，请参阅文档](../../identity-service/troubleshooting-guide.md#standard-namespaces) ，该标识由Adobe应用程序识别。

>[!NOTE]
>
>还可以为每个标识值提供一个布尔值，用于`primary`该值是否是主标识()。 只需为要用于的模式设置主标识 [!DNL Real-time Customer Profile]。 有关详细信息，请 [参阅合并](#union) 模式一节。

### 模式进化原则 {#evolution}

随着数字体验的性质不断发展，用来代表数字体验的模式也必须如此。 因此，设计良好的模式能够根据需要进行调整和发展，而不会对模式的先前版本造成破坏性的改变。

由于保持向后兼容性对模式发展至关重要，因此 [!DNL Experience Platform] 应实施纯粹的附加版本控制原则，以确保对模式的任何修订只会导致无损的更新和更改。 换言之，不 **支持中断更改。**

| 支持的更改 | 中断更改（不支持） |
|------------------------------------|---------------------------------|
| <ul><li>向现有模式添加新字段</li><li>使必填字段成为可选字段</li></ul> | <ul><li>删除以前定义的字段</li><li>引入新的必填字段</li><li>重命名或重定义现有字段</li><li>删除或限制以前支持的字段值</li><li>将属性移动到树中的其他位置</li></ul> |

>[!NOTE]
>
>如果模式尚未用于将数据引入， [!DNL Experience Platform]您可能会对该模式引入突破性的更改。 但是，一旦在中使用了模式, [!DNL Platform]它就必须遵守附加的版本控制策略。

### 模式和数据获取

为了将数据引入， [!DNL Experience Platform]必须先创建数据集。 数据集是[!DNL Catalog Service]的数据转 [换和跟踪的构建块](../../catalog/home.md)，通常表示包含所摄取数据的表或文件。 所有数据集都基于现有的XDM模式，它们为所摄取的数据应包含的内容以及如何构建提供约束。 有关更多信息， [请参阅Adobe Experience Platform](../../ingestion/home.md) 数据摄取概述。

## 模式积木

[!DNL Experience Platform] 使用一种合成方法，其中将标准构件块组合在一起以创建模式。 这种方法促进了现有组件的可重用性，并推动整个行业的标准化，以支持中的供应商模式和组件 [!DNL Platform]。

模式使用以下公式组成：

**类+ Mixin&amp;ast;= XDM模式**

&amp;ast;模式由类和零个或多 _个混音组成_ 。 这意味着您可以构建数据集模式，而完全不使用mixin。

### 类

编写模式从指定类开始。 类定义模式将包含的数据的行为方面（记录或时间序列）。 除此之外，类还描述了所有基于该类的模式需要包含的最小公共属性数，并为合并多个兼容数据集提供了一种方法。

类还决定哪些混音符合在模式中使用的条件。 下面的mixin部分将更详细 [地讨论](#mixin) 此问题。

每次集成都提供标准类， [!DNL Experience Platform]称为“行业”类。 行业类别是公认的行业标准，适用于各种使用案例。 行业类的示例包括 [!DNL XDM Individual Profile] Adobe [!DNL XDM ExperienceEvent] 提供的类和类。

[!DNL Experience Platform] 还允许“供应商”类，这些类是合作伙伴定义的类， [!DNL Experience Platform] 并提供给所有使用该供应商服务或应用程序的客户 [!DNL Platform]。

还有一些类用于描述内部单个组织的更具体的用 [!DNL Platform]例，称为“客户”类。 当没有可用于描述唯一用例的行业或供应商类时，客户类由组织定义。

例如，代表“忠诚度”项目成员的模式描述了有关个人的记录数据，因此可以基于该类(由Adobe定义的 [!DNL XDM Individual Profile] 标准“行业”类)。

### Mixin {#mixin}

混音是可重用的组件，它定义一个或多个字段，这些字段实现某些功能，如个人详细信息、酒店偏好或地址。 混合被设计为实现兼容类的模式的一部分。

混音根据所表示数据（记录或时间序列）的行为定义它们与哪些类兼容。 这意味着并非所有混音都可用于所有类。

混合的范围和定义与类相同：行业混合、供应商混合和客户混合由使用的单个组织定义 [!DNL Platform]。 [!DNL Experience Platform] 包括许多标准的行业混合，同时允许供应商为其用户定义混合，并允许个别用户为自己的特定概念定义混合。

例如，要为“忠诚会员[!UICONTROL ”模式捕获]“名字”和“家庭地址[!UICONTROL ”等详细信息，]您将能够使用定义这些常见概念的标准混音。 但是，特定于不常用用例的概念(如“[!UICONTROL 忠诚度项目级]”)通常没有预定义的混音。 在这种情况下，您必须定义自己的混音来捕获此信息。

请记住，模式由“零个或更多”混音组成，因此这意味着您无需使用任何混音即可构建有效的模式。

### Data type {#data-type}

数据类型在类或模式中用作引用字段类型的方式与基本文本字段相同。 关键区别在于数据类型可以定义多个子字段。 与混音类似，数据类型允许多字段结构的一致使用，但比混音具有更大的灵活性，因为通过将数据类型添加为字段的“模式类型”，可以在的任意位置包含数据类型。

[!DNL Experience Platform] 提供许多常用数据类型作为标准数据类型的一 [!DNL Schema Registry] 部分，以支持使用标准模式描述常用数据结构。 这在教程中有更详细的 [!DNL Schema Registry] 说明，当您逐步定义数据类型时，它将变得更加清晰。

### 字段

字段是模式最基本的构件。 字段通过定义特定数据类型提供与它们可以包含的数据类型相关的约束。 这些基本数据类型定义单个字段，而 [前面提到的数据类](#data-type) 型，允许您定义多个子字段，并在各种模式中重复使用相同的多字段结构。 因此，除了将字段的“数据类型”定义为注册表中定义的数据类型之一外，还支持基 [!DNL Experience Platform] 本标量类型，如：

* 字符串
* 整数
* 双精度
* 布尔值
* 阵列
* 对象

这些标量类型的有效范围可以进一步限制为某些模式、格式、最小值／最大值或预定义值。 使用这些约束，可以表示各种更具体的字段类型，包括：

* 枚举
* 长
* 短
* 字节
* 日期
* 日期时间
* 地图

>[!NOTE]
>
>“映射”字段类型允许键值对数据，包括单个键的多个值。 映射只能在系统级别定义，这意味着您可能在行业或供应商定义的模式中遇到映射，但该映射不能用于您定义的字段。 模式 [注册表API开发人员指南](../api/getting-started.md) ，包含有关定义字段类型的更多信息。

下游服务和应用程序使用的某些数据操作对特定字段类型强制实施限制。 受影响的服务包括但不限于：

* [[!DNL实时客户用户档案]](../../profile/home.md)
* [[!DNL Identity Service]](../../identity-service/home.md)
* [[!DNL分段]](../../segmentation/home.md)
* [[!DNL查询服务]](../../query-service/home.md)
* [[!DNL数据科学工作区]](../../data-science-workspace/home.md)

在创建用于下游服务的模式之前，请查看这些服务的相应文档，以便更好地了解该模式所针对的数据操作的现场要求和限制。

### XDM字段

除了基本字段和定义您自己的数据类型的能力之外，XDM还提供标准的字段和数据类型集，这些字段和数据类型由服务隐含地理解，并在跨组件使 [!DNL Experience Platform] 用时提供更高的一 [!DNL Platform] 致性。

这些字段（如“名字”和“电子邮件地址”）包含除基本标量字段类型之外的附加含义，告 [!DNL Platform] 诉任何共享相同XDM数据类型的字段都将以相同的方式行事。 无论数据来自何处或使用数据的服务在何处，都可以信任此行为 [!DNL Platform] 保持一致。

有关可 [用XDM字段的完整列表](field-dictionary.md) ，请参阅XDM字段字典。 建议尽可能使用XDM字段和数据类型，以支持跨平台的一致性和标准化 [!DNL Experience Platform]。

## 合成示例

模式表示要引入的数据的格式和结构，并 [!DNL Platform]使用合成模型构建。 如前所述，这些模式由类和与该类兼容的零个或多个混音组成。

例如，描述在零售商店购买的模式可能称为“商[!UICONTROL 店交易]”。 模式实现 [!DNL XDM ExperienceEvent] 与标准Commerce [!UICONTROL mixin和用户定义的Product] Info  mixin组合的类。

另一个跟踪网站流量的模式可称[!UICONTROL 为“Web访]问”。 它还实现了 [!DNL XDM ExperienceEvent] 类，但这次是将标准Web [!UICONTROL 混合] 。

下图显示了这些模式以及每个混音贡献的字段。 它还包含两个基于课堂的模式 [!DNL XDM Individual Profile] ，包括本指南中[!UICONTROL 前面提到的]“忠诚会员”模式。

![](../images/schema-composition/composition.png)

### Union {#union}

您 [!DNL Experience Platform] 可以为特定用例编写模式，也可以查看特定类类型的模式的“合并”。 上图显示了两个基于XDM ExperienceEvent类的模式和两个基于类的 [!DNL XDM Individual Profile] 模式。 合并，如下所示，聚合共享同一类的所有模式的字段([!DNL XDM ExperienceEvent] 和 [!DNL XDM Individual Profile]分别)。

![](../images/schema-composition/union.png)

通过启用模式与 [!DNL Real-time Customer Profile]一起使用，它将包含在该类型的合并中。 [!DNL Profile] 提供强大、集中的用户档案客户属性，以及客户在与之集成的任何系统中拥有的每个事件的加盖时间戳的帐户 [!DNL Platform]。 [!DNL Profile] 使用合并视图来表示此数据，并为每位客户提供整体视图。

有关使用的更多信 [!DNL Profile]息，请参 [阅实时客户用户档案概述](../../profile/home.md)。

## 将数据文件映射到XDM模式

所有被引入的数 [!DNL Experience Platform] 据文件都必须符合XDM模式的结构。 有关如何格式化数据文件以符合XDM层次（包括示例文件）的更多信息，请参阅示例ETL [转换文档](../../etl/transformations.md)。 有关将数据文件引入的一般信 [!DNL Experience Platform]息，请参 [阅批处理概述](../../ingestion/batch-ingestion/overview.md)。

## 后续步骤

现在，您已经了解了模式合成的基础知识，可以开始使用构建模式 [!DNL Schema Registry]。

该 [!DNL Schema Registry] 应用程序用于访问Adobe Experience Platform [!DNL Schema Library] 内的库，并提供一个用户界面和RESTful API，可从中访问所有可用的库资源。 它包 [!DNL Schema Library] 含由Adobe定义的行业资源、由合作伙伴定 [!DNL Experience Platform] 义的供应商资源以及由您的组织成员组成的类、混合、数据类型和模式。

要开始使用UI编写模式，请按照模式编 [辑器教程](../tutorials/create-schema-ui.md) ，构建本文档中提到的“忠诚会员”模式。

要开始使用 [!DNL Schema Registry] API，请阅读开始注册 [表API开发人员指南](../api/getting-started.md)。 阅读开发人员指南后，请按照教程中概述的步 [骤使用模式注册表API创建模式](../tutorials/create-schema-api.md)。