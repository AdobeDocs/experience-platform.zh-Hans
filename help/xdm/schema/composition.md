---
keywords: Experience Platform；主页；热门主题；模式;模式；枚举；混合；混合；混合；混合；数据类型；数据类型；数据类型；数据类型；主标识；主标识；XDM个人用户档案;XDM字段；数据类型；枚举；数据类型；体验事件;XDM体验事件;XDM体验事件；体验事件；;XDM Experienceevent;模式设计；类；类；类；类；数据类型；数据类型；数据类型；模式;模式；标识映射；标识映射；模式设计；映射；合并模式;合并
solution: Experience Platform
title: 模式合成基础
topic: overview
description: 本文档介绍了体验数据模型(XDM)模式，以及构成要在Adobe Experience Platform使用的模式的构件、原则和最佳做法。
translation-type: tm+mt
source-git-commit: 2dbd92efbd992b70f4f750b09e9d2e0626e71315
workflow-type: tm+mt
source-wordcount: '3165'
ht-degree: 0%

---


# 模式合成基础

本文档介绍了[!DNL Experience Data Model](XDM)模式，以及构成将在Adobe Experience Platform使用的模式的构件、原则和最佳做法。 有关XDM及其在[!DNL Platform]中的使用方式的一般信息，请参见[XDM系统概述](../home.md)。

## 了解模式

模式是表示和验证数据结构和格式的一组规则。 从高度讲，模式提供了真实对象（如人）的抽象定义，并勾勒出该对象的每个实例（如名、姓、生日等）中应包含哪些数据。

除了描述数据结构外，模式还对数据应用约束和期望，这样当数据在系统之间移动时，就可以验证数据。 这些标准定义允许一致地解释数据，而不管来源如何，并且无需跨应用程序进行翻译。

[!DNL Experience Platform] 通过使用模式来保持这种语义规范化。模式是描述[!DNL Experience Platform]中数据的标准方法，它允许符合模式的所有数据在整个组织内都可重复使用，而不会发生冲突，甚至可以在多个组织之间共享。

### 关系表与嵌入式对象

在使用关系数据库时，最佳实践包括将数据标准化，或将实体划分为离散部分，然后在多个表中显示。 为了将数据作为一个整体读取或更新实体，必须使用JOIN对多个单独的表执行读写操作。

XDM模式通过嵌入式对象的使用，可以直接表示复杂的数据并存储在具有分层结构的自包含文档中。 此结构的主要优点之一是它允许您查询数据，而无需通过昂贵的连接到多个非规范化表来重建实体。 您的模式层次结构可以有多少级别，没有硬性限制。

### 模式和大数据

现代数字系统产生大量行为信号（交易数据、网络日志、物联网、显示等）。 这些大数据优惠了优化体验的绝佳机会，但由于数据的规模和种类，使用起来极具挑战。 为了从数据中获得价值，必须对其结构、格式和定义进行标准化，以便能够一致、高效地处理数据。

模式通过允许从多个来源集成数据、通过通用结构和定义进行标准化并跨解决方案共享数据来解决这一问题。 这允许后续过程和服务回答任何类型的数据问题，从传统的数据建模方法转向数据建模方法，在该方法中，将要询问数据的所有问题都预先知道，并且数据被建模以符合这些期望。

### [!DNL Experience Platform]中基于模式的工作流

标准化是[!DNL Experience Platform]背后的一个关键概念。 XDM由Adobe驱动，旨在实现客户体验数据标准化并为客户体验管理定义标准模式。

构建[!DNL Experience Platform]的基础结构（称为[!DNL XDM System]）简化了基于模式的工作流，包括[!DNL Schema Registry]、[!DNL Schema Editor]、模式元数据和服务消耗模式。 有关详细信息，请参阅[XDM系统概述](../home.md)。

在[!DNL Experience Platform]中，构建和利用模式有几个关键优势。 首先，模式允许更好地管理数据并实现数据最小化，这一点对于隐私法规尤为重要。 其次，使用Adobe的标准组件构建模式，可让您开箱即用的洞察和使用AI/ML服务，并且最少可自定义。 最后，模式为数据共享洞察和有效安排提供基础架构。

## 规划模式

构建模式的第一步是确定您试图在模式中捕获的概念或真实对象。 一旦您确定了要描述的概念，您就可以开始规划模式，思考诸如数据类型、潜在身份域以及模式在未来的演变。

### [!DNL Experience Platform]中的数据行为

用于[!DNL Experience Platform]的数据分为两种行为类型：

* **记录数据**:提供有关主题属性的信息。主题可以是组织或个人。
* **时间序列数据**:提供记录主体直接或间接采取操作时系统的快照。

所有XDM模式都描述可以分类为记录或时间序列的数据。 模式的数据行为由模式的类定义，该类在模式首次创建时被分配给。 本文档后面对XDM类进行了更详细的介绍。

记录和时间序列模式都包含身份映射(`xdm:identityMap`)。 此字段包含主题的标识表示形式，该表示形式取自标为“标识”的字段，如下一节所述。

### [!UICONTROL 身份] {#identity}

模式用于将数据引入[!DNL Experience Platform]。 此视图可跨多个服务使用，以创建单个实体的单一统一数据。 因此，考虑模式时，必须考虑客户身份以及哪些字段可用于识别主题，无论数据来自何处。

为了帮助处理此过程，您的模式中的关键字段可以标记为身份。 在获取数据时，这些字段中的数据被插入到该个人的“[!UICONTROL 标识图]”中。 然后，[[!DNL Real-time Customer Profile]](../../profile/home.md)和其它[!DNL Experience Platform]服务可以访问图形数据，为每个客户提供拼接视图。

通常标为“[!UICONTROL Identity]”的字段包括：电子邮件地址、电话号码、[[!DNL Experience Cloud ID (ECID)]](https://experienceleague.adobe.com/docs/id-service/using/home.html)、CRM ID或其他唯一ID字段。 您还应考虑组织特有的所有唯一标识符，因为它们可能也是良好的“[!UICONTROL Identity]”字段。

在模式规划阶段考虑客户身份非常重要，这有助于确保整合数据以构建尽可能最可靠的用户档案。 请参阅[Adobe Experience Platform身份服务](../../identity-service/home.md)的概述，进一步了解身份信息如何帮助您向客户提供数字体验。

#### xdm:identityMap {#identityMap}

`xdm:identityMap` 是一个映射类型字段，它描述个人的各种身份值及其关联命名空间。此字段可用于为模式提供身份信息，而不是在模式本身的结构中定义身份值。

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

如上例所示，`identityMap`对象中的每个键都表示标识命名空间。 每个键的值是对象的数组，表示各个命名空间的标识值(`id`)。 有关由Adobe应用程序识别的标准身份命名空间](../../identity-service/troubleshooting-guide.md#standard-namespaces)的[列表，请参阅[!DNL Identity Service]文档。

>[!NOTE]
>
>还可为每个标识值提供一个布尔值，用于确定该值是否是主标识(`primary`)。 只需为要在[!DNL Real-time Customer Profile]中使用的模式设置主标识。 有关详细信息，请参阅[合并模式](#union)一节。

### 模式演化原则{#evolution}

随着数字体验的性质不断发展，用来代表数字体验的模式也必须如此。 因此，设计良好的模式能够根据需要进行调整和发展，而不会对模式的先前版本造成破坏性的改变。

由于保持向后兼容性对于模式发展至关重要，[!DNL Experience Platform]强制采用纯附加的版本控制原则，以确保对模式的任何修订只导致无损更新和更改。 换言之，不支持&#x200B;**中断更改。**

| 支持的更改 | 中断更改（不支持） |
|------------------------------------|---------------------------------|
| <ul><li>向现有模式添加新字段</li><li>使必填字段成为可选字段</li></ul> | <ul><li>删除以前定义的字段</li><li>引入新的必填字段</li><li>重命名或重定义现有字段</li><li>删除或限制以前支持的字段值</li><li>将属性移动到树中的其他位置</li></ul> |

>[!NOTE]
>
>如果尚未使用模式将数据收录到[!DNL Experience Platform]中，您可能会对该模式引入突破性的更改。 但是，在[!DNL Platform]中使用模式后，它必须遵守附加的版本控制策略。

### 模式和数据获取

要将数据收录到[!DNL Experience Platform]中，必须先创建数据集。 数据集是[[!DNL Catalog Service]](../../catalog/home.md)的数据转换和跟踪的构建块，通常表示包含所摄取数据的表或文件。 所有数据集都基于现有的XDM模式，它们为所摄取的数据应包含的内容以及如何构建提供约束。 有关详细信息，请参阅[Adobe Experience Platform数据摄取](../../ingestion/home.md)的概述。

## 模式积木

[!DNL Experience Platform] 使用一种合成方法，其中将标准构件块组合在一起以创建模式。这种方法促进现有组件的可重用性，并推动整个行业的标准化，以支持[!DNL Platform]中的供应商模式和组件。

模式使用以下公式组成：

**类+混音(&amp;A);= XDM模式**

&amp;ast;模式由类和零个或多个混音组成。 这意味着您可以构建数据集模式，而完全不使用mixin。

### 类{#class}

编写模式从指定类开始。 类定义模式将包含的数据的行为方面（记录或时间序列）。 除此之外，类还描述了所有基于该类的模式需要包含的最小公共属性数，并为合并多个兼容数据集提供了一种方法。

模式的类决定哪些混音符合在该模式中使用的条件。 这在下一节[中有更详细的讨论。](#mixin)

Adobe提供两个标准（“核心”）XDM类：[!DNL XDM Individual Profile]和[!DNL XDM ExperienceEvent]。 除了这些核心类之外，您还可以创建自己的自定义类，以描述组织的更具体用例。 当没有Adobe定义的核心类可用于描述唯一用例时，自定义类由组织定义。

### Mixin {#mixin}

混音是可重用的组件，它定义一个或多个字段，这些字段实现某些功能，如个人详细信息、酒店偏好或地址。 混合被设计为实现兼容类的模式的一部分。

混音根据所表示数据（记录或时间序列）的行为定义它们与哪些类兼容。 这意味着并非所有混音都可用于所有类。

[!DNL Experience Platform] 包括许多标准Adobe混音，同时允许供应商为其用户定义混音，并允许个别用户为自己的特定概念定义混音。

例如，要为“[!UICONTROL 忠诚会员]”模式捕获诸如“[!UICONTROL 名字]”和“[!UICONTROL 家庭地址]”等详细信息，您可以使用定义这些常见概念的标准混音。 但是，特定于不常用用例的概念(如“[!UICONTROL 忠诚度项目级别]”)通常没有预定义的混音。 在这种情况下，您必须定义自己的混音来捕获此信息。

请记住，模式由“零个或更多”混音组成，因此这意味着您无需使用任何混音即可构建有效的模式。

有关所有当前标准混合的列表，请参阅[官方XDM存储库](https://github.com/adobe/xdm/tree/master/components/mixins)。

### 数据类型{#data-type}

数据类型在类或模式中用作引用字段类型的方式与基本文本字段相同。 关键区别在于数据类型可以定义多个子字段。 与混音类似，数据类型允许多字段结构的一致使用，但比混音具有更大的灵活性，因为通过将数据类型添加为字段的“模式类型”，可以在的任意位置包含数据类型。

>[!NOTE]
>
>有关混音和数据类型之间差异的详细信息，请参阅[附录](#mixins-v-datatypes)，以及对于类似用例，使用一种方法的利弊。

[!DNL Experience Platform] 提供许多常用数据类型作为中的一 [!DNL Schema Registry] 部分，以支持使用标准模式描述常用数据结构。这在[!DNL Schema Registry]教程中有更详细的说明，当您逐步定义数据类型时，它将变得更加清晰。

### 字段

字段是模式最基本的构件。 字段通过定义特定数据类型提供与它们可以包含的数据类型相关的约束。 这些基本数据类型定义单个字段，而之前提到的[数据类型](#data-type)允许您定义多个子字段，并在各种模式中重复使用相同的多字段结构。 因此，除了将字段的“数据类型”定义为注册表中定义的数据类型之一外，[!DNL Experience Platform]还支持基本标量类型，如：

* 字符串
* 整数
* 双精度
* 布尔值
* 阵列
* 对象

>[!TIP]
>
>请参见[附录](#objects-v-freeform)，了解在对象类型字段上使用自由表单字段的利弊。

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
>“映射”字段类型允许键值对数据，包括单个键的多个值。 映射只能在系统级别定义，这意味着您可能在行业或供应商定义的模式中遇到映射，但该映射不能用于您定义的字段。 [模式注册表API开发人员指南](../api/getting-started.md)包含有关定义字段类型的详细信息。

下游服务和应用程序使用的某些数据操作对特定字段类型强制实施限制。 受影响的服务包括但不限于：

* [[!DNL Real-time Customer Profile]](../../profile/home.md)
* [[!DNL Identity Service]](../../identity-service/home.md)
* [[!DNL Segmentation]](../../segmentation/home.md)
* [[!DNL Query Service]](../../query-service/home.md)
* [[!DNL Data Science Workspace]](../../data-science-workspace/home.md)

在创建用于下游服务的模式之前，请查看这些服务的相应文档，以便更好地了解该模式所针对的数据操作的现场要求和限制。

### XDM字段

除了基本字段和定义您自己的数据类型的能力之外，XDM还提供了标准字段和数据类型集，这些字段和数据类型被[!DNL Experience Platform]服务隐含地理解，并且当在[!DNL Platform]组件中使用时提供更高的一致性。

这些字段（如“名字”和“电子邮件地址”）包含除基本标量字段类型之外的附加含义，告知[!DNL Platform]任何共享相同XDM数据类型的字段都将以相同方式行事。 无论数据来自何处，或[!DNL Platform]服务中使用数据，都可以信任此行为保持一致。

有关可用XDM字段的完整列表，请参阅[ XDM字段字典](field-dictionary.md)。 建议尽可能使用XDM字段和数据类型，以支持[!DNL Experience Platform]的一致性和标准化。

## 合成示例

模式表示将引入[!DNL Platform]并使用合成模型构建的数据的格式和结构。 如前所述，这些模式由类和与该类兼容的零个或多个混音组成。

例如，描述在零售商店购买的模式可能称为“[!UICONTROL 商店交易]”。 该模式实现与标准[!UICONTROL Commerce] mixin和用户定义的[!UICONTROL 产品信息] mixin组合的[!DNL XDM ExperienceEvent]类。

跟踪网站流量的另一个模式可能称为“[!UICONTROL Web访问]”。 它还实现[!DNL XDM ExperienceEvent]类，但这次合并了标准[!UICONTROL Web] mixin。

下图显示了这些模式以及每个混音贡献的字段。 它还包含两个基于[!DNL XDM Individual Profile]类的模式，包括本指南中前面提到的“[!UICONTROL 忠诚会员]”模式。

![](../images/schema-composition/composition.png)

### Union {#union}

[!DNL Experience Platform]允许您为特定用例编写模式，同时还允许您查看特定类类型的模式的“合并”。 上图显示了两个基于XDM ExperienceEvent类的模式和两个基于[!DNL XDM Individual Profile]类的模式。 合并符（如下所示）聚合共享相同类的所有模式的字段（分别为[!DNL XDM ExperienceEvent]和[!DNL XDM Individual Profile]）。

![](../images/schema-composition/union.png)

通过启用与[!DNL Real-time Customer Profile]一起使用的模式，该合并将包含在该类型的中。 [!DNL Profile] 提供强大、集中的用户档案客户属性，以及客户在与之集成的任何系统中拥有的每个事件的加盖时间戳的帐户 [!DNL Platform]。[!DNL Profile] 使用合并视图来表示此数据，并为每位客户提供整体视图。

有关使用[!DNL Profile]的详细信息，请参阅[实时客户用户档案概述](../../profile/home.md)。

## 将数据文件映射到XDM模式

所有被引入[!DNL Experience Platform]的数据文件都必须符合XDM模式的结构。 有关如何格式化数据文件以符合XDM层次（包括示例文件）的更多信息，请参见[示例ETL转换](../../etl/transformations.md)上的文档。 有关将数据文件引入[!DNL Experience Platform]的一般信息，请参阅[批处理摄取概述](../../ingestion/batch-ingestion/overview.md)。

## 后续步骤

现在，您已经了解模式合成的基础知识，可以开始使用[!DNL Schema Registry]探索和构建模式。

要查看两个核心XDM类及其常用兼容混合的结构，请参阅以下参考文档：

* [[!DNL XDM Individual Profile]](../classes/individual-profile.md)
* [[!DNL XDM ExperienceEvent]](../classes/experienceevent.md)

[!DNL Schema Registry]用于访问Adobe Experience Platform内的[!DNL Schema Library]，并提供一个用户界面和RESTful API，可从中访问所有可用的库资源。 [!DNL Schema Library]包含由Adobe定义的行业资源、由[!DNL Experience Platform]合作伙伴定义的供应商资源以及由组织成员组成的类、混合、数据类型和模式。

要开始使用UI编写模式，请按照[模式编辑器教程](../tutorials/create-schema-ui.md)构建本文档中提到的“忠诚会员”模式。

要开始使用[!DNL Schema Registry] API，请阅读[开始注册表API开发人员指南](../api/getting-started.md)进行模式。 阅读开发人员指南后，请按照教程中介绍的使用模式注册表API](../tutorials/create-schema-api.md)创建模式的步骤操作。[

## 附录

下节载有关于模式构成原则的补充资料。

### 对象与自由表单字段{#objects-v-freeform}

在设计模式时，在自由表单字段上选择对象时，需要考虑一些关键因素：

| 对象 | 自由表单字段 |
| --- | --- |
| 增加嵌套 | 嵌套更少或无嵌套 |
| 创建逻辑字段组 | 字段被放置在点对点位置 |

#### 对象

在自由表单字段上使用对象的利弊如下。

**优势**:

* 当您希望创建特定字段的逻辑分组时，最好使用对象。
* 对象以更结构化的方式组织模式。
* 对象间接有助于在区段生成器UI中创建良好的菜单结构。 模式中的分组字段会直接反映在区段生成器UI中提供的文件夹结构中。

**缺点**:

* 字段会变得更嵌套。
* 使用[Adobe Experience Platform查询服务](../../query-service/home.md)时，必须为嵌套在对象中的查询字段提供较长的引用字符串。

#### 自由表单字段

在对象上使用自由表单字段的利弊如下所示。

**优势**:

* 自由表单字段直接在模式的根对象下创建(`_tenantId`)，从而提高可见性。
* 使用查询服务时，自由表单字段的引用字符串往往较短。

**缺点**:

* 模式中自由表单字段的位置是临时的，这意味着这些字段在模式编辑器中以字母顺序显示。 这会降低模式的结构化程度，类似的自由表单字段最终可能会因名称而分开得很远。