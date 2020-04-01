---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Adobe Experience Platform细分服务
topic: overview
translation-type: tm+mt
source-git-commit: 5699022d1f18773c81a0a36d4593393764cb771a

---


# 分段服务概述

Adobe Experience Platform Segmentation Service提供用户界面和RESTful API，使您能够构建细分并根据实时客户用户档案数据生成受众。 这些细分在平台上集中配置和维护，任何Adobe解决方案都可轻松访问。

本文档概述了Segmentation Service及其在Adobe Experience Platform中的作用。

## Segmentation Service快速入门

了解本文档中使用的以下主要术语非常重要：

- **细分**:将大量个人(如客户、潜在客户、用户或组织)分为具有相似特征并将对营销策略作出类似反应的较小组。
- **细分定义**:用于描述目标受众的关键特性或行为的规则集。 概念化后，区段定义中概述的规则用于确定区段的合格受众成员。
- **受众**:生成的一组符合区段定义标准的用户档案。

## 细分的工作原理

细分是定义用户档案子集与用户档案商店共享的特定属性或行为的过程，以区分可销售的人群和客户群。 例如，在名为“您忘记购买运动鞋吗？”的电子邮件活动中，您可能希望受众过去30天内搜索跑鞋但未完成购买的所有用户。

在概念上定义区段后，它将在Experience Platform中构建。 通常，细分由营销人员或受众专家构建，但某些组织希望由其营销部门与数据分析师协作创建。 在审核发送到平台的数据时，数据分析人员通过选择将用于构建区段规则或条件的字段和值来组成区段定义。 这是使用UI或API完成的。

## 创建区段

无论是使用API创建还是使用区段生成器创建，区段最终都会使用用户档案查询语言(PQL)进行定义。 在这里，将在构建用于检索满足条件的用户档案的语言中描述概念段定义。 有关详细信息，请参阅 [PQL概述](./pql/overview.md)。

要了解如何在区段生成器（分段服务的UI实施）中创建和使用区段，请参阅区段生成 [器指南](./ui/overview.md)。

有关使用API构建区段定义的信息，请参阅有关使用API [创建受众区段的教程](./tutorials/create-a-segment.md)。

>[!NOTE] 在事件中，模式将被扩展，以后所有上传都必须相应地更新新添加的字段。 有关自定义体验数据模型(XDM)的更多信息，请访问 [模式编辑器教程](../xdm/tutorials/create-schema-ui.md)。

## 评估细分

### 流细分

>[!NOTE] 流细分是测试版功能，可应要求提供。

流细分是一个持续不断的数据选择过程，它会根据用户活动更新细分。 在构建并保存区段后，区段定义会针对传入数据应用到实时客户用户档案。 会定期处理细分增加和删除，确保您的目标受众保持相关性。

要了解有关流细分的更多信息，请阅读流 [细分文档](./ui/streaming-segmentation.md)。

### 批量分段

作为当前数据选择流程的替代方法，批处理分段通过段定义同时移动所有用户档案数据以生成相应的受众。 创建后，会保存并存储此区段，以便您导出它以供使用。

要了解如何评估区段，请参阅区 [段评估教程](./tutorials/evaluate-a-segment.md)。

## 访问分段结果

要了解如何访问导出的区段，请参阅区 [段评估教程](./tutorials/evaluate-a-segment.md)。

## 细分元数据

区段元数据便于在事件中索引，任何区段都将被重复使用和／或组合。

通过API或区段生成器合成区段需要您定义区段名称和合并策略。

### 区段名称

创建新区段时，您需要提供区段名称。 区段名称用于标识由分段服务构建的集合中的特定区段。 因此，区段名称应具有描述性、简明性和唯一性。

>[!NOTE] 在规划区段时，请记住，区段可以从任何其他区段中引用，并与之组合。 在选择名称时，请考虑您的区段可能包含可重用部分。

### 合并策略

合并策略是用户档案使用的规则，用于确定在某些条件下如何对数据进行优先级排序并合并为统一视图。
如果未定义合并策略，则使用默认的平台合并策略。 如果您希望使用特定于您的组织的合并策略，您可以创建自己的策略并将其标记为您的组织的默认策略。

>[!NOTE] 受众大小的估计基于组织的默认用户档案合并策略。

### 其他区段元数据

除了区段名称和合并策略之外，区段生成器还为您优惠了额外的“区段描述”元数据字段，您可以在其中汇总区段定义的用途。

## 高级细分功能

通过将流数据摄取与以下任何高级细分功能相结合 [](../ingestion/streaming-ingestion/overview.md) ，可将细分配置为持续生成受众:
- [顺序细分](#sequential)
- [动态细分](#dynamic)
- [多实体分割](#multi-entity)

以下各节将更详细地讨论这些高级功能。

## 顺序细分 {#sequential}

标准的用户旅程本质上是连续的。  Adobe Experience Platform允许您定义一系列有序的细分，以反映此旅程，从而捕获事件序列。 您可以使用区段生成器中的可视事件时间轴，将事件排列到所需的顺序。

需要按顺序细分的客户旅程的示例包括产品视图>产品添加>结帐>无购买。

## 动态细分 {#dynamic}

动态细分解决了营销人员在为营销活动构建细分时通常面临的可伸缩性问题。

与静态分段不同，动态分段要求您明确且重复地捕获每个可能的用例，动态分段使用变量来构建规则逻辑并动态表达关系。

### 用例：寻找在家以外购买的客户

为了说明此高级细分功能的价值，请考虑由数据架构师与营销人员协作来识别在其家庭状态以外进行购买的客户。

**问题**

静态分段要求您使用唯一的主状态属性定义单个区段，然后筛选不等于主状态的购买事件。 此类型的明确部分将显示“我正在寻找来自犹他州的人，而他们的购买状态不是犹他州”。 使用此方法创建受众需要您为每个美国州定义一个区段，总共50个区段。

由于缩放时不可避免地会出现不同的细分组合，因此静态细分所需的手动过程变得更加耗时，从而降低了整体效率。

**解决方案**

通过为购买状态属性分配变量，您的动态细分可以简化，以便“在购买状态不等于客户家庭状态的情况下查找我的购买”。 这样，您便可以将50个静态细分合并到一个动态细分中。

## 多实体分割 {#multi-entity}

借助高级的多实体细分功能，您可以使用多个XDM类创建细分，从而为人员模式添加扩展。 因此，分段服务可以在段定义期间访问其他字段，就像它们是用户档案数据存储的本机字段一样。

多实体细分提供了根据与业务需求相关的数据识别受众所需的灵活性。 无需查询数据库方面的专业知识即可快速轻松地完成此过程。 这样，您就无需对数据流进行代价高昂的更改或等待后端数据合并，即可将关键数据添加到细分中。

### 用例：价格驱动型促销

要说明此高级细分功能的价值，请考虑与营销人员协作的数据架构师。

在此示例中，数据架构师使用键将个人(由XDM个人用户档案和XDM ExperienceEvent作为其基类的模式组成)的数据连接到另一个类。 加入后，数据架构师或营销人员可以在区段定义期间使用这些新字段，就像它们是基类模式的本机字段一样。

**问题**

数据架构师和营销人员都为同一家服装零售商工作。 这家零售商在北美拥有1,000多家商店，并在整个生命周期内定期降低产品价格。 因此，营销人员希望运行一项特殊活动，为购买这些商品的购物者提供一个以折扣价购买这些商品的机会。

数据架构师的资源包括访问客户浏览的Web数据以及包含产品SKU标识符的购物车加货数据。 他们还可以访问单独的“产品”类别，该类别存储附加产品信息（包括产品价格）。 他们的指导是关注在过去14天内将产品添加到其购物车但没有购买该商品的客户，该商品的价格已经下降。

**解决方案**

>[!NOTE] 在此示例中，我们假定数据架构师已经建立了ID命名空间。

使用API，数据架构师将ExperienceEvent模式的密钥与“产品”类关联。 这样，数据架构师就可以像ExperienceEvent模式中的本机字段一样，使用“产品”类中的其他字段。 作为配置工作的最后一步，数据架构师需要将适当的数据引入实时客户用户档案。 这是通过启用“产品”数据集以与用户档案一起使用来实现的。 配置工作完成后，数据架构师或营销人员都可以在Segment Builder中构建目标区段。

请参阅 [模式构图概述](../xdm/schema/composition.md#union) ，了解如何定义跨XDM类的关系。

<!-- ## Personalization payload

Segments can now carry a payload of contextual details to enable deep personalization of Adobe Solutions as well as external non-Adobe applications. These payloads can be added while defining your target segment.

With contextual data built into the segment itself, this advanced Segmentation Service feature allows you to better connect with your customer.

Segment Payload helps you answer questions surrounding your customer’s frame of reference such as:
- What: What product was purchased? What product should be recommended next?
- When: At what time and date did the purchase occur?
- Where: In which store or city did the customer make their purchase?

While this solution does not change the binary nature of segment membership, it does add additional context to each profile through an associated segment membership object. Each segment membership object has the capacity to include three kinds of contextual data:

- **Identifier**: this is the ID for the segment 
- **Attributes**: this would include information about the segment ID such as last qualification time, XDM version, status and so on.
- **Event data**: Specific aspects of experience events which resulted in the profile qualifying for the segment

Adding this specific data to the segment itself allows execution engines to personalize the experience for the customers in their target audience. -->

### 用例

为了说明此高级细分功能的价值，请考虑三个标准用例，这些用例说明了在细分有效负荷增强之前在营销应用程序中存在的挑战：
- 电子邮件个性化
- 电子邮件重定位
- 广告重定位

**电子邮件个性化**

构建电子邮件活动的营销人员可能已尝试通过使用最近三个月内的客户商店购买来构建目标受众的细分。 理想情况下，此区段需要物品名称和进行购买的商店的名称。 在增强之前，难题是从购买事件中捕获商店标识符并将其分配给该客户的用户档案。

**电子邮件重定位**

创建和确定针对“购物车放弃”的电子邮件活动的区段通常很复杂。 在增强之前，由于可获得所需数据，很难了解要包含在个性化消息中的产品。 放弃产品的数据与体验事件相关，而体验过去难以监控和提取数据。

**广告重定位**

营销人员面临的另一个传统挑战是制作广告以重新定位已放弃购物车项目的客户。 虽然分部定义解决了这一难题，但在加强之前，没有正式方法区分所购买的产品和已放弃的产品。 现在，您可以在区段定义过程中目标特定数据集。

## 分段服务数据类型

分段服务中支持所有XDM数据类型。 构成区段定义的规则根据以下数据类型进行情境化。

### 字符串数据

区段定义使用字符串数据为区段受众定义非数字约束，如“国家／地区名称”或“忠诚度项目级别”。

字符串数据使用逻辑、包含／排除和比较语句包括在段定义中。 在将字符串属性添加到区段定义后，您可以使用字符串相关语句根据其他字符串字段对其进行评估。

| 语句类型 | 示例 |
| -------------- | -------- |
| 逻辑 | 和，或，不是 |
| 包含／排他 | include, must exist, exclude, must not exist |
| 比较 | equals, does not equal, contains,开始with |


### 日期数据

日期数据允许您通过使用特定开始/结束日期或使用下表中所示的与日期相关的语句，将基于时间的上下文分配给您的区段定义。 其中一项实施可能是创建与您的品牌在今年任何时候互动的 *受众* ，并且在过 *去几天内* 也很活跃的客户。

| 示例字段 | 与日期相关的声明 | 时间轴 |
| ------------- | ------------------------ | --------- |
| person.firstPurchase | 今，昨天，这个月，今年 | 与构建分类的日期相关。 |
| person.lastPurchase | 在最后，在，之前，之后，在 | 在任何给定周／月内相关。 |

### 体验事件

作为Adobe Experience Platform模式,XDM ExperienceEvents记录了客户与集成平台的应用程序的显式和隐式交互，包括交互时系统的快照。 ExperienceEvents是事实记录。 因此，在区段定义过程中，它们是可供您使用的数据源。

如下表所示，事件数据是使用关键字呈现的，这些关键字有助于优化事件行为并指定事件属性。

| 关键字 | 使用 |
| ------- | --- |
| 包含／排除 | 通过包含或遗漏数据来描述事件的行为。 |
| 任意／全部 | 帮助确定符合条件的细分数。 |
| “应用时间规则”切换按钮 | 整合日期数据。 |
| 等于、不等于、开始与、不开始与、结束于、不结束于、包含、不包含、存在、不存在 | 合并字符串数据。 |

### 区段

现有的区段定义也可以用作新区段定义的组件，从而将其属性和基于事件的规则添加到新区段。

### 受众

外部受众还可用作新区段定义的组件，将其属性规则添加到新区段。

目前，仅支持Adobe受众管理器作为受众。 将来将启用其他来源。

### 其他数据类型

除了上述内容之外，支持的数据类型的列表还包括：
- 字符串
- 统一资源标识符
- Enum
- 数值
- 长
- 整数
- 短
- 字节
- Boolean
- 日期
- 日期时间
- 阵列
- 对象
- 地图
- 事件

## 后续步骤

Segmentation Service提供了一个整合的工作流，用于根据实时客户用户档案数据构建细分。 总结：

- 细分是从用户档案商店中定义用户档案子集的过程，它允许您描述所需可销售组的行为或属性。 分段服务使此过程成为可能。
- 在规划区段时，请记住，区段可以从任何其他区段中引用并与之组合。
- 可以基于用户档案数据、相关时间序列数据或两者的规则构建区段。
- 可按需或连续评估区段。 按需评估后，所有用户档案数据会一次通过区段定义传递。 连续评估后，数据流在进入平台时通过细分定义。

要了解如何在UI中定义区段，请参阅“区段生 [成器”指南](./ui/overview.md)。 有关使用API构建区段定义的信息，请参阅有关使用API [创建区段的教程](./tutorials/create-a-segment.md)。