---
keywords: Experience Platform；主页；热门主题；架构；架构；枚举；mixin；字段组；字段组；mixin；数据类型；数据类型；数据类型；主要身份；XDM个人资料；XDM字段；枚举数据类型；体验事件；XDM体验事件；XDM ExperienceEvent；experienceevent；XDM Experienceevent；架构设计；类；类；类；数据类型；数据类型；数据类型；数据类型；架构；架构as；identityMap；身份映射；身份映射；架构设计；映射；合并架构；合并
solution: Experience Platform
title: 架构组合基础
description: 了解Experience Data Model (XDM)架构以及在Adobe Experience Platform中构建架构的构建块、原则和最佳实践。
exl-id: d449eb01-bc60-4f5e-8d6f-ab4617878f7e
source-git-commit: 8113b5298120f710f43c5a02504f19ca3af67c5a
workflow-type: tm+mt
source-wordcount: '4229'
ht-degree: 6%

---

# 模式组合基础

了解Experience Data Model (XDM)架构以及在Adobe Experience Platform中构建架构的构建块、原则和最佳实践。 有关XDM及其在中的使用方式的一般信息 [!DNL Platform]，请参见 [XDM系统概述](../home.md).

## 了解架构 {#understanding-schemas}

架构是一组规则，用于表示和验证数据的结构和格式。在高层面上，架构提供了真实世界对象（如人）的抽象定义，并概括了该对象的每个实例中应包含哪些数据（如名字、姓氏、生日等）。

除了描述数据结构之外，架构还会对数据应用约束和期望，以便数据在系统之间移动时能够被验证。 这些标准定义允许以一致的方式解释数据，而不管数据来自何处，并且消除跨应用程序翻译的需要。

Experience Platform使用架构维护此语义规范化。 架构是用于描述 Experience Platform 中数据的标准方式，符合架构的所有数据可以在组织中重复使用，而不会发生冲突，甚至可以在多个组织之间共享。

XDM架构非常适合以自包含格式存储大量复杂数据。 请参阅以下部分 [嵌入式对象](#embedded) 和 [大数据](#big-data) ，以了解有关XDM如何完成此任务的更多信息。

### Experience Platform中基于架构的工作流 {#schema-based-workflows}

标准化是Experience Platform背后的一个关键概念。 XDM由Adobe驱动，致力于标准化客户体验数据并定义用于客户体验管理的标准架构。

构建Experience Platform的基础架构，称为 [!DNL XDM System]，方便了基于模式的工作流，并包括 [!DNL Schema Registry]， [!DNL Schema Editor]、架构元数据和服务使用模式。 请参阅 [XDM系统概述](../home.md) 以了解更多信息。

在Experience Platform中使用架构有几个主要好处。 首先，架构允许更好的数据治理和数据最小化，这对于隐私法规尤其重要。 其次，使用Adobe的标准组件构建架构允许开箱即用的洞察和以最小的自定义使用AI/ML服务。 最后，架构为数据共享见解和高效编排提供了基础架构。

## 规划您的架构 {#planning}

构建架构的第一步是确定您尝试在架构中捕获的概念（或真实世界对象）。 一旦您确定了要描述的概念，就可以开始规划架构，方法是考虑数据类型、潜在的身份字段以及架构未来可能的发展方式等。

### Experience Platform中的数据行为 {#data-behaviors}

用于Experience Platform的数据分为两种行为类型：

* **记录数据**：提供有关主题属性的信息。 主体可以是组织，也可以是个人。
* **时间序列数据**：提供记录主体直接或间接执行操作时的系统快照。

所有XDM架构都描述了可归类为记录或时间序列的数据。 架构的数据行为由架构的类定义，该类在首次创建架构时分配给架构。 本文档后面详细介绍了XDM类。

记录和时间序列架构都包含标识映射(`xdm:identityMap`)。 此字段包含主体的身份表示形式，从标记为“身份”的字段绘制，如下节所述。

### [!UICONTROL 标识] {#identity}

>[!CONTEXTUALHELP]
>id="platform_schemas_identities"
>title="架构内的标识"
>abstract="标识是架构中的关键字段，可用于识别主题，例如电子邮件地址或营销 ID。这些字段用于为每个人构建标识图并构建客户配置文件。有关架构中标识的更多信息，请参阅该文档。"

架构用于将数据摄取到Experience Platform。 此数据可以跨多个服务使用，以创建单个实体的单个统一视图。 因此，在为客户身份设计架构时，重要的是要考虑哪些字段可用于识别主题，而不管数据可能来自何处。

为了帮助完成此过程，架构中的关键字段可以标记为标识。 摄取数据后，这些字段中的数据将插入&quot;[!UICONTROL 身份图]”代表该个人。 然后，可以通过访问图形数据 [[!DNL Real-Time Customer Profile]](../../profile/home.md) 和其他Experience Platform服务，以便提供各个客户的拼合视图。

通常标记为“”的字段[!UICONTROL 标识]”包括：电子邮件地址、电话号码、 [[!DNL Experience Cloud ID (ECID)]](https://experienceleague.adobe.com/docs/id-service/using/home.html)、 CRM ID或其他唯一ID字段。 考虑任何特定于贵组织的唯一标识符，因为它们可能有用”[!UICONTROL 标识]”字段。

在架构规划阶段考虑客户身份很重要，这样有助于确保将数据汇集在一起，以尽可能构建最强大的配置文件。 要详细了解身份信息如何帮助您向客户提供数字体验，请参阅 [Identity服务概述](../../identity-service/home.md). 请参阅数据建模最佳实践文档，以了解 [有关创建架构时使用标识的提示](./best-practices.md#data-validation-fields).

可通过两种方式将身份数据发送到Platform：

1. 通过 [架构编辑器UI](../ui/fields/identity.md) 或使用 [架构注册表API](../api/descriptors.md#create)
1. 使用 [`identityMap` 字段](#identityMap)

#### `identityMap` {#identityMap}

`identityMap` 是一个映射类型字段，用于描述个人的各种标识值及其关联的命名空间。 此字段可用于为架构提供标识信息，而不是在架构本身的结构中定义标识值。

使用的主要缺点 `identityMap` 身份会嵌入到数据中，并因此变得不那么可见。 如果您摄取原始数据，则应该在实际的架构结构中定义单独的标识字段。

>[!NOTE]
>
>使用的架构 `identityMap` 可用作关系中的源架构，但不能用作引用架构。 这是因为所有引用架构必须具有可见标识，该标识可以在源架构内的引用字段中映射。 请参阅上的UI指南 [关系](../tutorials/relationship-ui.md) 以了解有关源架构和参考架构要求的更多信息。

但是，如果架构的标识数量可变，或者您要从将标识存储在一起的源引入数据(例如 [!DNL Airship] 或Adobe Audience Manager)。 此外，如果您使用 [Adobe Experience Platform移动SDK](https://developer.adobe.com/client-sdks/home/).

简单标识映射的示例如下所示：

```json
"identityMap": {
  "email": [
    {
      "id": "jsmith@example.com",
      "primary": true
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
  "CRMID": [
    {
      "id": "2e33192000007456-0365c00000000000",
      "primary": false
    }
  ]
}
```

如上面的示例所示，在 `identityMap` 对象表示身份命名空间。 每个键的值是一个对象数组，表示标识值(`id`)。 请参阅 [!DNL Identity Service] 文档 [标准身份命名空间列表](../../identity-service/troubleshooting-guide.md#standard-namespaces) 可被Adobe应用程序识别。

>[!NOTE]
>
>用于表示该值是否为主标识(`primary`)也可以为每个标识值提供。 您只需要为要用于以下位置的架构设置主身份 [!DNL Real-Time Customer Profile]. 请参阅以下部分 [合并架构](#union) 以了解更多信息。

### 模式演化原则 {#evolution}

随着数字体验的性质不断演变，用于表示数字体验的架构也必须演变。 因此，设计良好的架构能够根据需要进行调整和演变，而不会导致对架构的先前版本进行破坏性更改。

由于保持向后兼容性对于模式演化至关重要，因此Experience Platform强制实施纯加性版本化原则。 此原则可确保对架构的任何修订仅导致非破坏性的更新和更改。 换句话说， **不支持重大更改。**

>[!NOTE]
>
>仅当尚未使用架构将数据摄取到Experience Platform中，并且尚未启用架构以在实时客户档案中使用时，您才可以对其引入重大更改。 但是，一旦架构被用于 [!DNL Platform]，则必须遵守添加版本控制策略。

下表列出了在编辑架构、字段组和数据类型时支持的更改：

| 支持的更改 | 重大更改（不支持） |
| --- | --- |
| <ul><li>向资源添加新字段</li><li>将必填字段设为可选</li><li>引入新的必填字段*</li><li>更改资源的显示名称和描述</li><li>启用架构以参与配置文件</li></ul> | <ul><li>删除以前定义的字段</li><li>重命名或重新定义现有字段</li><li>删除或限制以前支持的字段值</li><li>将现有字段移动到树中的其他位置</li><li>删除架构</li><li>禁用参与配置文件的架构</li></ul> |

\**请参阅以下部分，了解有关以下内容的重要注意事项 [设置新必填字段](#post-ingestion-required-fields).*

### 必填字段

单个架构字段可以是 [标记为必需](../ui/fields/required.md)，这意味着任何引入的记录都必须包含这些字段中的数据才能通过验证。 例如，根据需要设置架构的主要标识字段有助于确保所有摄取的记录都将参与实时客户档案。 同样，根据需要设置时间戳字段可确保按时间顺序保留所有时间序列事件。

>[!IMPORTANT]
>
>无论是否需要架构字段，Platform都不会接受 `null` 或任何引入的字段的值为空。 如果记录或事件中没有特定字段的值，则应该从摄取有效负载中排除该字段的键。

#### 在引入后根据需要设置字段 {#post-ingestion-required-fields}

如果某个字段曾用于摄取数据，并且最初未按要求设置，则该字段对于某些记录可能具有null值。 如果将此字段设置为必需的摄取后，则所有未来记录都必须包含此字段的值，即使历史记录可能为null。

将以前的可选字段设置为必填字段时，请牢记以下几点：

1. 如果您查询历史数据并将结果写入新数据集，则某些行将失败，因为它们包含必填字段的空值。
1. 如果字段参与 [Real-time Customer Profile](../../profile/home.md) 并且在根据需要设置数据之前导出数据，某些用户档案的数据可能为空。
1. 您可以使用架构注册表API查看Platform中所有XDM资源的带时间戳的更改日志，包括新的必填字段。 请参阅 [审核日志端点](../api/audit-log.md) 以了解更多信息。

### 架构和数据摄取

要将数据摄取到Experience Platform，必须首先创建数据集。 数据集是的数据转换和跟踪的构建块 [[!DNL Catalog Service]](../../catalog/home.md)，通常表示包含已摄取数据的表或文件。 所有数据集都基于现有XDM架构，这些架构为引入的数据应包含的内容以及应如何构建提供了限制。 有关更多详细信息，请参阅 [Adobe Experience Platform数据摄取](../../ingestion/home.md) 以了解更多信息。

## 架构的构建块 {#schema-building-blocks}

Experience Platform使用组合方法，其中组合标准构建块以创建架构。 这种方法促进现有组件的可重用性，并推动整个行业的标准化，以支持中的供应商架构和组件。 [!DNL Platform].

架构使用以下公式组成：

**类+架构字段组&amp;ast； = XDM架构**

&amp;ast；架构由一个类以及零个或多个架构字段组组成。 这意味着您无需使用字段组即可构建数据集架构。

### 类 {#class}

>[!CONTEXTUALHELP]
>id="platform_schemas_class"
>title="类"
>abstract="每个架构都基于一个类。这种类定义了架构的行为，以及基于该类的所有架构必须包含的公共属性。请参阅文档以了解有关类如何参与架构组合的更多信息。"

架构的合成从指定类开始。 类定义架构将包含的数据的行为方面（记录或时间序列）。 除此之外，类还描述了基于该类的所有架构所需包含的最少数量的公共属性，并提供了一种合并多个兼容数据集的方法。

架构的类确定哪些字段组适合在该架构中使用。 有关详情，请参见 [下一节](#field-group).

Adobe提供了多个标准（“核心”）XDM类。 其中两门课， [!DNL XDM Individual Profile] 和 [!DNL XDM ExperienceEvent]对于几乎所有下游平台进程而言，是必需的。 除了这些核心类之外，您还可以创建自己的自定义类，以描述组织更具体的用例。 当没有Adobe定义的核心类可用于描述独特用例时，自定义类由组织定义。

以下屏幕截图演示了类在Platform UI中的表示方式。 由于显示的示例架构不包含任何字段组，因此显示的所有字段均由架构的类([!UICONTROL XDM个人资料])。

![此 [!UICONTROL XDM个人资料] 在架构编辑器中。](../images/schema-composition/class.png)

有关可用标准XDM类的最新列表，请参阅 [官方XDM存储库](https://github.com/adobe/xdm/tree/master/components/classes). 或者，您可以参阅以下指南： [浏览XDM组件](../ui/explore.md) 如果您希望在UI中查看资源。

### 字段组 {#field-group}

>[!CONTEXTUALHELP]
>id="platform_schemas_fieldgroup"
>title="字段组"
>abstract="字段组是可重用的组件，可让您使用其他属性扩展架构。大多数字段组仅与某些类兼容。您可以使用 Adobe 定义的标准字段组，也可以手动定义您自己的自定义字段组。请参阅文档以了解有关字段组如何参与架构组合的更多信息。"

>[!CONTEXTUALHELP]
>id="platform_schemas_fieldgroup_requiredFieldgroup"
>title="必填字段组"
>abstract="您正在使用的源需要此字段组。因此，您无法从架构中删除它。"

字段组是可重复使用的组件，它定义一个或多个用于实现特定功能（如个人详细信息、酒店首选项或地址）的字段。 字段组旨在作为实现兼容类的架构的一部分包含。

字段组根据它们表示的数据（记录或时间序列）的行为，定义它们兼容的类或类。 这意味着并非所有字段组都可以与所有类一起使用。

Experience Platform包括许多标准Adobe字段组，同时还允许供应商为其用户定义字段组，以及单个用户为其自己的特定概念定义字段组。

例如，用于捕获详细信息，如&quot;[!UICONTROL 名字]”和“[!UICONTROL 家庭地址]适用于您的&quot;[!UICONTROL 忠诚会员]”架构中，您将能够使用标准字段组来定义这些常用概念。 但是，标准字段组可能未涵盖的对您的组织更具体的概念（例如自定义忠诚度计划详细信息或产品属性）。 在这种情况下，您必须定义自己的字段组来捕获此信息。

>[!NOTE]
>
>强烈建议您在架构中尽可能使用标准字段组，因为Experience Platform服务隐式理解这些字段，并在跨以下各项使用时提供更高的一致性 [!DNL Platform] 组件。
>
>标准组件（如“名字”和“电子邮件地址”）提供的字段包含基本标量字段类型以外的附加含义。 他们告诉 [!DNL Platform] 任何共享相同数据类型的字段都将以相同的方式运行。 无论数据来自何处或来自何处，这种行为都可以保持一致 [!DNL Platform] 正在使用数据的服务。

请记住，架构由“零个或多个”字段组组成，这意味着您无需使用任何字段组即可构建有效架构。

以下屏幕截图演示了字段组在Platform UI中的表示方式。 单个字段组([!UICONTROL 人口统计详细信息])添加到此示例中的架构，这提供了架构结构的一组字段。

![具有的架构编辑器 [!UICONTROL 人口统计详细信息] 在示例架构中高亮显示的字段组。](../images/schema-composition/field-group.png)

有关可用标准XDM字段组的最新列表，请参阅 [官方XDM存储库](https://github.com/adobe/xdm/tree/master/components/fieldgroups). 或者，您可以参阅以下指南： [浏览XDM组件](../ui/explore.md) 如果您希望在UI中查看资源。

### 数据类型 {#data-type}

数据类型在类或架构中用作引用字段类型，其使用方式与基本文本字段相同。 关键的区别在于，数据类型可以与字段组一样定义多个子字段。 它们之间的主要区别在于，通过将数据类型添加为字段的“数据类型”，可以将数据类型包含在架构中的任何位置。 虽然字段组仅与某些类兼容，但数据类型可以包含在任何父类或字段组中。

>[!NOTE]
>
>如果字段被定义为特定数据类型，则无法在另一个架构中创建具有不同数据类型的相同字段。 此限制适用于您组织的租户。

Experience Platform提供了许多常见数据类型，作为 [!DNL Schema Registry] 支持使用标准模式来描述常见的数据结构。 详情请参阅 [架构注册表教程](../tutorials/create-schema-api.md) 当您逐步完成定义数据类型的步骤时，和将更加清晰。

以下屏幕截图演示了数据类型在Platform UI中的表示方式。 提供的字段之一 [!UICONTROL 人口统计详细信息] 字段组使用&quot;[!UICONTROL 对象]”数据类型，如管道字符(`|`)。 此特定数据类型提供了多个与个人姓名相关的子字段，这是一种构造，可重复用于需要捕获个人姓名的其他字段。

![架构编辑器中的图表，显示突出显示全名对象和属性的个人。](../images/schema-composition/data-type.png)

有关可用标准XDM数据类型的最新列表，请参阅 [官方XDM存储库](https://github.com/adobe/xdm/tree/master/components/datatypes). 或者，您可以参阅以下指南： [浏览XDM组件](../ui/explore.md) 如果您希望在UI中查看资源。

### 字段 {#field}

字段是架构的最基本构建块。 字段通过定义特定数据类型，提供了有关它们可以包含的数据类型的约束。 这些基本数据类型定义单个字段，而 [数据类型](#data-type) 前面提到的允许您定义多个子字段并在各种架构中重用相同的多字段结构。 因此，除了将字段的“数据类型”定义为注册表中所定义的数据类型之一之外，Experience Platform还支持基本标量类型，例如：

* 字符串
* 整数
* 双精度
* 布尔值
* 数组
* 对象

>[!TIP]
>
>请参阅 [附录](#objects-v-freeform) 以了解在对象类型字段上使用自由表单字段的利弊。

这些标量类型的有效范围可以进一步限制为某些模式、格式、最小值/最大值或预定义值。 使用这些约束，可以表示范围更广的更具体的字段类型，包括：

* 枚举
* 长
* 短
* 字节
* 日期
* 日期时间
* 地图

>[!NOTE]
>
>“映射”字段类型允许键值对数据，包括单个键的多个值。 映射可以在标准XDM类和字段组中找到，但您也可以使用架构注册表API定义自定义映射。 请参阅上的教程 [定义自定义字段](../tutorials/custom-fields-api.md#custom-maps) 以了解更多信息。

## 组合示例 {#composition-example}

架构是使用组合模型构建的，用于表示要引入的数据的格式和结构 [!DNL Platform]. 如前所述，这些架构由一个类以及与该类兼容的零个或多个字段组组成。

例如，描述在零售商店购买的架构可能称为&quot;[!UICONTROL 存储交易记录]“。 架构实现 [!DNL XDM ExperienceEvent] 与标准组合的类 [!UICONTROL 商务] 字段组和用户定义的 [!UICONTROL 产品信息] 字段组。

另一个跟踪网站流量的架构可能称为“[!UICONTROL Web访问]“。 它还会实施 [!DNL XDM ExperienceEvent] 类，但这次将标准 [!UICONTROL Web] 字段组。

下图显示了这些架构以及每个字段组贡献的字段。 它还包含两个基于 [!DNL XDM Individual Profile] 类，包括&quot;[!UICONTROL 忠诚会员]”架构在本指南前面已提及。

![包含四个架构和为其做出贡献的字段组的流程图。](../images/schema-composition/composition.png)

### 并集 {#union}

虽然Experience Platform允许您为特定用例编写架构，它还允许您查看特定类类型的架构的“并集”。 上图显示了两个基于XDM ExperienceEvent类的架构和两个基于 [!DNL XDM Individual Profile] 类。 如下所示的并集聚合了共享相同类([!DNL XDM ExperienceEvent] 和 [!DNL XDM Individual Profile]、分别)。

![描述构成这些字段的合并架构流程图。](../images/schema-composition/union.png)

启用架构以用于 [!DNL Real-Time Customer Profile]，它包含在该类类型的并集中。 [!DNL Profile] 提供了客户属性的强大、集中的配置文件，以及客户在与集成的任何系统中发生的每个事件的带时间戳的帐户 [!DNL Platform]. [!DNL Profile] 使用合并视图来表示此数据，并提供每个客户的整体视图。

有关使用的更多信息 [!DNL Profile]，请参见 [Real-time Customer Profile概述](../../profile/home.md).

## 将数据文件映射到XDM架构 {#mapping-datafiles}

摄取到Experience Platform中的所有数据文件必须符合XDM架构的结构。 有关如何格式化数据文件以符合XDM层次结构的更多信息（包括示例文件），请参阅上的文档 [示例ETL转换](../../etl/transformations.md). 有关将数据文件引入Experience Platform的一般信息，请参阅 [批量摄取概述](../../ingestion/batch-ingestion/overview.md).

## 外部受众的架构

如果要将受众从外部系统引入到Platform中，则必须使用以下组件在架构中捕获这些受众：

* [[!UICONTROL 区段定义] 类](../classes/segment-definition.md)：使用此标准类捕获外部区段定义的键属性。
* [[!UICONTROL 区段成员资格详细信息] 字段组](../field-groups/profile/segmentation.md)：将此字段组添加到您的 [!UICONTROL XDM个人资料] 架构以将客户配置文件与特定受众关联。

## 后续步骤

现在您已了解架构组合的基础知识，可以开始使用探索和构建架构了 [!DNL Schema Registry].

要查看两个核心XDM类的结构及其常用的兼容字段组，请参阅以下参考文档：

* [[!DNL XDM Individual Profile]](../classes/individual-profile.md)
* [[!DNL XDM ExperienceEvent]](../classes/experienceevent.md)

此 [!DNL Schema Registry] 用于访问 [!DNL Schema Library] Adobe Experience Platform ，并提供一个用户界面和RESTful API，所有可用的库资源都可从该API访问。 此 [!DNL Schema Library] 包含由Adobe定义的行业资源、由Experience Platform合作伙伴定义的供应商资源，以及由您的组织成员组成的类、字段组、数据类型和架构。

要开始使用UI构建架构，请遵循以下说明 [架构编辑器教程](../tutorials/create-schema-ui.md) 构建本文档中提到的“忠诚会员”模式。

要开始使用 [!DNL Schema Registry] API，首先阅读 [架构注册API开发人员指南](../api/getting-started.md). 阅读开发人员指南后，请按照以下教程中概述的步骤 [使用架构注册表API创建架构](../tutorials/create-schema-api.md).

## 附录

以下部分包含有关模式组合原则的其他信息。

### 关系表与嵌入对象 {#embedded}

使用关系数据库时，最佳实践涉及标准化数据，或获取实体并将其划分为多个离散片段，这些片段随后显示在多个表中。 要将数据作为一个整体读取或更新实体，必须使用JOIN对多个单独的表进行读取和写入操作。

通过使用嵌入式对象，XDM架构可以直接表示复杂的数据并将其存储在具有分层结构的自包含文档中。 此结构的主要优点之一是，它允许您查询数据，而无需通过连接到多个非规范化表的昂贵连接来重构实体。 架构层次结构可以具有的级别数没有硬性限制。

### 架构和大数据 {#big-data}

现代数字系统会产生大量的行为信号（交易数据、网络日志、物联网、显示等）。 这种大数据提供了优化体验的绝佳机会，但由于数据的规模和多样性，使其使用起来颇具挑战性。 为了从数据中获得价值，其结构、格式和定义必须标准化，以便能够一致高效地处理。

架构通过允许从多个来源集成数据、通过通用结构和定义标准化数据并在解决方案之间共享数据而解决了此问题。 这允许后续的进程和服务回答所询问数据的任何类型的问题。 它告别了传统的数据建模方式，即所有需要询问的数据问题都事先已知，而数据建模就是为了符合这些期望。

### 对象与自由表单字段 {#objects-v-freeform}

在设计架构时，通过自由格式字段选择对象时要考虑一些关键因素：

| 对象 | 自由格式字段 |
| --- | --- |
| 增加嵌套 | 较少嵌套或不嵌套 |
| 创建逻辑字段分组 | 字段放置在临时位置 |

{style="table-layout:auto"}

#### 对象

下面列出了在自由格式字段上使用对象的利弊。

**优点**：

* 当要创建特定字段的逻辑分组时，最好使用对象。
* 对象以更加结构化的方式组织方案。
* 对象间接有助于在区段生成器UI中创建良好的菜单结构。 架构中的分组字段会直接反映在区段生成器UI中提供的文件夹结构中。

**缺点**：

* 字段变得更加嵌套。
* 使用时 [Adobe Experience Platform查询服务](../../query-service/home.md)中，必须为嵌套在对象中的查询字段提供更长的引用字符串。

#### 自由格式字段

下面列出了在对象上使用自由格式字段的利弊。

**优点**：

* 自由格式字段直接在架构的根对象下创建(`_tenantId`)，提高可见性。
* 使用查询服务时，自由格式字段的引用字符串往往较短。

**缺点**：

* 架构中自由格式字段的位置是临时的，这意味着它们在架构编辑器中按字母顺序显示。 这会使架构的结构性降低，并且类似的自由格式字段可能会因名称而异，相差很大。
