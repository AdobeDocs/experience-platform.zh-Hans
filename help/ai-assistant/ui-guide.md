---
title: Adobe Experience Platform的人工智能助手
description: 了解如何使用AI Assistant导航和了解Experience Platform和Real-time Customer Data Platform概念以及有关您的对象的使用信息。
source-git-commit: 0820ba0f14e9eae5d89cd48490b1af5f9afcda70
workflow-type: tm+mt
source-wordcount: '1223'
ht-degree: 0%

---

# AI助手UI指南

阅读本指南，了解如何在Adobe Experience Platform UI中使用AI助手。

## 在Experience PlatformUI中访问AI助手

要启动AI助手，请选择 **[!UICONTROL AI助手图标]** 从Experience PlatformUI的顶部标题中。

![Experience Platform主页，选中AI助手图标并打开AI助手界面。](./images/ai-assistant.png)

此时将显示AI Assistant界面，它立即为您提供开始使用的信息。 您可以使用下提供的选项 [!UICONTROL 开始使用的想法] 回答问题和命令，例如：

* [!UICONTROL 激活了我的哪些受众？]
* [!UICONTROL 什么是架构？]
* [!UICONTROL 告诉我一些Real-Time CDP的常见用例]

## AI助手UI指南

>[!NOTE]
>
>以下工作流是一个示例，它使用Experience Event架构创建过程来说明在使用Experience PlatformUI时如何使用AI Assistant。

考虑要创建的用例 **设备交易事件架构**. 在体验事件架构创建过程中，您遇到 `eventType` 字段。 “此时，您可以选择退出工作流并参阅 [架构组合的基础知识](../xdm/schema/composition.md) 文档，或者您可以使用AI助手检索问题的答案，并通过AI助手推荐的文档链接查找其他资源。”

首先，在提供的文本框中输入您的问题。 在下面的示例中，AI助手遇到以下问题：“**ExperienceEvent架构中的eventType字段是什么？**&quot;

![用于Experience Platform的AI助手，带有为查询准备的以下问题：“ExperienceEvent架构中的eventType字段是什么？](./images/question.png)

然后，AI Assistant查询其知识库并计算答案。 片刻后，AI助手会返回一个答案和相关建议，您可以将其用作跟进提示。

![用于Experience Platform的AI助手，可回答上一个查询。](./images/answer.png)

从AI助手收到响应后，您可以从多个选项中进行选择，以确定如何继续。

### AI Assistant功能 {#features}

此部分概述在Experience Platform工作流中可以使用的AI Assistant的各种功能。

### 查看操作数据对象 {#view-operational-data-objects}

根据您的查询，AI Assistant会提供有关沙盒中数据的其他信息。 要查看查询响应如何应用于您的特定沙盒，请选择 **[!UICONTROL 在您的沙盒中].**

在查看与沙盒相关的数据时，AI Assistant可能会提供显示查询数据的特定UI页面的直接链接。

+++选择以查看示例

在此示例中，AI Assistant返回有关沙盒中现有XDM架构的其他信息，包括它们的总计数和五个最常用的字段。

![将打开“在沙盒中”下拉窗口，显示有关架构的其他信息。](./images/in-your-sandbox.png)

+++

### 查看引文 {#view-citations}

您可以通过查看每个产品知识答案中可用的引文来验证AI助手返回给您的响应。

+++选择以查看如何显示源的示例

要查看引文并验证AI助理的响应，请选择 **[!UICONTROL 显示源]**.

![已选择“显示源”的AI助手响应。](./images/show-sources.png)

AI Assistant会更新界面，并为您提供可证实初始响应的文档的链接。 此外，启用引用后，AI Assistant将更新响应以包含脚注，以指示引用所提供文档的答案的特定部分。

![AI Assistant提供的概念问题引文的下拉菜单。](./images/citations.png)

您还可以使用AI Assistant在下提供的建议 **[!UICONTROL 相关建议]** 以进一步探讨与您最初的问题相关的主题。

![AI助理提供的建议列表。](./images/related-suggestions.png)

+++

### 运营见解 {#operational-insights}

您必须在活动的沙盒中，以便AI Assistant能够充分响应有关您的操作见解的问题。

+++选择以查看操作分析问题的示例

在下面的示例中，AI助手被询问以下查询： **“向我显示使用Amazon S3源创建的数据流”**， AI助手随后会使用一个表进行响应，该表列出了您的数据流及其对应的ID。 要查看整个数据表，请选择右上角的展开图标。

![跟进有关运营见解的问题。](./images/usage-data-question.png)

此时将显示表的展开视图，其中会根据查询参数为您提供更加全面的数据流列表。

![展开表的视图。](./images/table.png)

当出现操作见解问题提示时，AI Assistant会提供有关如何计算答案的解释。 在以下示例中，AI Assistant概述了为识别使用创建的数据流而采取的步骤。 [!DNL Amazon S3] 源。

![跟进有关区段定义的问题，该问题说明AI Assistant如何计算答案。](./images/answer-explained.png)

您还可以提供筛选器和修改问题，并可以指示AI助手根据您包括的筛选器呈现其结果。 例如，您可以要求AI Assistant按区段定义的创建日期顺序显示区段定义计数的趋势，删除总配置文件为零的区段定义，并在显示数据时使用月名称而不是整数。

+++

### 使用自动完成 {#use-auto-complete}

您可以使用自动完成函数接收沙盒中存在的数据对象列表。 自动完成推荐适用于以下域：受众、架构、数据集、源和目标。

+++选择以查看自动完成的示例

您可以通过包含加号(**`+`**)。 作为替代方法，您还可以选择加号(**`+`**)，它位于文本输入框底部。 此时将显示一个窗口，其中包含来自沙盒的推荐数据对象列表。

![自动完成示例](./images/autocomplete.png)

+++

### 使用多圈 {#use-multi-turn}

您可以使用AI助手的多轮功能在体验期间进行更自然的对话。 给定情况下，AI助手能够回答后续问题。 该上下文可从较早的交互推断。

+++选择以查看多圈示例

在下面的示例中，首先要求AI助手提供数据流的总数，然后要求列出最近的10个数据流。

![多圈示例](./images/multi-turn.png)

+++

## 提供反馈 {#feedback}

您可以使用应答中提供的选项针对AI助手体验提供反馈。

要提供反馈，请在从AI助手收到响应后选择向上拇指、向下拇指或标记，然后在提供的文本框中输入反馈。

![AI助手中的反馈选项。](./images/provide-feedback.png)

要重置，请选择省略号(**`...`**)，然后选择 **[!UICONTROL 开始新对话]**. 这会告知AI助手，您打算更改主题，在对失败或引用不正确信息的查询进行故障诊断时尤其有用。

+++选择以查看更多示例

>[!BEGINTABS]

>[!TAB 竖起大拇指]

选择竖起大拇指图标可就您在AI助手方面的体验提出反馈。

![正反馈窗口。](./images/thumbs-up.png)

>[!TAB 拇指朝下]

选择向下拇指图标，根据您使用AI助手时的经验提供可改进内容的反馈。 在此步骤中，您还可以提供关于您的体验的特定注释。 评论中提供的反馈每天进行审核。

![负反馈窗口。](./images/thumbs-down.png)

>[!TAB 标志]

选择标志图标以提供关于您使用AI助手体验的进一步报告。

![报告结果窗口。](./images/flag.png)

>[!ENDTABS]

+++