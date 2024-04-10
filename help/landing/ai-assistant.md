---
title: Adobe Experience Platform的人工智能助手
description: 了解如何使用AI Assistant导航和了解Experience Platform和Real-time Customer Data Platform概念以及有关您的对象的使用信息。
badge: Alpha
hide: true
hidefromtoc: true
exl-id: 8be1c222-3ccd-4a41-978e-33ac9b730f8c
source-git-commit: f38f528c421c7cbf7116cc0ee323e8e7dcde6292
workflow-type: tm+mt
source-wordcount: '2730'
ht-degree: 0%

---

# Adobe Experience Platform的人工智能助手

>[!NOTE]
>
> 适用于Adobe Experience Platform的AI助手当前正在Alpha中。 该功能和文档可能会发生更改。

AI助手是一种UI功能，可用于导航和了解Adobe Experience Platform和Real-time Customer Data Platform概念以及有关您的对象的使用信息。

您可以查询AI Assistant以获取以下信息：

* 有关如何执行与数据和受众相关的任务的指南。
* 组织中现有数据对象的状态和量度。
* 用例示例和细微差别以更好地了解您的数据对象，包括属性、受众、数据流、数据集、目标、架构和源。

阅读以下指南，了解如何使用AI Assistant帮助导航和了解您的Experience Platform和Real-Time CDP工作流。

>[!BEGINSHADEBOX]

**AI助手如何工作？**

AI Assistant通过查询数据库，然后将数据库中的数据转换为人类可读的答案来响应您提交的问题。

这种底层数据的内部表示形式也称为知识图 — 一个包含给定答案的概念、数据和元数据的综合网络。

知识图由每次提交查询时引用的子图组成：

* 客户使用情况数据。
* 跨各种元存储区的客户使用情况数据。
* 文档Experience League。

在查询AI Assistant之前，需要考虑两类问题：

* **概念问题**：概念问题与数据或Adobe相关的受众概念有关。 概念问题的一些示例包括：
   * 批量分段与流式分段之间有何区别？
   * 是否有行业数据模型以及如何使用它们？
   * Real-Time CDP的最佳用途是什么？
* **使用问题**：使用问题与组织内的数据对象有关。 使用问题的一些示例包括：
   * 我有多少个数据集？
   * 有多少架构属性从未使用过？
   * 已激活哪些受众？

>[!ENDSHADEBOX]

## 使用AI Assistant可以实现的目标

可以使用AI助手实现以下目标：

| 目标 | 描述 | 示例 |
| --- | --- | --- |
| 学习概念和持续工作流 | <ul><li>作为新手，您可以使用AI Assistant学习Real-Time CDP和Adobe Journey Optimizer概念，并熟悉不熟悉的产品和功能。</li><li>作为经验丰富的用户，您可以使用AI Assistant解决可能阻止工作流的边缘案例。 | <ul><li>如何在历程分析中设置功能板？</li><li>告诉我Real-Time CDP的一些用例。</li></ul> |
| 故障排除 | 使用AI Assistant了解如何调试工作流中可能遇到的基本错误。 | <ul><li>为什么会出现此错误 {ERROR_MESSAGE} 是刻薄吗？</li><li>为何无法删除名为“Luma：电子邮件受众”的受众？</li></ul> |
| 沙盒卫生 | 使用AI Assistant识别任何重复或未使用的对象，以便您能够有效地维护沙盒。 | <ul><li>能否向我显示类似的受众？</li><li>是否有任何没有关联数据集的架构？</li></ul> |
| 价值分析 | 使用AI Assistant识别您最常用的数据对象，评估任何绩效指标或找到最有价值的数据对象。 | <ul><li>我们的“Luma：电子邮件受众”区段定义中有多少个配置文件？</li><li>何时将受众激活到“Experience Cloud受众”目标？</li></ul> |
| 搜索 | 使用AI Assistant查找支持的Experience Platform对象，如受众、数据集、目标、架构和源。 | <ul><li>在名称中列出包含“Luma”的受众（在上季度创建）。</li><li>“Luma：自定义操作”XDM架构中有哪些属性？</li></ul> |
| 影响分析 | 使用AI Assistant识别某些工作流中使用的数据对象，以便您能够评估任何更改的影响。 | <ul><li>使用哪些受众 `homeAddress.city` 在“Luma：PersonProfiles”架构中？</li><li>哪些数据集是 `consents.marketing.push.val` 配置文件属性存储在中？</li></ul> |

## 在Experience PlatformUI中访问AI助手

要启动AI助手，请选择 **[!UICONTROL AI助手图标]** 从Experience PlatformUI的顶部标题中。

![Experience Platform主页，选中AI助手图标并打开AI助手界面。](./images/ai-assistant/ai-assistant.png)

此时将显示AI Assistant界面，它立即为您提供开始使用的信息。 您可以使用下提供的选项 [!UICONTROL 开始使用的想法] 回答问题和命令，例如：

* [!UICONTROL 激活了我的哪些受众？]
* [!UICONTROL 什么是架构？]
* [!UICONTROL 告诉我一些Real-Time CDP的常见用例]

![AI Assistant的“开始使用的想法”部分。](./images/ai-assistant/ideas-to-get-started.png)

要与AI Assistant交互，请使用输入框键入查询或命令。 您也可以使用(**`+`**)符号来使用自动完成功能和书签图标来访问您加入书签的查询和命令。

![AI Assistant输入框突出显示。](./images/ai-assistant/interact.png)

## 用例示例：使用AI Assistant加快模式创建过程

>[!NOTE]
>
>以下工作流是一个示例，它使用Experience Event架构创建过程来说明在使用Experience PlatformUI时如何使用AI Assistant。

考虑要创建的用例 **设备交易事件架构**. 在体验事件架构创建过程中，您遇到 `eventType` 字段。 “此时，您可以选择退出工作流并参阅 [架构组合的基础知识](../xdm/schema/composition.md) 文档，或者您可以使用AI助手检索问题的答案，并通过AI助手推荐的文档链接查找其他资源。”

首先，在提供的文本框中输入您的问题。 在下面的示例中，AI助手遇到以下问题：“**ExperienceEvent架构中的eventType字段是什么？**&quot;

![用于Experience Platform的AI助手，带有为查询准备的以下问题：“ExperienceEvent架构中的eventType字段是什么？](./images/ai-assistant/question.png)

然后，AI Assistant查询其知识库并计算答案。 片刻后，AI助手会返回一个答案和相关建议，您可以将其用作跟进提示。

![用于Experience Platform的AI助手，可回答上一个查询。](./images/ai-assistant/answer.png)

从AI助手收到响应后，您可以从多个选项中进行选择，以确定如何继续。

### 保存查询 {#save-your-query}

+++选择以查看如何保存查询的示例

要保存查询，请选择问题旁边的书签图标。

![选定书签的屏幕截图。](./images/ai-assistant/save-your-query.png)

要访问已保存的查询，请选择输入框下方的书签图标，然后选择要运行的查询。

![书签图标的屏幕截图和已保存查询的列表。](./images/ai-assistant/bookmarks.png)

+++

### 在沙盒中查看数据 {#view-data-in-your-sandbox}

+++选择以查看示例

根据您的查询，AI Assistant会提供有关沙盒中数据的其他信息。 要查看查询响应如何应用于沙盒，请选择 **[!UICONTROL 在您的沙盒中].**

在此步骤中，AI助手可以提供指向某些相关对象的UI页面的直接链接。 在以下示例中，AI Assistant提供到 [!UICONTROL 架构] 和 [!UICONTROL 区段] UI页面。

![“在您的沙盒中”选项的屏幕截图。](./images/ai-assistant/in-your-sandbox.png)

+++

### 验证响应 {#verify-the-response}

+++选择以查看如何显示源的示例

要查看引文并验证AI助理的响应，请选择 **[!UICONTROL 显示源]**. AI Assistant提供可证实其响应的文档的链接。 您还可以使用AI Assistant在下提供的查询 [!UICONTROL 相关建议] 以进一步浏览与原始查询相关的主题。

![“显示源”屏幕截图。](./images/ai-assistant/show-sources.png)

+++

### 数据使用和可视化 {#data-usage-and-visualization}

+++选择以查看数据使用问题和数据可视化图表的示例

要让AI Assistant响应有关您组织内数据使用情况的查询，您必须位于活动沙盒中。

在以下示例中，AI助手随以下查询一起提供： **“向我显示包含超过1000个配置文件的区段定义，并包含激活状态。”** 然后，AI Assistant会使用图表进行响应，该图表可视化您的区段和配置文件数据。

![跟进有关数据使用的问题。](./images/ai-assistant/data-usage-question.png)

您可以将鼠标悬停在单个栏上以查看特定数据。 您还可以选择展开图标以查看图表的大图。

![阐述数据可视化的后续问题。](./images/ai-assistant/data-visualization.png)

此时将显示可视化图表的展开视图。 您可以使用扩展模式进一步检查数据，当返回具有大量列的可视化图表时，扩展模式特别有用。

![扩展图表。](./images/ai-assistant/chart-expanded.png)

当出现数据使用问题提示时，AI Assistant会提供它如何计算答案的说明。 在以下示例中，AI Assistant概述了为显示具有1000多个用户档案的区段定义及其各自的激活状态而采取的步骤。

![跟进有关区段定义的问题，该问题说明AI Assistant如何计算答案。](./images/ai-assistant/results-explained.png)

您还可以为查询提供筛选器和修改，并且可以指示AI Assistant根据您包括的筛选器呈现其结果。 例如，您可以要求AI助手按其创建日期的顺序显示计数区段定义的趋势，删除总配置文件为零的区段定义，并在显示数据时使用月名称而不是整数。

+++

### 使用自动完成 {#use-auto-complete}

+++选择以查看自动完成的示例

您可以使用自动完成函数接收沙盒中存在的数据对象列表。 自动完成推荐适用于以下域：受众、架构、数据集、源和目标。

您可以通过包含加号(**`+`**)。 作为替代方法，您还可以选择加号(**`+`**)，它位于文本输入框底部。 此时将显示一个窗口，其中包含来自沙盒的推荐数据对象列表。

![自动完成示例](./images/ai-assistant/auto-complete-one.png)

接下来，选择要查询的数据对象以完成问题，然后提交问题。

![自动填写问题与答案的示例](./images/ai-assistant/auto-complete-two.png)

+++

### 使用多圈 {#use-multi-turn}

+++选择以查看多圈示例

您可以使用AI助手的多轮功能在体验期间进行更自然的对话。 给定情况下，AI助手能够回答后续问题。 该上下文可从较早的交互推断。

在下面的示例中，AI助理需要了解当前组织的数据流总数。

![多圈示例](./images/ai-assistant/multi-turn-one.png)

接下来，AI助手会收到另一个跟进请求。 这次，AI Assistant通过列出组织中当前存在的数据流进行响应。

![带问答的多圈示例](./images/ai-assistant/multi-turn-two.png)

+++

## 文档 {#documentation}

目前，文档索引涵盖Adobe Experience Platform(Real-Time CDP和Audiences)。 索引会定期更新。

文档检索模型是根据Experience Platform(Real-Time CDP和Audiences)进行培训的。 Adobe Experience Platform范围之外的问题，例如，关于Adobe Target和Creative Cloud套件等其他Adobe产品的问题，无法回答。

## 数据使用 {#data-usage}

您还可以向AI Assistant询问有关您在以下域中的数据使用情况的问题：

* 属性
* 受众
* 数据流
* 数据集
* 目标 _（有关帐户的问题和有关数据流的某些问题此时无法回答。）_
* 架构 _（有关字段组的问题目前无法回答。）_
* 源 _（有关帐户的问题目前无法回答。）_

对于使用数据查询，答案可能不会反映UI的当前状态。 支持这些问题的数据每24小时更新一次。 例如，用户白天在Real-Time CDP中所做的更改会在晚上与数据存储同步，然后早上就可供用户提问了。 您可能需要将问题的格式设置为：“标题为的受众是什么时候 {TITLE} 创建时间？” 而不是“什么时候 {TITLE} 是否创建了受众？”

您需要登录沙盒以查询与对象（如受众、架构、数据集、属性和目标）相关的特定数据。

### 示例数据使用问题 {#example-data-usage-questions}

+++选择以查看示例数据使用问题列表

| 问题类型 | 描述 | 示例 |
| --- | --- | --- | 
| 数据族系 | 跨其他Experience Platform对象跟踪一个或多个对象的使用情况 | <ul><li>使用哪些数据集 {SCHEMA_NAME} 纲要？</li><li>使用相同架构摄取了多少数据集？</li><li>激活的受众中使用了哪些数据集？</li><li>列出具有在激活受众中使用的属性的架构。</li><li>显示激活到的受众 {DESTINATION_ACCOUNT_NAME} 和超过1000个配置文件。</li><li>显示激活的受众中使用的属性，这些受众在2023年1月之后已修改。</li><li>通过什么摄取的数据集 {SOURCE_NAME}？</li><li>哪些数据流关联 {DATAFLOW_NAME}</li><li>列出与已激活受众相关且在过去1年创建的架构。</li></ul> |
| 分发和聚合 | 有关Experience Platform对象使用情况的基于摘要的问题 | <ul><li>激活的受众的百分比是多少？</li><li>区段中使用了多少字段？</li><li>哪些受众激活到的目标数量最多？</li><li>列出重复的受众。</li><li>显示激活到的受众 {DESTINATION_ACCOUNT_NAME} 并按配置文件大小对其进行排名。</li><li>尚未激活但具有100个以上配置文件的受众的百分比是多少。 给我看看他们的名字。</li><li>列出将数据摄取到我的数据集中的3个源连接器。</li><li>根据活跃受众的发生次数，列出其中使用的前5个属性。</li></ul> |
| 对象查找 | 检索或访问Experience Platform对象或其属性。 | <ul><li>哪些数据集没有与其关联的任何架构</li><li>列出用于的属性 {AUDIENCE_NAME}？</li><li>给我已启用配置文件但自创建后未修改的架构列表。</li><li>上周修改了哪些受众？</li><li>列出具有相同区段定义的受众及其创建日期。</li><li>哪些数据集启用了配置文件，并且还包括从每个数据集创建了多少受众。</li><li>哪些源帐户与数据集XYZ关联？</li><li>显示区段定义和修改日期 {AUDIENCE_NAME}.</li></ul> |

+++

## 提供反馈 {#feedback}

>[!BEGINSHADEBOX]

**已请求您的反馈**

在此Alpha阶段，邀请您就您从AI助手收到的响应提供反馈。 所有回复和提交的反馈都经过审查，以继续改进人工智能助理的经验。

要提供反馈，请在从AI助手收到响应后选择竖起或竖下大拇指，然后在提供的文本框中输入反馈。 接下来，选择 **[!UICONTROL 提交反馈]** 以提交。

>[!ENDSHADEBOX]

+++提供反馈

>[!BEGINTABS]

>[!TAB 竖起大拇指]

选择竖起大拇指图标可就您在AI助手方面的体验提出反馈。

![正反馈窗口。](./images/ai-assistant/thumbs-up.png)

>[!TAB 拇指朝下]

选择向下拇指图标，根据您使用AI助手时的经验提供可改进内容的反馈。 在此步骤中，您还可以提供关于您的体验的特定注释。 评论中提供的反馈每天进行审核。

![负反馈窗口。](./images/ai-assistant/thumbs-down.png)

>[!TAB 标志]

选择标志图标以提供关于您使用AI助手体验的进一步报告。

![报告结果窗口。](./images/ai-assistant/flag.png)

>[!ENDTABS]

+++

## 其他信息 {#additional-information}

请参阅本节以了解有关AIExperience Platform助手的其他信息。

### 警告和限制 {#caveats-and-limitations}

以下部分概述了使用AI助手时要考虑的当前注意事项和限制。

#### 限时闲聊

您可以与AI助手进行闲谈，但当前此功能有限。

#### 功能问题

AI助手可能会对其功能产生不准确的印象。 它可能会错误地回答以下类型的问题：

| 示例问题 | 注意 |
| --- | --- |
| “您能回答以下问题吗？ {ENTITY}？” | 只要AI助手能够在其索引中找到引用给定实体的单个页面，它就会响应“是”。 |
| “你知道吗 **x** 语言？” | AI助手当前仅支持英语，但可能会回答“是”，因为基础模型能够支持它。 |
| “你能……” | AI助手可能会回答“是”，即使它不能。 |

### 提示 {#tips}

以下部分概述了使用AI助手时应考虑的一些提示和解决方法。

#### 可能会用错误的信息源回答问题

在某些情况下，您对使用情况数据的疑问会得到基于文档的回答。 这是因为AI Assistant可能会将您的问题错误地路由到错误的信息源。 您可以通过以下方式防止出现这种情况：

* 改写您的问题以使用更多类似于SQL的语言
* 显式调用要使用的信息源。

有关示例，请阅读下表：

| 错误的问题 | 好问题 | 注释 |
| --- | --- | --- |
| 我最大的受众是什么？ | 我最大的受众是什么？ 使用数据。 | 明确告知AI助手，您希望答案基于数据。 |
| 我最大的受众是什么？ | 列出我最大的受众。 | 在某些情况下，“什么……”问题可能会被误认为基于文档的问题。 使用诸如“list”之类的命令更能说明您在上下文中对数据提出疑问。 |
| 我有多少个数据集？ | 计算我的数据集。 | 最初的问题适用于受众，但可能不适用于数据集。 |
