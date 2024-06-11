---
title: AI助手的问题指南
description: 请阅读本文档，了解在查询AI助手时可以使用的示例问题。
exl-id: d16d1262-cc2d-45c9-94c4-b86132183442
source-git-commit: 26e27e7a62731fe43ef203741121b22226078b28
workflow-type: tm+mt
source-wordcount: '1206'
ht-degree: 1%

---

# AI助手的问题指南

请阅读此文档，以了解在查询AI助手时可以使用的一组示例问题。

您还可以通过本文档了解有关以下内容的提示 [如何用短语回答您的问题](#phrasing-your-questions) 以从AI Assistant获取最佳响应。

## 基于目标的问题 {#objectives-questions}

以下示例问题按使用AI Assistant时可以完成的目标分组：

| 目标 | 描述 | 示例 |
| --- | --- | --- |
| 学习概念和持续工作流 | <ul><li>作为新手，您可以使用AI Assistant学习Real-Time CDP和Adobe Journey Optimizer概念，并熟悉不熟悉的产品和功能。</li><li>作为经验丰富的用户，您可以使用AI Assistant解决可能阻止工作流的边缘案例。 | <ul><li>如何在历程分析中设置功能板？</li><li>告诉我Real-Time CDP的一些用例。</li></ul> |
| 故障排除 | 使用AI Assistant了解如何调试工作流中可能遇到的基本错误。 | <ul><li>为什么会出现此错误 {ERROR_MESSAGE} 是刻薄吗？</li><li>为何无法删除名为“Luma：电子邮件受众”的受众？</li></ul> |
| 沙盒卫生 | 使用AI Assistant识别任何重复或未使用的对象，以便您能够有效地维护沙盒。 | <ul><li>能否向我显示类似的受众？</li><li>是否有任何没有关联数据集的架构？</li></ul> |
| 价值分析 | 使用AI Assistant识别您最常用的数据对象，评估任何绩效指标或找到最有价值的数据对象。 | <ul><li>我们的“Luma：电子邮件受众”区段定义中有多少个配置文件？</li><li>何时将受众激活到“Experience Cloud受众”目标？</li></ul> |
| 搜索 | 使用AI Assistant查找支持的Experience Platform对象，如受众、数据集、目标、架构和源。 | <ul><li>在名称中列出包含“Luma”的受众（在上季度创建）。</li><li>“Luma：自定义操作”XDM架构中有哪些属性？</li></ul> |
| 影响分析 | 使用AI Assistant识别某些工作流中使用的数据对象，以便您能够评估任何更改的影响。 | <ul><li>使用哪些受众 `homeAddress.city` 在“Luma：PersonProfiles”架构中？</li><li>哪些数据集是 `consents.marketing.push.val` 配置文件属性存储在中？</li></ul> |

{style="table-layout:auto"}

## 按实体和产品知识问题列出的运营见解{#objects-questions}

以下问题按数据对象分组，并分类为 [运营洞察](./home.md#operational-insights) 或 [产品知识](./home.md#product-knowledge).

* **受众 — 运营分析**
   * 哪些受众使用其他受众？
   * 受众中用户档案数量的分布情况如何？
   * 显示上次修改时间早于以下时间的受众： {RELATIVE_DATE}.
   * 哪些受众具有0个配置文件？
   * 是 {USE_AUTO_COMPLETE_TO_FILL_AUDIENCE_NAME} 是否用于任何其他受众？
* **属性 — 运营分析**
   * 哪些受众具有xdm属性 {ATTRIBUTE_PATH} 在他们的区段定义中？
   * 任何受众中未使用多少XDM架构属性？
   * 哪些架构具有xdm属性 {ATTRIBUTE_PATH} 在里面？
   * 激活哪些XDM属性？
   * 具有超过10个配置文件的受众中使用哪些XDM属性？
* **数据流 — 运营见解**
   * 哪些数据流参与 {USE_AUTO_COMPLETE_TO_FILL_DATASET_NAME} 数据集？
   * 未使用哪些源数据流或者不再有数据进入？
   * 列出我具有的源数据流。
   * 为每个源连接器配置哪些数据流？
* **数据集 — 运营洞察**
   * 使用相同架构摄取了多少数据集？
   * 与哪个源连接器关联 {USE_AUTO_COMPLETE_TO_FILL_DATASET_NAME} 数据集？
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
   * 已在哪些历程中创建 {RELATIVE_DATE} （例如，上一周）或 {RELATIVE_DATE} （例如，特定日期之前/之后/日期）？
   * 显示在中修改的历程列表 {RELATIVE_DATE} （例如，上一周）或 {RELATIVE_DATE} （例如，特定日期之前/之后/日期）？
   * 列出我的实时历程。
   * 列出实时历程中使用的受众。
* **来源 — 运营分析**
   * 哪些源处于活动状态？
   * 哪个源连接器与数据集关联 {USE_AUTO_COMPLETE_TO_FILL_DATASET_NAME}.
   * 哪个源连接器的关联帐户数最多？
   * 显示数据流及其关联的源连接器。
* **有针对性的学习 — 产品知识(Real-Time CDP和Journey Optimizer)**
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
| <ul><li>指定要检索或分析的对象或信息。</li><li>尝试将数据对象名称放在引号中。 如果您只知道对象名称的一部分，则还可以在问题中指定该部分。</li><li>使用 [对象自动完成](./ui-guide.md#use-auto-complete) 以帮助AI Assistant更好地了解查询的上下文。</li></ul> | <ul><li>哪些数据集使用“Luma — 忠诚度”架构？</li><li>显示名称中包含“Luma”的激活区段。 按用户档案计数对其进行排名。</li></ul> |
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

## 后续步骤

通过阅读本文档，您现在了解了如何优化AI Assistant的问题。 有关如何在工作流中使用功能的信息，请阅读 [AI助手UI指南](ui-guide.md).
