---
keywords: Experience Platform；主页；热门主题；模式;模式；枚举；混音；字段组；字段组；混合；数据类型；数据类型；数据类型；主标识；主标识；XDM个人用户档案;XDM字段；数据类型；枚举；体验事件;XDM体验事件;XDM体验事件；体验事件；体验事件；XDM Experienceevent;模式设计；类；类；类；类；数据类型；数据类型；数据类型；模式;模式；标识；标识映射；标识映射；模式设计；映射；映射；合并模式;合并
solution: Experience Platform
title: 模式合成基础
topic-legacy: overview
description: 本文档介绍了体验数据模型(XDM)模式，以及构建要在Adobe Experience Platform中使用的模式的构件、原则和最佳做法。
exl-id: d449eb01-bc60-4f5e-8d6f-ab4617878f7e
source-git-commit: 632ea4e2a94bfcad098a5fc5a5ed8985c0f41e0e
workflow-type: tm+mt
source-wordcount: '3621'
ht-degree: 0%

---

# 模式合成基础

本文档介绍[!DNL Experience Data Model](XDM)模式以及构建要在Adobe Experience Platform中使用的模式的构件、原则和最佳做法。 有关XDM及其在[!DNL Platform]中的使用方式的一般信息，请参阅[ XDM系统概述](../home.md)。

## 了解模式

模式是表示和验证数据结构和格式的一组规则。 从高度讲，模式提供了真实对象（如人）的抽象定义，并概述了该对象的每个实例（如名、姓、生日等）中应包含哪些数据。

除了描述数据的结构外，模式还对数据应用约束和期望，以便当数据在系统之间移动时验证它。 这些标准定义允许一致地解释数据，而不管来源如何，并且不需要跨应用程序进行翻译。

[!DNL Experience Platform] 使用模式保持此语义规范化。模式是描述[!DNL Experience Platform]中数据的标准方式，它允许在组织内重复使用符合模式的所有数据，而不会发生冲突，甚至在多个组织之间共享。

XDM模式是以自包含格式存储大量复杂数据的理想之选。 有关XDM如何实现此操作的详细信息，请参阅本文档附录中关于[嵌入对象](#embedded)和[大数据](#big-data)的部分。

### [!DNL Experience Platform]中基于模式的工作流

标准化是[!DNL Experience Platform]背后的一个关键概念。 由Adobe驱动的XDM旨在实现客户体验数据标准化并为客户体验管理定义标准模式。

构建[!DNL Experience Platform]的基础架构（称为[!DNL XDM System]）简化了基于模式的工作流，并包括[!DNL Schema Registry]、[!DNL Schema Editor]、模式元数据和服务消费模式。 有关详细信息，请参阅[XDM系统概述](../home.md)。

在[!DNL Experience Platform]中构建和利用模式有几个关键优势。 首先，模式允许更好地管理数据并实现数据最小化，这一点对于隐私法规尤为重要。 其次，使用Adobe的标准组件构建模式可以实现开箱即用的洞察和使用AI/ML服务，并且最少可自定义。 最后，模式为数据共享洞察和高效安排提供了基础架构。

## 规划模式

构建模式的第一步是确定您试图在模式中捕获的概念或真实对象。 一旦您确定要描述的概念，您就可以开始规划模式，考虑诸如数据类型、潜在身份域以及模式在未来可能的演变等。

### [!DNL Experience Platform]中的数据行为

用于[!DNL Experience Platform]的数据分为两种行为类型：

* **记录数据**:提供有关主题属性的信息。主题可以是组织或个人。
* **时间序列数据**:提供记录主体直接或间接采取操作时系统的快照。

所有XDM模式都描述了可以分类为记录或时间序列的数据。 模式的模式行为由的类定义，该类在首次创建模式时分配给。 本文档后面将进一步详细描述XDM类。

记录和时间序列模式都包含身份映射(`xdm:identityMap`)。 此字段包含主题的标识表示形式，它取自标为“标识”的字段（如下一节所述）。

### [!UICONTROL 身份] {#identity}

模式用于将数据引入[!DNL Experience Platform]。 此视图可跨多个服务使用，以创建单个实体的统一数据。 因此，在考虑模式时，务必考虑客户身份，以及无论数据来自何处，都可以使用哪些字段来标识主题。

为了帮助处理此过程，您的模式中的关键字段可以标记为身份。 在数据摄取时，这些字段中的数据将插入该个人的“[!UICONTROL 标识图]”中。 然后，可以通过[[!DNL Real-time Customer Profile]](../../profile/home.md)和其他[!DNL Experience Platform]服务访问图表数据，以提供每个客户的拼接视图。

通常标为“[!UICONTROL Identity]”的字段包括：电子邮件地址、电话号码、[[!DNL Experience Cloud ID (ECID)]](https://experienceleague.adobe.com/docs/id-service/using/home.html)、CRM ID或其他唯一ID字段。 您还应考虑特定于您组织的任何唯一标识符，因为它们可能也是好的“[!UICONTROL 标识]”字段。

在模式规划阶段考虑客户身份非常重要，这有助于确保将数据汇总在一起，以构建最可靠的用户档案。 请参阅[Adobe Experience Platform Identity Service](../../identity-service/home.md)的概述，进一步了解身份信息如何帮助您向客户提供数字体验。

#### `identityMap` {#identityMap}

`identityMap` 是一个映射类型字段，它描述个人的各种标识值及其关联的命名空间。此字段可用于为模式提供身份信息，而不是在模式本身的结构中定义身份值。

使用`identityMap`的主要缺点是身份会嵌入到数据中，因此变得不那么可见。 如果您要获取原始数据，则应该在实际模式结构中定义单个标识字段。

但是，如果要从存储身份的源(如[!DNL Airship]或Adobe Audience Manager)导入数据，则标识映射可能特别有用。 此外，如果您使用[Adobe Experience Platform Mobile SDK](https://aep-sdks.gitbook.io/docs/)，则需要标识映射。

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

如上例所示，`identityMap`对象中的每个键都表示标识命名空间。 每个键的值是对象的数组，表示各个命名空间的标识值(`id`)。 有关由Adobe应用程序识别的标准标识命名空间](../../identity-service/troubleshooting-guide.md#standard-namespaces)的[列表，请参阅[!DNL Identity Service]文档。

>[!NOTE]
>
>还可为每个标识值提供一个布尔值，用于确定该值是否为主标识(`primary`)。 只需为要在[!DNL Real-time Customer Profile]中使用的模式设置主标识。 有关详细信息，请参阅[合并模式](#union)中的一节。

### 模式进化原则 {#evolution}

随着数字体验的性质不断演变，用于代表数字体验的模式也必须如此。 因此，设计良好的模式能够根据需要进行调整和发展，而不会对模式的先前版本造成破坏性的变化。

由于保持向后兼容性对模式演化至关重要，[!DNL Experience Platform]强制采用纯附加的版本控制原则，以确保对模式的任何修订只会导致非破坏性的更新和更改。 也就是说，不支持&#x200B;**中断更改。**

| 支持的更改 | 中断更改（不支持） |
|------------------------------------|---------------------------------|
| <ul><li>向现有模式添加新字段</li><li>将必填字段设置为可选字段</li></ul> | <ul><li>删除以前定义的字段</li><li>引入新的必填字段</li><li>重命名或重定义现有字段</li><li>删除或限制以前支持的字段值</li><li>将属性移动到树中的其他位置</li></ul> |

>[!NOTE]
>
>如果尚未使用模式将数据收录到[!DNL Experience Platform]中，您可能会对该模式引入突破性更改。 但是，在[!DNL Platform]中使用模式后，它必须遵循附加版本控制策略。

### 模式和数据获取

要将数据收录到[!DNL Experience Platform]中，必须先创建数据集。 数据集是[[!DNL Catalog Service]](../../catalog/home.md)的数据转换和跟踪的构建块，通常表示包含摄取的数据的表或文件。 所有数据集都基于现有的XDM模式，这为摄取的数据应包含的内容及其结构提供了约束。 有关详细信息，请参阅[Adobe Experience Platform Data Ingestion](../../ingestion/home.md)的概述。

## 模式

[!DNL Experience Platform] 使用一种合成方法，在该方法中，将标准构件块组合在一起以创建模式。这种方法促进现有组件的可重用性，并推动整个行业的标准化，以支持[!DNL Platform]中的供应商模式和组件。

模式使用以下公式组成：

**类+模式字段组(&amp;A);= XDM模式**

&amp;ast;模式由类和零个或多个模式字段组组成。 这意味着您无需使用字段组即可构建数据集模式。

### 类 {#class}

编写模式从指定类开始。 类定义模式将包含的数据的行为方面（记录或时间序列）。 除此之外，类还描述了所有基于该类的模式需要包含的公共属性的最小数量，并为合并多个兼容数据集提供了一种方法。

模式的类决定哪些字段组有资格在该模式中使用。 在下一节[中将详细讨论此问题。](#field-group)

Adobe提供多个标准（“核心”）XDM类。 几乎所有下游平台进程都需要其中两个类[!DNL XDM Individual Profile]和[!DNL XDM ExperienceEvent]。 除了这些核心类，您还可以创建自己的自定义类来描述组织的更具体用例。 当没有Adobe定义的核心类可用于描述唯一用例时，自定义类由组织定义。

以下屏幕截图演示了类在平台UI中的表示方式。 由于显示的示例模式不包含任何字段组，所有显示的字段都由模式的类([!UICONTROL XDM单个用户档案])提供。

![](../images/schema-composition/class.png)

有关可用标准XDM类的最新列表，请参阅[官方XDM存储库](https://github.com/adobe/xdm/tree/master/components/classes)。 或者，如果您希望在UI中视图资源，也可以参阅[探索XDM组件](../ui/explore.md)的指南。

### 字段组{#field-group}

字段组是可重用的组件，它定义一个或多个字段，这些字段实现某些功能，如个人详细信息、酒店首选项或地址。 字段组将作为实现兼容类的模式的一部分包含。

字段组根据所表示数据（记录或时间序列）的行为定义它们与哪些类兼容。 这意味着并非所有字段组都可用于所有类。

[!DNL Experience Platform] 包括许多标准的Adobe字段组，同时允许供应商为其用户定义字段组，并允许个人用户为自己的特定概念定义字段组。

例如，要为“[!UICONTROL Loyalty Members]”模式捕获诸如“[!UICONTROL First Name]”和“[!UICONTROL Home Address]”等详细信息，您可以使用定义这些常见概念的标准字段组。 但是，特定于较不常见用例的概念(如“[!UICONTROL 忠诚度项目级别]”)通常没有预定义的字段组。 在这种情况下，您必须定义自己的字段组才能捕获此信息。

请记住，模式由“零个或更多”字段组组成，因此这意味着您无需使用任何字段组即可构建有效模式。

以下屏幕截图演示了字段组在平台UI中的显示方式。 本例中，单个字段组（[!UICONTROL 人口统计详细信息]）被添加到模式，该字段组为模式的结构提供字段分组。

![](../images/schema-composition/field-group.png)

有关可用标准XDM字段组的最新列表，请参阅[官方XDM存储库](https://github.com/adobe/xdm/tree/master/components/mixins)。 或者，如果您希望在UI中视图资源，也可以参阅[探索XDM组件](../ui/explore.md)的指南。

### 数据类型{#data-type}

数据类型与基本文本字段一样用作类或模式中的引用字段类型。 关键区别在于数据类型可以定义多个子字段。 与字段组类似，数据类型允许多字段结构的一致使用，但比字段组具有更大的灵活性，因为通过将数据类型添加为字段的“数据类型”，可以在模式的任意位置包括数据类型。

[!DNL Experience Platform] 提供许多常用数据类型，作为 [!DNL Schema Registry] 的一部分，以支持使用标准模式描述常用数据结构。这在[!DNL Schema Registry]教程中有更详细的说明，在您逐步定义数据类型时，会更加清晰。

以下屏幕截图演示了数据类型在平台UI中的表示方式。 [!UICONTROL 人口统计详细信息]字段组提供的字段之一使用“[!UICONTROL 人员名称]”数据类型，如字段名称旁的管道字符(`|`)后面的文本所指示。 此特定数据类型提供与个人姓名相关的多个子字段，此构造可重用于需要捕获个人姓名的其他字段。

![](../images/schema-composition/data-type.png)

有关可用标准XDM数据类型的最新列表，请参阅[官方XDM存储库](https://github.com/adobe/xdm/tree/master/components/datatypes)。 或者，如果您希望在UI中视图资源，也可以参阅[探索XDM组件](../ui/explore.md)的指南。

### 字段

字段是模式最基本的构建块。 字段通过定义特定数据类型提供了有关可包含的数据类型的约束。 这些基本数据类型定义单个字段，而之前提到的[数据类型](#data-type)允许您定义多个子字段，并在各种模式中重复使用相同的多字段结构。 因此，除了将字段的“数据类型”定义为注册表中定义的数据类型之一之外，[!DNL Experience Platform]还支持基本标量类型，例如：

* 字符串
* 整数
* 双精度
* 布尔值
* 数组
* 对象

>[!TIP]
>
>有关在对象类型字段上使用自由表单字段的利弊，请参阅[附录](#objects-v-freeform)。

这些标量类型的有效范围可以进一步限制为某些模式、格式、最小值/最大值或预定义值。 使用这些约束，可以表示范围更广的特定字段类型，包括：

* 枚举
* 长
* 短
* 字节
* 日期
* 日期时间
* 地图

>[!NOTE]
>
>“map”字段类型允许键值对数据，包括单个键的多个值。 映射只能在系统级别定义，这意味着您可能在行业或供应商定义的模式中遇到映射，但无法在您定义的字段中使用。 [模式注册表API开发人员指南](../api/getting-started.md)包含有关定义字段类型的详细信息。

下游服务和应用程序使用的某些数据操作对特定字段类型强制实施限制。 受影响的服务包括但不限于：

* [[!DNL Real-time Customer Profile]](../../profile/home.md)
* [[!DNL Identity Service]](../../identity-service/home.md)
* [[!DNL Segmentation]](../../segmentation/home.md)
* [[!DNL Query Service]](../../query-service/home.md)
* [[!DNL Data Science Workspace]](../../data-science-workspace/home.md)

在创建用于下游服务的模式之前，请查阅这些服务的相应文档，以便更好地了解该模式所针对的数据操作的现场要求和限制。

### XDM字段

除了基本字段和定义您自己的数据类型的能力之外，XDM还提供了一组标准字段和数据类型，这些字段和数据类型由[!DNL Experience Platform]服务隐式理解，并且当在[!DNL Platform]组件中使用时提供更高的一致性。

这些字段（如“名字”和“电子邮件地址”）包含除基本标量字段类型之外的附加含义，告知[!DNL Platform]任何共享相同XDM数据类型的字段将以相同方式行事。 无论数据来自何处，或[!DNL Platform]服务使用数据时，都可以信任此行为是一致的。

有关可用XDM字段的完整列表，请参阅[ XDM字段词典](field-dictionary.md)。 建议尽可能使用XDM字段和数据类型，以支持[!DNL Experience Platform]中的一致性和标准化。

## 合成示例

模式表示将被引入[!DNL Platform]并使用合成模型构建的数据的格式和结构。 如前所述，这些模式由一个类和与该类兼容的零个或多个字段组组成。

例如，描述在零售商店购买情况的模式可能称为“[!UICONTROL 商店交易]”。 该模式实现与标准[!UICONTROL Commerce]字段组和用户定义的[!UICONTROL 产品信息]字段组组合的[!DNL XDM ExperienceEvent]类。

跟踪网站流量的另一个模式可能称为“[!UICONTROL Web访问]”。 它还实现[!DNL XDM ExperienceEvent]类，但此次合并标准[!UICONTROL Web]字段组。

下图显示了这些模式以及每个字段组贡献的字段。 它还包含两个基于[!DNL XDM Individual Profile]类的模式，包括本指南中前面提到的“[!UICONTROL 忠诚会员]”模式。

![](../images/schema-composition/composition.png)

### Union {#union}

[!DNL Experience Platform]允许您为特定用例编写模式，但它还允许您看到特定类类型的模式的“合并”。 上图显示了两个基于XDM ExperienceEvent类的模式和两个基于[!DNL XDM Individual Profile]类的模式。 合并（如下所示）将聚合共享同一类的所有模式的字段（分别为[!DNL XDM ExperienceEvent]和[!DNL XDM Individual Profile]）。

![](../images/schema-composition/union.png)

通过启用与[!DNL Real-time Customer Profile]一起使用的模式，该合并将包含在该类型的类中。 [!DNL Profile] 提供强大、集中的用户档案客户属性，以及客户在与之集成的任何系统中拥有的每个事件的加盖时间戳的帐 [!DNL Platform]户。[!DNL Profile] 使用合并视图来表示此数据，并为每位客户提供整体视图。

有关使用[!DNL Profile]的详细信息，请参阅[实时客户用户档案概述](../../profile/home.md)。

## 将数据文件映射到XDM模式

所有被收录到[!DNL Experience Platform]中的数据文件都必须符合XDM模式的结构。 有关如何格式化数据文件以符合XDM层次（包括示例文件）的详细信息，请参阅[示例ETL转换](../../etl/transformations.md)上的文档。 有关将数据文件收录到[!DNL Experience Platform]的一般信息，请参阅[批处理摄取概述](../../ingestion/batch-ingestion/overview.md)。

## 模式外部区段

如果要将来自外部系统的细分引入平台，则必须使用以下组件在您的模式中捕获这些细分：

* [[!UICONTROL 区段] 定义类](../classes/segment-definition.md):使用此标准类捕获外部区段定义的关键属性。
* [[!UICONTROL 区段成员] 资格Detailsfield组](../field-groups/profile/segmentation.md):将此字段组添加到您的XDM [!UICONTROL 单个概] 要文件架构，以便将客户用户档案与特定区段关联。

## 后续步骤

现在，您已经了解了模式合成的基础知识，现在，您可以开始使用[!DNL Schema Registry]探索和构建模式。

要查看两个核心XDM类及其常用的兼容字段组的结构，请参阅以下参考文档：

* [[!DNL XDM Individual Profile]](../classes/individual-profile.md)
* [[!DNL XDM ExperienceEvent]](../classes/experienceevent.md)

[!DNL Schema Registry]用于访问Adobe Experience Platform中的[!DNL Schema Library]，并提供可从中访问所有可用库资源的用户界面和RESTful API。 [!DNL Schema Library]包含由Adobe定义的行业资源、由[!DNL Experience Platform]合作伙伴定义的供应商资源以及由组织成员组成的类、字段组、数据类型和模式。

要开始使用UI编写模式，请配合[模式编辑器教程](../tutorials/create-schema-ui.md)，构建本文档中提到的“忠诚会员”模式。

要开始使用[!DNL Schema Registry] API，请阅读[模式注册表API开发人员指南](../api/getting-started.md)进行开始。 阅读开发人员指南后，请按照教程中概述的步骤操作，该教程位于[中，使用模式 Registry API](../tutorials/create-schema-api.md)创建模式。

## 附录

以下各节载有关于模式组成原则的补充资料。

### 关系表与嵌入式对象 {#embedded}

使用关系数据库时，最佳实践是标准化数据，或将实体划分为离散部分，然后在多个表中显示。 为了将数据作为一个整体读取或更新实体，必须使用JOIN对多个单独的表执行读写操作。

通过使用嵌入式对象，XDM模式可以直接表示复杂的数据并将其存储在具有分层结构的自包含文档中。 此结构的主要优点之一是，它允许您查询数据，而无需通过昂贵的连接到多个非规范表来重建实体。 您的模式层次结构的级别没有硬性限制。

### 模式和大数据{#big-data}

现代数字系统产生大量的行为信号（交易数据、网络日志、物联网、显示等）。 这些大数据优惠了优化体验的绝佳机会，但由于数据的规模和多样性，使用这些数据极具挑战。 为了从数据中获得价值，其结构、格式和定义必须标准化，以便能够一致、高效地处理数据。

模式通过允许从多个来源整合数据、通过共同结构和定义标准化并跨解决方案共享数据来解决这一问题。 这允许后续过程和服务回答任何类型的数据问题，从传统的数据建模方法转向数据建模方法，在这种方法中，将要询问数据的所有问题都预先知道，并且数据建模以符合这些期望。

### 对象与自由格式字段{#objects-v-freeform}

在设计模式时，在自由格式字段上选择对象时，需要考虑一些关键因素：

| 对象 | 自由格式字段 |
| --- | --- |
| 增加嵌套 | 嵌套更少或没有 |
| 创建逻辑字段组 | 字段被放置在临时位置 |

#### 对象

在自由表单域上使用对象的利弊如下。

**专业人士**:

* 当您希望创建特定字段的逻辑分组时，最好使用对象。
* 对象以更结构化的方式组织模式。
* 对象间接有助于在区段生成器用户界面中创建良好的菜单结构。 模式中的分组字段会直接反映在区段生成器用户界面中提供的文件夹结构中。

**缺点**:

* 字段会变得更加嵌套。
* 当使用[Adobe Experience Platform 查询服务](../../query-service/home.md)时，必须为嵌套在对象中的查询字段提供较长的引用字符串。

#### 自由格式字段

在对象上使用自由表单字段的利弊如下。

**专业人士**:

* 自由表单字段直接在模式的根对象下创建(`_tenantId`)，从而提高了可见性。
* 使用查询服务时，自由表单字段的引用字符串往往更短。

**缺点**:

* 模式中自由表单字段的位置是临时的，这意味着这些字段在模式编辑器中以字母顺序显示。 这可能会使模式的结构变得不那么复杂，类似的自由表单字段最终可能会因名称而分离得很远。
