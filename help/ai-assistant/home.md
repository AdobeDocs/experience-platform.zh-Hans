---
title: Adobe Experience Platform中的AI助手概述
description: 了解 AI 助手、其细微差别和用例，以及如何使用它来通过 Adobe Experience Platform 和 Real-Time Customer Data Platform 加快工作流程。
exl-id: cfd4ac22-fff3-4b50-bbc2-85b6328f603c
source-git-commit: e90333d09585c8aa0ef176dcfc4717e86364fd54
workflow-type: tm+mt
source-wordcount: '927'
ht-degree: 15%

---

# Adobe Experience Platform的人工智能助手

以下视频旨在支持您了解AI助手。

>[!VIDEO](https://video.tv.adobe.com/v/3429845?learn=on)

请阅读本文档，了解Adobe Experience Platform中的AI助手。

Adobe Experience Platform 中的 AI 助手是一种对话体验，您可以使用它来加速 Adobe 应用程序中的工作流程。您可以使用 AI 助手更好地了解产品知识、解决问题或搜索信息并找到运营洞察。AI 助手支持 Experience Platform、Real-time Customer Data Platform、Adobe Journey Optimizer 和 Customer Journey Analytics。

![首次触发用户体验的AI助手界面。](./images/ai-assistant-full.png)

>[!IMPORTANT]
>
>在使用AI助手之前，必须同意[用户协议](https://www.adobe.com/legal/licenses-terms/adobe-dx-gen-ai-user-guidelines.html)。 用户协议还包含公共测试版协议。 这样一来，您便可以在以Beta版容量推出其他AI Assistant功能时使用。

+++选择以查看用户协议界面

![用户协议的第一页。](./images/user-agreement-1.png)

![用户协议的最后一页。](./images/user-agreement-2.png)

+++

## 了解AI助手 {#understanding-ai-assistant}

AI Assistant通过查询数据库，然后将数据库中的数据转换为人类可读的答案来响应您提交的问题。

基础数据的这种内部表示也称为&#x200B;**[!DNL Knowledge Graph]** — 给定答案的概念、数据和元数据的综合网络。

[!DNL Knowledge Graph]包含每次提交查询时引用的子图：

* 客户运营洞察。
* 跨各种元存储区的客户运营洞察。
* Experience League文档。

在查询AI Assistant之前，需要考虑两类问题：

### 产品知识 {#product-knowledge}

产品知识是指以Experience League文档为基础的概念和主题。 产品知识问题可进一步细分为以下子组：

| 产品知识 | 示例 |
| --- | --- |
| 点式学习 | <ul><li>标识与主键或外键之间有何区别？</li><li>什么是相似受众？</li></ul> |
| 打开发现 | <ul><li>如何导出此数据集？</li><li>是否有适用于医疗保健客户的架构？</li></ul> |
| 故障排除 | <ul><li>为何我无法打开Adobe拥有的架构以获取配置文件？</li><li>为什么无法删除区段？</li></ul> |

{style="table-layout:auto"}

观看以下视频，了解有关AI Assistant产品知识的更多信息：

>[!VIDEO](https://video.tv.adobe.com/v/3438032/?learn=on)

### 运营洞察 {#operational-insights}

操作分析是指回答AI Assistant生成的有关元数据对象（属性、受众、数据流、数据集、目标、历程、架构和源）的答案，包括计数、查找和谱系影响。 它不会查看沙盒中的任何数据。

* 我有多少个数据集？
* 有多少架构属性从未使用过？
* 已激活哪些受众？

您可以在以下域中向AI Assistant询问有关您的操作见解的问题：

| 域 | 支持的元数据 | 不支持的元数据 |
| --- | --- | --- |
| 属性 | <ul><li>属性名称搜索</li><li>属性 — 架构关系</li><li>属性 — 数据集关系</li><li>属性 — 受众关系</li><li>属性 — 目标关系</li></ul> | <ul><li>属性类</li><li>审核</li><li>弃用状态</li><li>标记</li><li>存储在属性中的值</li></ul> |
| 受众 | <ul><li>受众人数</li><li>受众类型（流式传输或批处理）</li><li>创建/修改日期</li><li>激活状态</li><li>轮廓计数</li><li>复制受众</li><li>受众定义搜索</li><li>受众 — 受众关系</li><li>受众 — 属性关系</li><li>受众 — 数据集关系</li><li>受众 — 目标关系</li><li>名称搜索</li><li>名称和ID搜索 | <ul><li>受众重叠</li><li>受众激活</li><li>受众 — 营销活动关系</li><li>审核</li><li>创建/修改</li><li>标记</li><li>配置文件资格趋势</li></ul> |
| 数据流 | <ul><li>数据流计数</li><li>数据流状态</li><li>数据流 — 数据集关系</li><li>数据流 — 源关系</li></ul> | <ul><li>创建/修改</li><li>数据流 — 批次关系</li><li>摄取配置文件计数</li></ul> |
| 数据集 | <ul><li>数据集计数</li><li>配置文件启用状态</li><li>创建/修改日期</li><li>数据集 — 架构关系</li><li>数据集 — 受众关系</li><li>数据集 — 属性关系</li><li>数据集 — 数据流关系</li><li>名称搜索 </li><li>名称和ID搜索</li></ul> | <ul><li>审核</li><li>创建者</li><li>数据集 — 批次关系</li><li>数据集创建/修改</li><li>数据集大小</li><li>配置文件数</li><li>行数</li><li>值搜索</li></ul> |
| 目标 | <ul><li>已配置的目标计数</li><li>目标 — 受众关系</li><li>目标属性关系</li></ul> | <ul><li>帐户设置</li><li>帐户凭据信息</li><li>独特配置文件已激活</li></ul> |
| 历程 | <ul><li>计数</li><li>名称搜索</li><li>名称和ID搜索</li><li>历程状态</li><li>触发状态（受众与事件）</li><li>创建/修改日期</li><li>循环频率</li></ul> | <ul><li>属性 — 历程关系</li><li>审核</li><li>创建/修改</li><li>创建者</li><li>活动</li><li>历程 — 数据集</li><li>历程 — 架构</li><li>产品建议</li><li>配置文件资格趋势</li><li>步骤事件</li></ul> |
| 架构 | <ul><li>架构计数</li><li>创建/修改日期</li><li>架构 — 属性关系</li><li>架构 — 数据集关系</li><li>架构 — 受众关系</li><li>配置文件启用状态</li><li>名称搜索</li><li>名称和ID搜索</li></ul> | <ul><li>审核</li><li>创建/修改</li><li>创建者</li><li>字段组</li><li>身份标识</li><li>身份标识命名空间</li><li>标记</li><li>配置文件数</li></ul> |
| 源 | <ul><li>帐户计数</li><li>帐户状态</li><li>每个帐户的活动/不活动数据流</li><li>Source连接器 — 数据流关系</li><li>Source帐户 — 数据流关系</li></ul> | <ul><li>帐户凭据信息</li><li>帐户设置</li><li>数据摄取量度</li><li>配置文件数</li><li>Source — 批处理关系</li></ul> |

{style="table-layout:auto"}

对于操作分析问题，答案可能不会反映UI的当前状态。 支持这些问题的数据每24小时更新一次。 例如，用户白天在Real-Time CDP中所做的更改会在晚上与数据存储同步，然后早上就可供用户提问了。 您需要登录沙盒以查询与对象相关的特定数据。

观看以下视频，了解有关AI助手操作见解的其他信息：

>[!VIDEO](https://video.tv.adobe.com/v/3444031?learn=on&enablevpops)

### 功能范围 {#feature-scope}

目前，人工智能助理的范围如下：

* [产品知识](./home.md#product-knowledge)： AI助手可以回答Experience Platform、Real-Time Customer Data Platform和Adobe Journey Optimizer的产品知识问题。 您还可以深入探讨Customer Journey Analytics的产品知识主题，但只能通过Customer Journey Analytics UI进行探讨。
* [操作分析](./home.md#operational-insights)：您可以向AI助手询问有关以下数据对象的操作分析的问题：属性、受众、数据流、数据集、目标、历程、架构和源。

## 后续步骤

现在您已大致了解AI助手，接下来可以在工作流中继续使用AI助手。 有关更多信息，请参阅以下文档：

* [AI助手UI指南](./ui-guide.md)
* [功能访问](./access.md)
* [问题指南](./questions.md)
* [AI助手中的隐私、安全和管理](./privacy.md)
* [常见问题解答](./faq.md)
