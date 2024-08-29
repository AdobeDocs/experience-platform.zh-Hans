---
title: AI助手的问题指南
description: 请阅读本文档，了解在查询AI助手时可以使用的示例问题。
exl-id: d16d1262-cc2d-45c9-94c4-b86132183442
source-git-commit: fc87c28d7019e123d974e4d2ad307928a3d3fe89
workflow-type: tm+mt
source-wordcount: '1524'
ht-degree: 1%

---

# AI助手的问题指南

请阅读此文档，以了解在查询AI助手时可以使用的一组示例问题。

您还可以使用此文档学习有关[如何对您的问题添加短语](#phrasing-your-questions)的提示，以便从AI助手获得最佳响应。

## 基于目标的问题 {#objectives-questions}

以下示例问题按使用AI Assistant时可以完成的目标分组：

| 目标 | 描述 | 示例 |
| --- | --- | --- |
| 学习概念和持续工作流 | <ul><li>作为新手，您可以使用AI Assistant学习Real-Time CDP和Adobe Journey Optimizer概念，并熟悉不熟悉的产品和功能。</li><li>作为经验丰富的用户，您可以使用AI Assistant解决可能阻止工作流的边缘案例。 | <ul><li>如何在历程分析中设置功能板？</li><li>告诉我Real-Time CDP的一些用例。</li></ul> |
| 故障排除 | 使用AI Assistant了解如何调试工作流中可能遇到的基本错误。 | <ul><li>此错误{ERROR_MESSAGE}是什么意思？</li><li>为何无法删除名为“Luma：电子邮件受众”的受众？</li></ul> |
| 沙盒卫生 | 使用AI Assistant识别任何重复或未使用的对象，以便您能够有效地维护沙盒。 | <ul><li>能否向我显示类似的受众？</li><li>是否有任何没有关联数据集的架构？</li></ul> |
| 价值分析 | 使用AI Assistant识别您最常用的数据对象，评估任何绩效指标或找到最有价值的数据对象。 | <ul><li>我们的“Luma：电子邮件受众”区段定义中有多少个配置文件？</li><li>何时将受众激活到“Experience Cloud受众”目标？</li></ul> |
| 搜索 | 使用AI Assistant查找支持的Experience Platform对象，如受众、数据集、目标、架构和源。 | <ul><li>在名称中列出包含“Luma”的受众（在上季度创建）。</li><li>“Luma：自定义操作”XDM架构中有哪些属性？</li></ul> |
| 影响分析 | 使用AI Assistant识别某些工作流中使用的数据对象，以便您能够评估任何更改的影响。 | <ul><li>哪些受众在“Luma： PersonProfiles”架构中使用`homeAddress.city`？</li><li>`consents.marketing.push.val`配置文件属性存储在哪些数据集中？</li></ul> |

{style="table-layout:auto"}

## 按实体和产品知识问题列出的运营见解{#objects-questions}

以下问题按数据对象分组，并被分类为[操作分析](./home.md#operational-insights)或[产品知识](./home.md#product-knowledge)。

![](./images/prompt.png)

* **受众 — 运营分析**
   * 哪些受众使用其他受众？
   * 受众中用户档案数量的分布情况如何？
   * 显示上次在{RELATIVE_DATE}之前修改的受众。
   * 哪些受众具有0个配置文件？
   * {USE_AUTO_COMPLETE_TO_FILL_AUDIENCE_NAME}是否用于任何其他受众？
* **属性 — 运营分析**
   * 哪些受众的区段定义中具有xdm属性{ATTRIBUTE_PATH}？
   * 任何受众中未使用多少XDM架构属性？
   * 哪些架构中具有xdm属性{ATTRIBUTE_PATH}？
   * 激活哪些XDM属性？
   * 具有超过10个配置文件的受众中使用哪些XDM属性？
* **数据流 — 运营分析**
   * 哪些数据流对{USE_AUTO_COMPLETE_TO_FILL_DATASET_NAME}数据集有贡献？
   * 未使用哪些源数据流或者不再有数据进入？
   * 列出我具有的源数据流。
   * 为每个源连接器配置哪些数据流？
* **数据集 — 运营分析**
   * 使用相同架构摄取了多少数据集？
   * 哪个源连接器与{USE_AUTO_COMPLETE_TO_FILL_DATASET_NAME}数据集关联？
   * 每个受众使用哪些数据集？
   * 哪些架构未在任何数据集中使用？
   * 我有多少个数据集？
* **目标 — 运营分析**
   * 哪些目标处于活动状态？
   * 哪些目标帐户激活了0个受众？
   * 每个目标激活了多少受众？
   * 哪些目标的激活受众数量最多？
* **历程 — 运营分析**
   * 我有多少个历程？
   * 已在{RELATIVE_DATE}（例如上一周）或{RELATIVE_DATE}（例如特定日期之前/之后/日期）创建哪些历程？
   * 是否显示在{RELATIVE_DATE}（例如上周）或{RELATIVE_DATE}（例如特定日期之前/之后/日期）中修改的历程列表？
   * 列出我的实时历程。
   * 列出实时历程中使用的受众。
* **源 — 运营分析**
   * 哪些源处于活动状态？
   * 哪个源连接器与数据集{USE_AUTO_COMPLETE_TO_FILL_DATASET_NAME}关联。
   * 哪个源连接器的关联帐户数最多？
   * 显示数据流及其关联的源连接器。
* **定向学习 — 产品知识(Real-Time CDP和Journey Optimizer)**
   * 哪些受众具有相似性？
   * 用户组与角色有何关系？
   * 什么时候应该使用数据类型而不是字段组？
   * 标识与主键或外键之间有何区别？
   * 如何计算配置文件丰富度？
* **故障排除 — 产品知识(Real-Time CDP和Journey Optimizer)**
   * AI 助手能帮上什么忙？
   * 能否在摄取数据后删除启用配置文件的架构？
   * 为何无法删除受众？
   * 评估受众和获得定位结果需要多长时间？

## 用短语表述您的问题 {#phrasing-your-questions}

您必须清晰而有条理地向AI Assistant表达您的问题，以便获得尽可能准确的响应。 请参阅以下提示列表，以获取有关如何根据上下文提出明确问题的指导：

* 以简洁的方式陈述您的任务和/或问题。
* 避免使用模糊的语言或过于复杂的语法以促进理解。
* 提供关于您的任务和/或问题的相关上下文，因为上下文可以帮助AI助手生成更相关的响应。

请阅读下表，了解在向AI助手提问时应遵循的最佳实践的进一步指导。

下表概述了在使用AI Assistant时可以遵循的最佳实践：

| Do | 示例 |
| --- | --- |
| <ul><li>指定要检索或分析的对象或信息。</li><li>尝试将数据对象名称放在引号中。 如果您只知道对象名称的一部分，则还可以在问题中指定该部分。</li><li>使用[对象自动完成](./ui-guide.md#use-auto-complete)以帮助AI Assistant更好地了解查询的上下文。</li></ul> | <ul><li>哪些数据集使用“Luma — 忠诚度”架构？</li><li>显示名称中包含“Luma”的激活区段。 按用户档案计数对其进行排名。</li></ul> |
| <ul><li>避免歧义，使用清晰的语言</li><li>使用准确的术语以确保查询更清晰。</li><li>在询问有关Adobe Experience Platform的问题时，请尝试使用特定于Experience Platform的术语来提高响应的相关性。</li></ul> | <ul><li>“ACME受众”中有多少个人资料。</li><li>显示激活的受众中使用的前5个XDM属性。</li></ul> |
| <ul><li>提供上下文或指定条件以筛选结果。</li><li>在问题中使用过滤条件限制响应中的数据量。</li></ul> | <ul><li>向我显示尚未激活且创建日期超过6个月且从未修改的受众。</li><li>向我显示激活到“ACME目标”并具有超过10000个配置文件的受众。</li></ul> |

{style="table-layout:auto"}

| 不要 | 示例 |
| --- | --- |
| 使用模糊或模糊的语言。 | <ul><li>给我有关数据集的信息。</li><li>“ACME受众”中有多少用户？</li><li>显示区段。</li><li>列表属性。</li></ul> |
| 发出不完整的请求。 | “Luma — 忠诚度数据集” |
| 接受没有上下文的知识。 | <ul><li>过去6个月中的受众。</li><li>为我构建查询。</li></ul> |
| 制定过于复杂的查询。 | 提供跨所有对象及其依赖关系的数据谱系的综合分析。 |
| 省略标准或参数。 | 向我显示数据集。 |

{style="table-layout:auto"}

## 不支持的问题的示例 {#unsupported-questions}

以下是AI助手当前不支持的问题示例列表。

+++选择以查看不支持的问题的示例

### 运营洞察

* 此沙盒中有多少配置文件位于加利福尼亚？ （**注意**：对于类似的问题，您必须提供特定条件，以便为您的请求提供足够的上下文，在这种情况下，特定条件为“加利福尼亚州”）。
* 此配置文件{PROFILE_INFO/ATTRIBUTE_VALUE}包含哪些区段？
* 数据集中有多少用户档案有电子邮件？
* 哪个数据集构成此沙盒中的最大配置文件数？
* 哪个数据集的记录数最多？
* {RELATIVE_DATE}中删除了多少区段？
* 我的哪个数据集大小最大？
* 在{AUDIENCE_NAME}中向我提供配置文件。
* 我的沙盒中的配置文件总数是多少
* 有多少身份命名空间与受众{AUDIENCE_NAME}关联？
* 向我显示今天评估的所有受众区段的报表
* 有多少区段具有重叠的用户档案？
* 正在加载到{DATASET_NAME}中的批次数量
* 我有多少个活动选件？
* 我有多少个活动的营销活动？
* 我的数据源来自何处？
* 最大的数据集或数据源是什么？
* 我能否获取已创建这些架构的用户列表？

### 故障排除

* 为何此批次{BATCH_NAME/BATCH_ID}仍在处理中？
* 为什么没有符合此受众{AUDIENCE_NAME}资格条件的受众？
* 我看不到客户人工智能，为什么以及如何修复它？
* 我看不到数据集预览，为什么以及如何修复它？
* 为何无法删除{SEGMENT/DATASET/SCHEMA_NAME}？
* 我有权访问查询服务吗？

### 任务和自动化

* 编写一个查询，从{DATASET_NAME}中给我一条记录。
* 将示例API调用写入/schemas/{schemaId}/fields/{fieldPath}/values。
* 为我设置源/目标。
* 使用条件{USER_SPECIFIC_CRITERIA}为我创建受众。

+++

## 后续步骤

通过阅读本文档，您现在了解了如何优化AI Assistant的问题。 有关如何在工作流期间使用该功能的信息，请阅读[AI助手UI指南](ui-guide.md)。
