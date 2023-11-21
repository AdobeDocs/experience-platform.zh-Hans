---
title: Adobe Experience Platform助理
description: 了解如何使用助手导航和了解Experience Platform和Real-time Customer Data Platform概念以及有关对象的使用信息。
badge: Alpha
hide: true
hidefromtoc: true
exl-id: 8be1c222-3ccd-4a41-978e-33ac9b730f8c
source-git-commit: a0395c4d3514693d3200571496eff47768da52ba
workflow-type: tm+mt
source-wordcount: '2183'
ht-degree: 0%

---

# Adobe Experience Platform助理

>[!NOTE]
>
>Adobe Experience Platform助手当前正在Alpha中。 该功能和文档可能会发生更改。

Adobe Experience Platform助手是一个UI功能，您可以使用它来导航和了解Experience Platform和Real-time Customer Data Platform概念以及有关您的对象的使用信息。

您可以查询“助手”以获取以下信息：

* 有关如何执行与数据和受众相关的任务的指南。
* 组织中现有数据对象的状态和量度。
* 用例示例和细微差别可更好地了解您的数据对象，包括属性、数据集、目标、架构、区段和源。

本文档提供了有关如何访问和使用Assistant来提问并获得有关Experience Platform和Real-Time CDP概念的答案的信息。

>[!BEGINSHADEBOX]

**助理如何工作？**

Assistant通过查询数据库并将数据库中的数据转换为人工可读的答案来回答您提交的问题。

这种底层数据的内部表示形式也称为知识图 — 一个包含给定答案的概念、数据和元数据的综合网络。

知识图由每次提交查询时引用的子图组成：

* 客户使用情况数据。
* 跨各种元存储区的客户使用情况数据。
* 文档Experience League。

在查询Assistant之前，需要考虑两类问题：

* **概念问题**：概念问题与数据或Adobe相关的受众概念有关。 概念问题的一些示例包括：
   * 批量分段与流式分段之间有何区别？
   * 是否有行业数据模型以及如何使用它们？
   * Real-Time CDP的最佳用途是什么？
* **使用问题**：使用问题与组织内的数据对象有关。 使用问题的一些示例包括：
   * 我有多少个数据集？
   * 有多少架构属性从未使用过？
   * 已激活哪些区段？

>[!ENDSHADEBOX]

## 用于在UI中Experience Platform的访问助手

您可以从Experience PlatformUI中的标题导航访问助手。

选择 **[!UICONTROL “助手”图标]** 从标题转到Launch Assistant面板。

![已选中带有助理图标的Experience PlatformUI主页。](./images/ai-assistant/ai-assistant.png)

<!-- +++Use immersive mode

To use [!DNL Immersive mode] select the focus icon in the header navigation of the Assistant.

![select-immersive](./images/ai-assistant/select-immersive.png)

A dedicated pop-up interface for Assistant appears at the center of your screen.

![immersive-mode](./images/ai-assistant/immersive-mode.png)

+++

From here, you can input your question in the text box and query Assistant for concepts regarding data or audiences. You can also ask questions about your data objects to better understand how you can use them for your respective use case.  -->

### 示例用例：使用助理加快模式创建过程 {#example-use-case}

>[!NOTE]
>
>以下示例工作流使用ExperienceEvent架构创建过程来说明在使用Experience PlatformUI时如何使用Assistant。

考虑要创建的用例 **设备交易事件架构**. 在ExperienceEvent架构创建过程中，您发现 `eventType` 字段。 此时，您可以离开工作流，并参阅上的文档 [架构组合的基础知识](../xdm/schema/composition.md)，或者您也可以使用助手即时获取问题的答案。

首先，在提供的文本框中输入您的问题。 在以下示例中，向助理提了一个问题：“**ExperienceEvent架构中的eventType字段是什么？**&quot;

![带有以下问题的Experience Platform助理已准备进行查询：“什么是ExperienceEvent架构中的eventType字段？](./images/ai-assistant/question.png)

然后，Assistant查询其知识库并计算答案。 几分钟后，助理会返回一个答案和相关建议，您可以将其用作跟进提示。

给定的答案提供指向任何引用实体的超链接。 在以下示例中，选择 **[!UICONTROL 架构]** 查看引用的架构的列表，或者 **[!UICONTROL 区段]** 以查看引用的区段的列表。

![带有上一个查询答案的Experience Platform助手。](./images/ai-assistant/answer.png)

Assistant允许您通过查看其源来验证答案。 提供了有关概念问题的文档链接，而数据使用问题可以通过演示如何计算答案的SQL查询进行验证。

![助理在返回答案后提供的选项。](./images/ai-assistant/options.png)

### 跟进问题 {#follow-up-question}

+++选择以查看后续问题的示例

您可以通过提出跟进问题来进一步了解有关特定主题的更多信息。 在下一个示例中，将询问助理如何将eventType用于分段。

![“Experience Platform助手”上显示的跟进问题和答案。](./images/ai-assistant/follow-up-question.png)

+++

### 数据使用问题 {#data-usage-question}

+++选择以查看数据使用问题的示例

您还可以向助理询问有关数据使用的问题。 在查询数据使用情况时，您必须位于活动沙盒中，以便助手回答您的查询。

对于涉及数据使用信息的响应， Assistant提供指向相关实体的链接。 此外，“助理”还会向您说明它如何计算其答案。

![一个数据使用问题，询问用户有多少区段。](./images/ai-assistant/data-usage-question.png)

+++

### 多圈 {#multi-turn}

+++选择以查看多圈示例

您可以使用“助理”的多轮功能在体验期间进行更自然的对话。 助理能够回答后续问题，因为上下文可以从以前的交互中推断出来。

在下面的示例中，要求助理列出组织中现有的区段，作为之前有关区段总数的查询的跟进。

![](./images/ai-assistant/multi-turn-one.png)

接下来，助理将收到另一个跟进请求。 此时，助理将通过列出按其各自大小排序的现有区段来进行响应。

![](./images/ai-assistant/multi-turn-two.png)

+++

### 使用自动完成 {#use-auto-complete}

+++选择以查看自动完成的示例

您可以使用自动完成函数接收沙盒中存在的数据对象列表。 自动完成推荐适用于以下域：区段、架构、数据集、源和目标。

要使用自动完成，请输入加号(**`+`**)。 或者，也可以选择加号(**`+`**)。 然后，将显示一个窗口，其中包含沙盒中存在的推荐数据对象列表。

![](./images/ai-assistant/autocomplete-options.png)

接下来，选择要查询的数据对象以完成问题，然后提交问题。

![](./images/ai-assistant/autocomplete-question.png)

+++

## 范围 {#scope}

助理可以回答有关Real-Time CDP和Experience Platform概念的问题，以及特定于您用户帐户的数据使用问题。 助理还可以根据您所在的UI页面推断上下文。 它可以识别：

* 您正在使用的用户帐户。
* 您所属的组织。
* 您在屏幕上查看的页面。
* 您在屏幕上查看的资源（包括类型和ID）。
* 鉴于您正在处理特定Experience Platform或Real-Time CDP工作流，因此助理可以推断您的意图。

### 文档 {#documentation}

目前，文档索引涵盖Adobe Experience Platform(Real-Time CDP和Audiences)。 索引会定期更新。

文档检索模型是根据Experience Platform(Real-Time CDP和Audiences)进行培训的。 Adobe Experience Platform范围之外的问题，例如，关于Adobe Target和Creative Cloud套件等其他Adobe产品的问题，无法回答。

### 数据使用 {#data-usage}

您还可以向Assistant询问有关以下域中的数据使用情况的问题：

* 属性
* 数据集
* 目标 _（有关帐户的问题和有关数据流的某些问题此时无法回答。）_
* 架构 _（有关字段组的问题目前无法回答。）_
* 区段
* 源 _（有关帐户的问题目前无法回答。）_

对于使用数据查询，答案可能不会反映UI的当前状态。 支持这些问题的数据每24小时更新一次。 例如，用户白天在Real-Time CDP中所做的更改会在晚上与数据存储同步，然后早上就可供用户提问了。 您可能需要将问题的格式设置为：“标题为的区段是什么时候 {TITLE} 创建时间？” 而不是“什么时候 {TITLE} 是否创建了区段？”

您需要登录沙盒以查询与对象（如架构、数据集、属性、目标和区段）相关的特定数据。

### 示例数据使用问题 {#example-data-usage-questions}

+++选择以查看示例数据使用问题列表

| 问题类型 | 描述 | 示例 |
| --- | --- | --- | 
| 数据族系 | 跨其他Experience Platform对象跟踪一个或多个对象的使用情况 | <ul><li>使用哪些数据集 {SCHEMA_NAME} 纲要？</li><li>使用相同架构摄取了多少数据集？</li><li>激活的区段中使用了哪些数据集？</li><li>列出具有激活区段中所用属性的架构。</li><li>显示激活的目标区段 {DESTINATION_ACCOUNT_NAME} 和超过1000个配置文件。</li><li>显示激活的区段中使用的属性，这些区段在2023年1月之后已修改。</li><li>通过什么摄取的数据集 {SOURCE_NAME}？</li><li>哪些数据流关联 {DATAFLOW_NAME}</li><li>列出与激活的区段相关且在过去1年中创建的架构。</li></ul> |
| 分发和聚合 | 有关Experience Platform对象使用情况的基于摘要的问题 | <ul><li>已激活区段的百分比是多少？</li><li>区段中使用了多少字段？</li><li>哪些区段激活到的目标数量最多？</li><li>列出重复的区段。</li><li>向我显示激活到的区段 {DESTINATION_ACCOUNT_NAME} 并按配置文件大小对其进行排名。</li><li>尚未激活但具有100个以上配置文件的区段的百分比是多少。 给我看看他们的名字。</li><li>列出将数据摄取到我的数据集中的3个源连接器。</li><li>根据激活区段中的出现情况，列出其中使用的前5个属性。</li></ul> |
| 对象查找 | 检索或访问Experience Platform对象或其属性。 | <ul><li>哪些数据集没有与其关联的任何架构</li><li>列出用于的属性 {SEGMENT_NAME}？</li><li>给我已启用配置文件但自创建后未修改的架构列表。</li><li>上周修改了哪些区段？</li><li>列出具有相同区段定义的区段及其创建日期。</li><li>哪些数据集启用了配置文件，并且还包括从每个数据集创建了多少区段。</li><li>哪些源帐户与数据集XYZ关联？</li><li>显示区段定义和修改日期 {SEGMENT_NAME}.</li></ul> |

+++

## 验证响应 {#verify-the-response}

可以使用多种不同的方式验证助理返回响应。

### 文档引用 {#citations}

每次响应时，“助理”都会为您提供引文，您可以参考这些引文进行验证或获取更多信息。

选择 **[!UICONTROL 显示源]** 以获取助手引用以计算其响应的文档的链接列表。 当您选择指向所引用文档的链接时，您将转到该特定页面的相关部分，并突出显示特定信息。

![指向“助手”中显示的源的链接。](./images/ai-assistant/show-sources.png)

## 提供反馈 {#feedback}

>[!BEGINSHADEBOX]

**已请求您的反馈**

在此Alpha阶段，邀请您对从助理收到的响应提供反馈。 所有答复和提出的反馈都经过审查，以继续改善助理的经验。

要提供反馈，请在收到助理的响应后选择竖起或竖下大拇指，然后在提供的文本框中输入反馈。 接下来，选择 **[!UICONTROL 提交反馈]** 以提交。

>[!ENDSHADEBOX]

+++提供反馈

>[!BEGINTABS]

>[!TAB 竖起大拇指]

选择竖起大拇指图标以就您在助手方面的良好体验提供反馈。

![正反馈窗口。](./images/ai-assistant/thumbs-up.png)

>[!TAB 拇指朝下]

选择向下缩略图图标，根据您使用助理的经验，提供可改进内容的反馈。 在此步骤中，您还可以提供关于您的体验的特定注释。 评论中提供的反馈每天进行审核。

![负反馈窗口。](./images/ai-assistant/thumbs-down.png)

>[!TAB 标志]

选择标志图标以提供有关使用助手体验的进一步报告。

![报告结果窗口。](./images/ai-assistant/flag.png)

>[!ENDTABS]

+++

## 其他信息 {#additional-information}

请参阅本节以了解有关Experience Platform助理的其他信息。

### 警告和限制 {#caveats-and-limitations}

以下部分概述了使用助手时要考虑的当前注意事项和限制。
<!-- 
#### Conversational experience

You must consider several nuances regarding the conversational experience when querying the Assistant.

>[!NOTE]
>
>These limitations are temporary and are being improved upon throughout the course of the alpha.

>[!BEGINTABS]

>[!TAB Unable to infer context from prior discussion]

The Assistant currently cannot reference prior discussions as context for a given question. See the table below for examples:

| Ambiguous question | Clear question | Note |
| --- | --- | --- |
| <ul><li>First question: "What is a segment?"</li><li>Follow up question: "Are there different types of them?"</li></ul>| <ul><li>First question: "What is a segment?"</li><li>Follow up question: "Are there different types of **segments**?"</li></ul> | The Assistant cannot infer what "them" means. |
| <ul><li>First question: "What is a segment?"</li><li>Follow up question: "Can you elaborate more?"</li></ul> | <ul><li>First question: "What is a segment?"</li><li>Follow up question: "Explain what a segment is in depth"</li></ul> | The Assistant cannot intelligently reference documentation based on "more". |
| <ul><li>First question: "What is a segment?"</li><li>Follow up question: "Can you give me an example of one?"</li></ul> | <ul><li>First question: "What is a segment?"</li><li>Follow up question: "Can you give me an example of a segment?"</li></ul> | The Assistant cannot infer what you want an example of.|
| <ul><li>First question: "What is a batch segment?"</li><li>Follow up question: "How does it compare to a streaming segment?"</li></ul> | <ul><li>First question: "What is a batch segment?"</li><li>Follow up question: "Can you compare a streaming segment to a batch segment?"</li></ul> | The Assistant cannot infer what "it" is referring to and thus cannot compare the streaming segment. |
| <ul><li>First question: "How many segments do I have?"</li><li>Follow up question: "How many of them use Facebook as a destination?"</li></ul> | <ul><li>First question: "How many segments do I have?"</li><li>Follow up question: "How many of the segments that I have are using Facebook as a destination?"</li></ul> | The Assistant is cannot infer what "them" is referring to. |

{style="table-layout:auto"}

>[!TAB Unable to infer context from a page]

When asking the Assistant about a particular element of the Experience Platform UI page that you are on, you must clearly define the specific element within your question. 

| Ambiguous question | Clear question | Note |
| --- | --- | --- |
| "What does this do?" | "What does {PAGE_NAME} do? | The Assistant cannot infer what "this" is referring to. You must provide the specific page element that you are querying about. |
| "Why won't it save?" | "Why can't I save a new sandbox called {NAME}?" | The Assistant cannot infer what "it" is referring to and cannot know that you are having issues with an entity. |

{style="table-layout:auto"}

Furthermore, the Assistant can only answer questions regarding error messages, given that the error is documented in Experience League.

>[!TAB Ambiguity]

You must phrase your questions clearly and scope them within a product, application, or domain, as the Assistant currently cannot disambiguate questions.

| Ambiguous question | Clear question | Note |
| --- | --- | --- |
| "How do I create a filter? | How do I create a filter in Profile Query Language? | You must specify the feature that which you are filtering for because a variety of Experience Platform features support filtering. |
| "How do I get started? | How do I get started using destinations? | You must provide clarity on your goals and use case because overly broad concepts may result in generic or unnecessarily specific answers. |

{style="table-layout:auto"}

>[!ENDTABS] -->

#### 限时闲聊

您可以与助理进行闲聊，但当前此能力有限。

#### 功能问题

助理可能会对自己的工作产生不准确的印象。 它可能会错误地回答以下类型的问题：

| 示例问题 | 注意 |
| --- | --- |
| “您能回答以下问题吗？ {ENTITY}？” | 只要助理能够在其索引中找到引用给定实体的单个页面，它就会响应“是”。 |
| “你知道吗 **x** 语言？” | 助理目前仅支持英语，但可能会回答“是”，因为底层模型能够支持它。 |
| “你能……” | “助理”可能会回答“是”，即使它不能。 |

### 提示 {#tips}

以下部分概述了使用助理时要考虑的一些提示和解决方法。

#### 可能会用错误的信息源回答问题

在某些情况下，您对使用情况数据的疑问会得到基于文档的回答。 这是因为Assistant可能会将您的问题错误地路由到错误的信息源。 您可以通过以下方式防止出现这种情况：

* 改写您的问题以使用更多类似于SQL的语言
* 显式调用要使用的信息源。

有关示例，请阅读下表：

| 错误的问题 | 好问题 | 注释 |
| --- | --- | --- |
| 我最大的细分市场是什么？ | 我最大的细分市场是什么？ 使用数据。 | 明确告知助理您希望答案基于数据。 |
| 我最大的细分市场是什么？ | 列出我最大的区段。 | 在某些情况下，“什么……”问题可能会被误认为基于文档的问题。 使用诸如“list”之类的命令更能说明您在上下文中对数据提出疑问。 |
| 我有多少个数据集？ | 计算我的数据集。 | 最初的问题适用于区段，但可能不适用于数据集。 |
