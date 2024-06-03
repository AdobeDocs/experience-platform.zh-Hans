---
title: Adobe Experience Platform中的AI助手概述
description: 了解AI Assistant、其细微差别和用例，以及如何使用它来加快您与Adobe Experience Platform和Real-time Customer Data Platform的工作流。
hide: true
hidefromtoc: true
source-git-commit: fe87a487079f5154f238b2d425cdd249a4724762
workflow-type: tm+mt
source-wordcount: '2294'
ht-degree: 0%

---

# Adobe Experience Platform的人工智能助手

请阅读本文档，了解Adobe Experience Platform中的AI助手。

Adobe Experience Platform中的AI助手是一种对话体验，可用于加快Adobe应用程序中的工作流程。 您可以使用AI Assistant更好地了解产品知识、排除问题或搜索信息并查找运营见解。 AI Assistant支持Experience Platform、Real-time Customer Data Platform、Adobe Journey Optimizer和Customer Journey Analytics。

>[!IMPORTANT]
>
>* 您必须同意 [用户协议](https://adobe.sharepoint.com/:w:/s/ExCUserExperience/EVzJv1jFBiZGnaFEufsfIqwBC_9ehv3KaXTkEMTGpQFRpg?e=qzwOo8) 才能使用AI助手。 用户协议还包含公共测试版协议。 这样一来，您便可以在以Beta版容量推出其他AI Assistant功能时使用。

![首次触发用户体验的AI Assistant界面。](./images/blank.png)

## 了解AI助手 {#understanding-ai-assistant}

AI Assistant通过查询数据库，然后将数据库中的数据转换为人类可读的答案来响应您提交的问题。

这种底层数据的内部表示形式也称为 **[!DNL Knowledge Graph]**  — 一个包含给定答案的概念、数据和元数据的综合网络。

此 [!DNL Knowledge Graph] 由提交查询时引用的子图组成：

* 客户运营洞察。
* 跨各种元存储区的客户运营洞察。
* 文档Experience League。

在查询AI Assistant之前，需要考虑两类问题：

### 产品知识 {#product-knowledge}

产品知识是指以Experience League文档为基础的概念和主题。 产品知识问题可进一步细分为以下子组：

| 产品知识 | 示例 |
| --- | --- |
| 点式学习 | <ul><li>标识与主键或外键之间有何区别？</li><li>如何计算配置文件丰富度？</li></ul> |
| 打开发现 | <ul><li>如何导出此数据集？</li><li>是否有适用于医疗保健客户的架构？</li></ul> |
| 故障排除 | <ul><li>为何我无法打开Adobe拥有的架构以访问配置文件？</li><li>为什么无法删除区段？</li></ul> |

{style="table-layout:auto"}

### 运营见解 {#operational-insights}

>[!IMPORTANT]
>
>操作见解答案为测试版。 任何有权访问 **查看运营分析** 权限将有权访问操作见解答案。

操作分析是指回答AI Assistant生成的有关元数据对象（属性、受众、数据流、数据集、目标、历程、架构和源）的答案，包括计数、查找和谱系影响。 它不会查看沙盒中的任何数据。

* 我有多少个数据集？
* 有多少架构属性从未使用过？
* 已激活哪些受众？

您可以在以下域中向AI Assistant询问有关您的操作见解的问题：

* 属性
* 受众
* 数据流
* 数据集
* 目标 _（有关帐户的问题和有关数据流的某些问题此时无法回答。）_
* 历程
* 架构 _（有关字段组的问题目前无法回答。）_
* 源 _（有关帐户的问题目前无法回答。）_

对于操作分析问题，答案可能不会反映UI的当前状态。 支持这些问题的数据每24小时更新一次。 例如，用户白天在Real-Time CDP中所做的更改会在晚上与数据存储同步，然后早上就可供用户提问了。 您需要登录沙盒以查询与对象相关的特定数据。

## 功能访问 {#feature-access}

对AI Assistant的访问受以下参数控制：

* **访问应用程序：** 您可以在Adobe Experience Platform、Adobe Real-Time CDP、Adobe Journey Optimizer和 [Customer Journey Analytics](https://experienceleague.adobe.com/en/docs/analytics-platform/using/ai-assistant).
* **合同访问：** 贵公司必须同意以下条款 [!DNL GenAI] — 相关法律条款，贵组织才能使用AI助手。 如果您无法访问AI助手，请联系贵组织的管理员或Adobe帐户团队。
* **权限：** 使用 [权限UI](../access-control/abac/ui/permissions.md) 授予或撤销对贵组织中AI助理的访问权限。 要使用AI助手，给定用户必须属于使用 **启用AI助手** 和 **查看运营分析** 权限。
   * 作为管理员，您可以添加 **启用AI助手** 并将用户添加到给定角色，以允许用户访问组织中的AI助手。
   * 作为管理员，您可以添加 **查看运营分析** 将用户添加到给定角色中，以让他们使用AI助手的操作分析功能。 操作见解当前为测试版。

![具有给定角色中包含的启用AI助手和查看操作分析权限的权限UI页面。](./images/permissions.png)

## 示例问题 {#example-questions}

此部分概述可在工作流中参考的示例问题。 这些问题分为三个部分：运营见解、目标和对象。

### 按运营分析分组的示例问题 {#operational-insights-questions}

+++选择以查看操作分析问题的示例及其各自的用例：

| 问题类型 | 用例 | 示例 |
| --- | --- | --- | 
| 数据族系 | 跨其他Experience Platform对象跟踪一个或多个对象的使用情况 | <ul><li>哪些数据集使用“ACME架构”架构？</li><li>使用相同架构摄取了多少数据集？</li><li>激活的受众中使用了哪些数据集？</li><li>列出具有在激活受众中使用的属性的架构。</li><li>显示激活到“ACME目标”且具有1000多个配置文件的受众。</li><li>显示激活的受众中使用的属性，这些受众在2023年1月之后已修改。</li><li>通过“ACME Amazon S3”源摄取的数据集是什么？</li><li>哪些数据流与“ACME忠诚度数据流”相关联？</li><li>列出与已激活受众相关且在过去1年创建的架构。</li></ul> |
| 分发和聚合 | 有关Experience Platform对象使用情况的基于摘要的问题 | <ul><li>激活的受众的百分比是多少？</li><li>区段中使用了多少字段？</li><li>哪些受众激活到的目标数量最多？</li><li>列出重复的受众。</li><li>显示激活到“ACME目标”的受众，并按用户档案大小对其进行排名。</li><li>尚未激活但具有100个以上配置文件的受众的百分比是多少。 给我看看他们的名字。</li><li>列出将数据摄取到我的数据集中的3个源连接器。</li><li>根据活跃受众的发生次数，列出其中使用的前5个属性。</li></ul> |
| 对象查找 | 检索或访问Experience Platform对象或其属性。 | <ul><li>哪些数据集没有与其关联的任何架构</li><li>列出用于“ACME受众”的属性？</li><li>给我已启用配置文件但自创建后未修改的架构列表。</li><li>上周修改了哪些受众？</li><li>列出具有相同区段定义的受众及其创建日期。</li><li>哪些数据集启用了配置文件，并且还包括从每个数据集创建了多少受众。</li><li>哪些源帐户与数据集XYZ关联？</li><li>显示“ACME受众”的区段定义和修改日期。</li></ul> |
| 对象比较 | 识别重复的受众。 | <ul><li>根据其区段定义，列出重复的受众。</li><li>哪些重复受众激活到“ACME目标”。</li></ul> |

{style="table-layout:auto"}

+++

### 按目标分组的示例问题 {#objectives-questions}

+++选择此选项可查看可使用AI助手完成的目标列表

| 目标 | 描述 | 示例 |
| --- | --- | --- |
| 学习概念和持续工作流 | <ul><li>作为新手，您可以使用AI Assistant学习Real-Time CDP和Adobe Journey Optimizer概念，并熟悉不熟悉的产品和功能。</li><li>作为经验丰富的用户，您可以使用AI Assistant解决可能阻止工作流的边缘案例。 | <ul><li>如何在历程分析中设置功能板？</li><li>告诉我Real-Time CDP的一些用例。</li></ul> |
| 故障排除 | 使用AI Assistant了解如何调试工作流中可能遇到的基本错误。 | <ul><li>为什么会出现此错误 {ERROR_MESSAGE} 是刻薄吗？</li><li>为何无法删除名为“Luma：电子邮件受众”的受众？</li></ul> |
| 沙盒卫生 | 使用AI Assistant识别任何重复或未使用的对象，以便您能够有效地维护沙盒。 | <ul><li>能否向我显示类似的受众？</li><li>是否有任何没有关联数据集的架构？</li></ul> |
| 价值分析 | 使用AI Assistant识别您最常用的数据对象，评估任何绩效指标或找到最有价值的数据对象。 | <ul><li>我们的“Luma：电子邮件受众”区段定义中有多少个配置文件？</li><li>何时将受众激活到“Experience Cloud受众”目标？</li></ul> |
| 搜索 | 使用AI Assistant查找支持的Experience Platform对象，如受众、数据集、目标、架构和源。 | <ul><li>在名称中列出包含“Luma”的受众（在上季度创建）。</li><li>“Luma：自定义操作”XDM架构中有哪些属性？</li></ul> |
| 影响分析 | 使用AI Assistant识别某些工作流中使用的数据对象，以便您能够评估任何更改的影响。 | <ul><li>使用哪些受众 `homeAddress.city` 在“Luma：PersonProfiles”架构中？</li><li>哪些数据集是 `consents.marketing.push.val` 配置文件属性存储在中？</li></ul> |

{style="table-layout:auto"}

+++

### 按对象分组的示例问题 {#objects-questions}

+++选择此选项可查看AI助手可以帮助您解决的示例问题列表：

| 对象 | 描述 |
| --- | --- |
| 受众 — 运营分析 | <ul><li>哪些受众使用其他受众？</li><li>受众中用户档案数量的分布情况如何？</li><li>显示上次修改于以下日期之前的受众： {RELATIVE_DATE}.</li><li>哪些受众具有0个配置文件？</li><li>是 {USE_AUTOCOMPLETE_TO_FILL_AUDIENCE_NAME} 是否用于任何其他受众？</li></ul> |
| 属性 — 运营分析 | <ul><li>哪些受众具有XDM属性 {ATTRIBUTE_PATH} 在他们的区段定义中？</li><li>任何受众中未使用多少XDM架构属性？</li><li>哪些架构具有XDM属性 {ATTRIBUTE_PATH} 在里面？</li><li>激活哪些XDM属性？</li><li>具有超过10个配置文件的受众中使用哪些XDM属性</li></ul> |
| 数据流 — 运营见解 | <ul><li>哪些数据流参与 {DATASET_NAME} 数据集？</li><li>未使用哪些源数据流或者不再有数据进入？</li><li> |
| 数据集 — 运营洞察 | <ul><li>使用相同架构摄取了多少数据集？</li><li>与哪个源连接器关联 {DATASET_NAME} 数据集></li><li>每个受众使用哪些数据集？</li><li>哪些架构未在任何数据集中使用？</li><li>我有多少个数据集？</li></ul> |
| 目标 — 运营分析 | <ul><li>哪些目标处于活动状态？</li><li>哪些目标帐户激活了0个受众？</li><li> |
| 历程 — 运营分析 | <ul><li>我有多少个历程？</li><li>已在哪些历程中创建 {RELATIVE_DATE} （例如，上周）或 {RELATIVE_DATE} （例如，特定日期之前/之后/日期）？</li><li>显示在中修改的历程列表 {RELATIVE_DATE} （例如，上周）或 {RELATIVE_DATE} （例如，特定日期之前/之后/日期）？</li><li>列出我的历程。</li><li>列出实时历程中使用的受众。</li></ul> |
| 架构 — 运营见解 | <ul><li>哪些架构的字段对受众的贡献最大？</li><li>有多少个架构启用了配置文件？</li><li>列出上周修改的所有架构。</li><li>哪些架构未在任何数据集中使用？</li><li>列出上周创建的所有架构。</li></ul> |
| 来源 — 运营分析 | <ul><li>哪些源处于活动状态？</li><li>哪个源连接器与数据集关联 {DATASET_NAME}？</li><li>哪个源连接器的关联帐户数最多？</li><li>显示数据流及其关联的源连接器。</li></ul> |
| 有针对性的学习 — 产品知识(Real-Time CDP和Journey Optimizer) | <ul><li>AI Assistant可以帮助做什么？</li><li>哪些受众具有相似性？</li><li>用户组与角色有何关系？</li><li>什么时候应该使用数据类型而不是字段组？</li><li>标识与主键或外键之间有何区别？</li><li>如何计算配置文件丰富度？</li></ul> |
| 故障排除 — 产品知识(Real-Time CDP和Journey Optimizer) | <ul><li>AI Assistant可以帮助做什么？</li><li>我能否在摄取数据后删除启用配置文件的架构？</li><li>为何无法删除受众？</li><li>评估受众和获得定位结果需要多长时间？</li></ul> |

{style="table-layout:auto"}

+++

## 用短语表述您的问题 {#phrasing-your-questions}

您必须清晰而有条理地向AI Assistant表达您的问题，以便获得尽可能准确的响应。 请参阅以下提示列表，以获取有关如何根据上下文提出明确问题的指导：

* 以简洁的方式陈述您的任务和/或问题。
* 避免使用模糊的语言或过于复杂的语法以促进理解。
* 提供关于您的任务和/或问题的相关上下文，因为上下文可以帮助AI助手生成更相关的响应。

请阅读下表，了解在向AI助手提问时应遵循的最佳实践的进一步指导。

+++选择以查看在提问时要遵循的最佳实践示例

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

+++

## 后续步骤

现在您已大致了解AI助手，接下来可以在工作流中继续使用AI助手。 有关更多信息，请参阅以下文档：

* [AI助手UI指南](./ui-guide.md)
* [AI助手中的隐私、安全和管理](./privacy.md)
* [常见问题解答](./faq.md)