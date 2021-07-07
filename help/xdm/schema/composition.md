---
keywords: Experience Platform；主页；热门主题；架构；架构；枚举；混合；字段组；字段组；数据类型；数据类型；数据类型；数据类型；数据类型；数据类型；主标识；XDM个人配置文件；XDM字段；数据类型；数据类型；体验事件；XDM体验事件；experienceevent;experienceevent;XDM Experienceevent；架构；设计；类；类；类；类；数据类型；数据类型；数据类型；数据类型；架构；标识映射；架构架构设计；映射；图；并集架构；并集
solution: Experience Platform
title: 架构组合的基础知识
topic-legacy: overview
description: 本文档介绍了Experience Data Model(XDM)架构，以及构建架构以在Adobe Experience Platform中使用的构建基块、原则和最佳实践。
exl-id: d449eb01-bc60-4f5e-8d6f-ab4617878f7e
source-git-commit: 7d05b5d57ec4597b168be0261e75da5f243cb660
workflow-type: tm+mt
source-wordcount: '3629'
ht-degree: 0%

---

# 架构组合的基础知识

本文档介绍[!DNL Experience Data Model](XDM)架构以及组合架构在Adobe Experience Platform中使用的构建基块、原则和最佳实践。 有关XDM及其在[!DNL Platform]中的使用方式的一般信息，请参阅[XDM系统概述](../home.md)。

## 了解模式

架构是一组规则，用于表示和验证数据的结构和格式。 在高级别上，架构提供了真实世界对象（如人）的抽象定义，并概述了该对象的每个实例中应包含哪些数据（如名字、姓氏、生日等）。

除了描述数据结构之外，架构还对数据应用约束和期望，这样当数据在系统之间移动时，便可对其进行验证。 这些标准定义允许对数据进行一致的解释（无论其来源如何），并且无需跨应用程序进行翻译。

[!DNL Experience Platform] 使用模式维护此语义标准化。架构是描述[!DNL Experience Platform]中数据的标准方式，它允许符合架构的所有数据在组织之间重复使用，而不会发生冲突，甚至在多个组织之间共享。

XDM模式非常适合以自包含格式存储大量复杂数据。 有关XDM如何完成此操作的详细信息，请参阅本文档附录中关于[嵌入对象](#embedded)和[大数据](#big-data)的部分。

### [!DNL Experience Platform]中基于架构的工作流

标准化是[!DNL Experience Platform]背后的一个关键概念。 XDM在Adobe的驱动下，致力于标准化客户体验数据并定义客户体验管理的标准架构。

构建[!DNL Experience Platform]的基础架构（称为[!DNL XDM System]）有助于基于架构的工作流，并包括[!DNL Schema Registry]、[!DNL Schema Editor]、架构元数据和服务使用模式。 有关更多信息，请参阅[XDM系统概述](../home.md)。

利用[!DNL Experience Platform]中的模式具有以下几个主要优势。 首先，架构允许更好地管理数据并将数据最小化，这对于隐私法规尤为重要。 其次，使用Adobe的标准组件构建架构允许开箱即用的分析和使用AI/ML服务，并且只需极少的自定义。 最后，架构为数据共享分析和高效编排提供了基础架构。

## 规划架构

构建架构的第一步是确定您尝试在架构中捕获的概念或真实世界对象。 确定您尝试描述的概念后，您可以开始通过考虑数据类型、潜在身份字段以及架构将来可能如何演变等内容来规划您的架构。

### [!DNL Experience Platform]中的数据行为

要在[!DNL Experience Platform]中使用的数据分为两种行为类型：

* **记录数据**:提供有关主题属性的信息。主题可以是组织或个人。
* **时间系列数据**:提供记录主体直接或间接执行某项操作时系统的快照。

所有XDM架构都描述了可以分类为记录或时间序列的数据。 架构的数据行为由架构的类定义，该类在首次创建架构时分配给架构。 本文档后面将进一步详细描述XDM类。

记录架构和时序架构都包含标识映射(`xdm:identityMap`)。 此字段包含主题的标识表示形式，从标记为“标识”的字段中提取，如下一节中所述。

### [!UICONTROL 身份] {#identity}

架构用于将数据摄取到[!DNL Experience Platform]中。 此数据可跨多项服务使用，以创建单个实体的单个统一视图。 因此，在考虑架构时，请务必考虑客户身份以及哪些字段可用于标识主题，而不管数据来自何处。

为了帮助完成此过程，可以将架构中的关键字段标记为标识。 在摄取数据时，这些字段中的数据会插入到该个人的“[!UICONTROL 身份图]”中。 然后，[[!DNL Real-time Customer Profile]](../../profile/home.md)和其他[!DNL Experience Platform]服务可以访问图形数据，以提供每个客户的拼合视图。

通常标记为“[!UICONTROL Identity]”的字段包括：电子邮件地址、电话号码、[[!DNL Experience Cloud ID (ECID)]](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=zh-Hans)、CRM ID或其他唯一ID字段。 您还应考虑特定于贵组织的任何唯一标识符，因为它们可能也是良好的“[!UICONTROL Identity]”字段。

在架构规划阶段考虑客户身份非常重要，以帮助确保将数据汇总在一起，构建尽可能最可靠的配置文件。 请参阅[Adobe Experience Platform Identity Service](../../identity-service/home.md)上的概述，了解有关身份信息如何帮助您向客户交付数字体验的更多信息。

可通过两种方式将身份数据发送到Platform:

1. 通过[架构编辑器UI](../ui/fields/identity.md)或使用[架构注册表API](../api/descriptors.md#create)向单个字段添加标识描述符
1. 使用[`identityMap`字段](#identityMap)

#### `identityMap` {#identityMap}

`identityMap` 是一个映射类型字段，用于描述个人的各种身份值及其关联的命名空间。此字段可用于为架构提供标识信息，而不是在架构本身的结构中定义标识值。

使用`identityMap`的主要缺点是身份会嵌入到数据中，并因此变得不那么可见。 如果要摄取原始数据，则应该在实际架构结构中定义单个标识字段。 使用`identityMap`的架构也无法参与关系。

但是，如果您要从存储身份的源(例如[!DNL Airship]或Adobe Audience Manager)中导入数据，或者架构的标识数量存在变量，则身份映射会特别有用。 此外，如果您使用的是[Adobe Experience Platform Mobile SDK](https://aep-sdks.gitbook.io/docs/)，则需要身份映射。

简单身份映射的示例如下所示：

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

如上例所示，`identityMap`对象中的每个键都表示标识命名空间。 每个键的值是对象数组，表示各个命名空间的标识值(`id`)。 请参阅[!DNL Identity Service]文档，获取由Adobe应用程序识别的标准身份命名空间](../../identity-service/troubleshooting-guide.md#standard-namespaces)列表。[

>[!NOTE]
>
>还可以为每个标识值提供一个布尔值，用于确定值是否为主标识(`primary`)。 只需为要在[!DNL Real-time Customer Profile]中使用的架构设置主标识。 有关更多信息，请参阅[并集架构](#union)中的部分。

### 模式演化原则 {#evolution}

随着数字体验的性质不断发展，用于表示这些体验的模式也必须不断改变。 因此，经过精心设计的架构能够根据需要进行调整和演变，而不会对架构的先前版本造成破坏性的更改。

由于保持向后兼容性对于模式演变至关重要，因此[!DNL Experience Platform]强制采用纯加性版本控制原则。 此原则可确保架构的任何修订都只会导致无损的更新和更改。 换言之，不支持&#x200B;**中断更改。**

>[!NOTE]
>
>如果某个架构尚未用于将数据摄取到[!DNL Experience Platform]中，并且尚未启用以在实时客户资料中使用，则可能会对该架构进行重大更改。 但是，在[!DNL Platform]中使用架构后，它必须遵循附加版本控制策略。

下表分析了编辑架构、字段组和数据类型时支持哪些更改：

| 支持的更改 | 中断更改（不支持） |
| --- | --- |
| <ul><li>向资源添加新字段</li><li>使必填字段为可选字段</li><li>更改资源的显示名称和描述</li><li>启用架构以参与用户档案</li></ul> | <ul><li>删除以前定义的字段</li><li>引入新的必填字段</li><li>重命名或重定义现有字段</li><li>删除或限制以前支持的字段值</li><li>将现有字段移动到树中的其他位置</li><li>删除架构</li><li>禁用架构以阻止其参与用户档案</li></ul> |

### 模式和数据摄取

要将数据摄取到[!DNL Experience Platform]中，必须首先创建数据集。 数据集是[[!DNL Catalog Service]](../../catalog/home.md)的数据转换和跟踪的构建块，通常表示包含摄取数据的表或文件。 所有数据集都基于现有的XDM架构，该架构为摄取的数据应包含的内容以及其结构方式提供了约束。 有关更多信息，请参阅[Adobe Experience Platform数据摄取](../../ingestion/home.md)的概述。

## 架构的构建基块

[!DNL Experience Platform] 使用组合方法，其中标准构建块被组合以创建模式。这种方法可促进现有组件的可重用性，并推动整个行业的标准化，以支持[!DNL Platform]中的供应商模式和组件。

架构使用以下公式组成：

**类+架构字段组(&amp;A);= XDM架构**

&amp;ast；架构由类和零个或多个架构字段组组成。 这意味着您无需使用字段组即可构建数据集架构。

### 类 {#class}

从分配类开始合成架构。 类定义架构将包含的数据的行为方面（记录或时间系列）。 除此之外，类还描述了所有基于该类的架构需要包含的公共属性的最小数量，并为合并多个兼容数据集提供了一种方法。

架构的类确定哪些字段组有资格在该架构中使用。 在[下一节](#field-group)中将更详细地讨论此问题。

Adobe提供了多个标准（“核心”）XDM类。 几乎所有下游平台进程都需要其中两个类，即[!DNL XDM Individual Profile]和[!DNL XDM ExperienceEvent]。 除了这些核心类之外，您还可以创建自己的自定义类，以描述贵组织的更具体用例。 当没有Adobe定义的核心类可用于描述唯一用例时，自定义类由组织定义。

以下屏幕截图演示了类在平台UI中的显示方式。 由于显示的示例架构不包含任何字段组，因此所有显示的字段都由架构的类([!UICONTROL XDM Individual Profile])提供。

![](../images/schema-composition/class.png)

有关可用标准XDM类的最新列表，请参阅[官方XDM存储库](https://github.com/adobe/xdm/tree/master/components/classes)。 或者，如果您希望在UI中查看资源，请参阅[探索XDM组件](../ui/explore.md)上的指南。

### 字段组 {#field-group}

字段组是可重用的组件，它定义一个或多个字段，以实现某些功能，如个人详细信息、酒店首选项或地址。 字段组将作为实现兼容类的架构的一部分包含在内。

字段组根据所表示数据（记录或时间序列）的行为，定义与哪些类兼容。 这意味着并非所有字段组都可用于所有类。

[!DNL Experience Platform] 包括许多标准的Adobe字段组，同时允许供应商为其用户定义字段组，而个人用户则为自己的特定概念定义字段组。

例如，要为“[!UICONTROL 忠诚会员]”架构捕获详细信息，如“[!UICONTROL 名字]”和“[!UICONTROL 家庭地址]”，您将能够使用定义这些常见概念的标准字段组。 但是，特定于不太常见用例的概念（例如“[!UICONTROL 忠诚度计划级别]”）通常没有预定义字段组。 在这种情况下，您必须定义自己的字段组才能捕获此信息。

>[!NOTE]
>
>强烈建议您尽可能在架构中使用标准字段组，因为[!DNL Experience Platform]服务会隐式理解这些字段，并在[!DNL Platform]组件中使用时提供更高的一致性。
>
>标准组件提供的字段（如“名字”和“电子邮件地址”）包含基本标量字段类型以外的附加含义，告诉[!DNL Platform]共享相同数据类型的任何字段都将以相同的方式行事。 无论数据来自何处，或[!DNL Platform]服务中使用数据，都可以相信此行为保持一致。

请记住，架构由“零个或更多”字段组组成，这意味着您无需使用任何字段组即可构建有效架构。

以下屏幕截图演示了字段组在平台UI中的显示方式。 将单个字段组（[!UICONTROL 人口统计详细信息]）添加到此示例中的架构，该架构为架构的结构提供了字段分组。

![](../images/schema-composition/field-group.png)

有关可用标准XDM字段组的最新列表，请参阅[官方XDM存储库](https://github.com/adobe/xdm/tree/master/components/fieldgroups)。 或者，如果您希望在UI中查看资源，请参阅[探索XDM组件](../ui/explore.md)上的指南。

### 数据类型 {#data-type}

数据类型在类或架构中用作引用字段类型，其方式与基本文字字段相同。 关键区别在于数据类型可以定义多个子字段。 与字段组类似，数据类型允许一致地使用多字段结构，但比字段组具有更大的灵活性，因为通过将数据类型添加为字段的“数据类型”，数据类型可以包含在架构中的任意位置。

[!DNL Experience Platform] 在中提供许多常见数据类型，以 [!DNL Schema Registry] 支持使用标准模式描述常用数据结构。[!DNL Schema Registry]教程中对此进行了更详细的说明，在您逐步完成定义数据类型的步骤时，该教程会变得更加清晰。

以下屏幕截图演示了数据类型在平台UI中的显示方式。 [!UICONTROL 人口统计详细信息]字段组提供的其中一个字段使用“[!UICONTROL 人员名称]”数据类型，如字段名称旁边的竖线字符(`|`)后面的文本所示。 此特定数据类型提供了与个人姓名相关的多个子字段，该结构可重复使用于需要捕获人员姓名的其他字段。

![](../images/schema-composition/data-type.png)

有关可用标准XDM数据类型的最新列表，请参阅[官方XDM存储库](https://github.com/adobe/xdm/tree/master/components/datatypes)。 或者，如果您希望在UI中查看资源，请参阅[探索XDM组件](../ui/explore.md)上的指南。

### 字段

字段是架构的最基本构建块。 字段通过定义特定数据类型来对其可以包含的数据类型提供约束。 这些基本数据类型定义单个字段，而之前提到的[数据类型](#data-type)允许您定义多个子字段，并在各种架构中重复使用相同的多字段结构。 因此，除了将字段的“数据类型”定义为注册表中定义的数据类型之一外，[!DNL Experience Platform]还支持基本标量类型，例如：

* 字符串
* 整数
* 双精度
* 布尔值
* 数组
* 对象

>[!TIP]
>
>有关在对象类型字段上使用自由格式字段的利弊，请参阅[附录](#objects-v-freeform)。

这些标量类型的有效范围可进一步限制为某些模式、格式、最小值/最大值或预定义值。 使用这些约束，可以表示各种更具体的字段类型，包括：

* 枚举
* 长
* 短
* 字节
* 日期
* 日期时间
* 地图

>[!NOTE]
>
>“map”字段类型允许使用键值对数据，包括单个键的多个值。 映射只能在系统级别定义，这意味着您可能会遇到在行业或供应商定义的架构中定义的映射，但无法在您定义的字段中使用。 [架构注册API开发人员指南](../api/getting-started.md)包含有关定义字段类型的更多信息。

## 组合示例

架构表示将被摄取到[!DNL Platform]中并使用组合模型构建的数据的格式和结构。 如前所述，这些架构由一个类和与该类兼容的零个或多个字段组组成。

例如，描述在零售商店购物的架构可称为“[!UICONTROL 商店交易]”。 该架构实现与标准[!UICONTROL Commerce]字段组和用户定义的[!UICONTROL Product Info]字段组组合的[!DNL XDM ExperienceEvent]类。

跟踪网站流量的另一个架构可称为“[!UICONTROL Web访问]”。 它也实现了[!DNL XDM ExperienceEvent]类，但这次合并了标准[!UICONTROL Web]字段组。

下图显示了这些架构以及每个字段组贡献的字段。 它还包含两个基于[!DNL XDM Individual Profile]类的架构，包括本指南中前面提到的“[!UICONTROL 忠诚会员]”架构。

![](../images/schema-composition/composition.png)

### Union {#union}

虽然[!DNL Experience Platform]允许您为特定用例编写架构，但它还允许您查看特定类类型的架构“并集”。 上图显示了两个基于XDM ExperienceEvent类的架构和两个基于[!DNL XDM Individual Profile]类的架构。 下面显示的并集，聚合共享相同类（分别为[!DNL XDM ExperienceEvent]和[!DNL XDM Individual Profile]）的所有架构的字段。

![](../images/schema-composition/union.png)

启用与[!DNL Real-time Customer Profile]一起使用的架构后，该架构将包含在该类类型的并集中。 [!DNL Profile] 提供客户属性的强大、集中的配置文件，以及客户在与集成的任何系统中发生的每个事件的加盖时间戳的帐 [!DNL Platform]户。[!DNL Profile] 使用并集视图来表示此数据，并提供每个客户的整体视图。

有关使用[!DNL Profile]的更多信息，请参阅[实时客户资料概述](../../profile/home.md)。

## 将数据文件映射到XDM模式

摄取到[!DNL Experience Platform]的所有数据文件都必须符合XDM架构的结构。 有关如何设置数据文件格式以符合XDM层次结构（包括示例文件）的更多信息，请参阅[示例ETL转换](../../etl/transformations.md)上的文档。 有关将数据文件摄取到[!DNL Experience Platform]的常规信息，请参阅[批量摄取概述](../../ingestion/batch-ingestion/overview.md)。

## 外部区段的架构

如果要将来自外部系统的区段引入平台，则必须使用以下组件在您的架构中捕获它们：

* [[!UICONTROL 区段] 定义类](../classes/segment-definition.md):使用此标准类可捕获外部区段定义的关键属性。
* [[!UICONTROL 区段成员] 资格Detailsfield组](../field-groups/profile/segmentation.md):将此字段组添加到您的XDM单 [!UICONTROL 个配置文] 件架构中，以将客户配置文件与特定区段关联。

## 后续步骤

现在，您已了解架构组合的基础知识，接下来便可以使用[!DNL Schema Registry]开始探索和构建架构。

要查看两个核心XDM类及其常用兼容字段组的结构，请参阅以下参考文档：

* [[!DNL XDM Individual Profile]](../classes/individual-profile.md)
* [[!DNL XDM ExperienceEvent]](../classes/experienceevent.md)

[!DNL Schema Registry]用于访问Adobe Experience Platform中的[!DNL Schema Library]，并提供可从中访问所有可用库资源的用户界面和RESTful API。 [!DNL Schema Library]包含由Adobe定义的行业资源、由[!DNL Experience Platform]合作伙伴定义的供应商资源以及由组织成员组成的类、字段组、数据类型和架构。

要开始使用UI合成架构，请遵循[架构编辑器教程](../tutorials/create-schema-ui.md)来构建本文档中提到的“忠诚会员”架构。

要开始使用[!DNL Schema Registry] API，请首先阅读[架构注册API开发人员指南](../api/getting-started.md)。 阅读开发人员指南后，请按照教程中介绍的使用架构注册API](../tutorials/create-schema-api.md)创建架构的步骤操作。[

## 附录

以下各节包含有关模式组成原则的其他信息。

### 关系表与嵌入式对象 {#embedded}

在使用关系数据库时，最佳做法包括标准化数据，或将实体划分为离散段，然后在多个表中显示。 为了将数据作为一个整体读取或更新实体，必须使用JOIN对多个单独的表执行读写操作。

XDM模式通过使用嵌入式对象，可以直接表示复杂的数据并将其存储在具有分层结构的自包含文档中。 此结构的主要优势之一是它允许您查询数据，而无需通过与多个非规范化表的昂贵连接来重建实体。 对于架构层次结构的级别数，没有硬性限制。

### 模式和大数据 {#big-data}

现代数字系统会生成大量的行为信号（交易数据、网络日志、物联网、显示等）。 这种大数据提供了超凡的优化体验的机会，但由于数据的规模和种类繁多，使用起来也极具挑战性。 为了从数据中获得价值，必须对其结构、格式和定义进行标准化，以便能够一致、高效地对其进行处理。

模式通过允许从多个源集成数据、通过通用结构和定义进行标准化以及跨解决方案共享来解决此问题。 这允许后续流程和服务回答任何类型的数据问题，从传统的数据建模方法转向数据建模方法，在该方法中，将要询问数据的所有问题都事先已知，并且数据建模符合这些预期。

### 对象与自由格式字段 {#objects-v-freeform}

在设计架构时，在自由格式字段上选择对象时需要考虑一些关键因素：

| 对象 | 自由格式字段 |
| --- | --- |
| 增加嵌套 | 少或不嵌套 |
| 创建逻辑字段分组 | 字段被放置在临时位置中 |

{style=&quot;table-layout:auto&quot;}

#### 对象

下面列出了在自由格式字段上使用对象的利弊。

**优点**:

* 当您想要创建特定字段的逻辑分组时，最好使用对象。
* 对象以更结构化的方式组织架构。
* 对象间接有助于在区段生成器UI中创建良好的菜单结构。 架构中的分组字段会直接反映在区段生成器UI中提供的文件夹结构中。

**缺点**:

* 字段会变得更加嵌套。
* 使用[Adobe Experience Platform查询服务](../../query-service/home.md)时，必须为嵌套在对象中的查询字段提供较长的引用字符串。

#### 自由格式字段

下面列出了在对象上使用自由格式字段的利弊。

**优点**:

* 自由格式字段直接在架构的根对象下创建(`_tenantId`)，从而提高可见性。
* 使用查询服务时，自由表单字段的引用字符串往往较短。

**缺点**:

* 架构中自由格式字段的位置是临时的，这意味着它们在架构编辑器中以字母顺序显示。 这可能会降低架构的结构，并且类似的自由格式字段最终可能会因名称而有很大的差异。
