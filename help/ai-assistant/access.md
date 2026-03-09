---
title: 访问Experience Platform中的AI助手（旧版）
description: 了解如何在Experience Cloud UI中访问AI助手。
exl-id: c4cdff25-512c-4b4c-be91-ad9360067a0a
source-git-commit: 077c42f2190316a00168bbeca685c08677c2b13a
workflow-type: tm+mt
source-wordcount: '876'
ht-degree: 0%

---

# 访问Experience Platform中的AI助手（旧版）

>[!IMPORTANT]
>
>本文档适用于AI助手（旧版）。 有关AI助手（下一代）的信息，请阅读Experience Cloud [文档中](https://experienceleague.adobe.com/zh-hans/docs/experience-cloud-ai/experience-cloud-ai/ai-assistant/ai-assistant-ui)AI的[AI助手UI指南](https://experienceleague.adobe.com/zh-hans/docs/experience-cloud-ai/experience-cloud-ai/home)。

请参阅下表比较AI助手（旧版）和AI助手（下一代）：

| 功能区域 | AI助手（旧版） | AI助手（新一代） |
| --- | --- | --- |
| 用户体验 | AI助手（旧版）仅在右边栏面板中可用。 | AI助手（新一代）在右边栏面板和沉浸式全屏体验中均可用。 |
| 功能范围 | 您可以将AI助手（旧版）用于产品知识和操作见解。 | 您可以使用AI Assistant（新一代）来获取产品知识、运营见解以及高级代理技能和多步骤任务执行。 |
| 平台架构 | AI助手（旧版）不是在Agent Orchestrator栈栈上构建的。 | AI Assistant （下一代）由[Adobe Experience Platform Agent Orchestrator](https://experienceleague.adobe.com/zh-hans/docs/experience-cloud-ai/experience-cloud-ai/agents/agent-orchestrator)提供支持，支持可扩展性和功能间的高级协调。 |
| 应用范围 | AI Assistant（旧版）是一种特定于应用程序的实施。 | 您可以使用AI Assistant（下一代）在所有Adobe Experience Cloud应用程序中实现统一的AI Assistant体验。 |
| 访问和权限模型 | 应用程序范围的访问模型与各个产品边界保持一致。 | 所有用户均可访问AI Assistant（下一代）和相关的Experience Platform代理。 **注释**： <ul><li>**Adobe Experience Manager**：您的管理员必须授予您通过[Adobe Admin Console](https://helpx.adobe.com/cn/enterprise/using/admin-console.html)访问AI助手（下一代）的权限。</li><li>**Customer Journey Analytics**：您的管理员必须通过[Customer Journey Analytics访问控制](https://experienceleague.adobe.com/zh-hans/docs/analytics-platform/using/technotes/access-control?lang=en)授予您访问AI助手权限。 这允许您提问产品知识和数据见解问题。 |

您可以在Adobe Experience Cloud中的多个应用程序中访问AI助手（旧版）。

>[!NOTE]
>
>如果您在权限UI中收到弹出消息，通知您组织必须首先同意其他法律条款才能访问AI助手（旧版），请联系您的Adobe客户团队以获得这些条款的指导。

## 快速入门 {#get-started}

在访问AI Assistant（旧版）之前，您必须完成两个先决步骤。

1. 贵组织必须首先同意法律条款。 有关更多信息，请与您的Adobe客户团队联系。
2. 管理员必须向您授予足够权限才能访问AI助手（旧版）。

如果您没有完成这两个先决条件步骤中的任何一个，则当您在Experience Platform UI中选择AI助手（旧版）聊天图标时，将会看到以下消息。

>[!BEGINTABS]

>[!TAB 您的组织无法使用AI助手（旧版）]

如果您使用的组织在法律上不具备使用AI助手（旧版）的资格，您将看到以下消息。 在这种情况下，您必须联系Adobe客户团队以解决访问权限问题。

![如果组织无法使用AI助手（旧版），则在Experience Platform UI上显示的弹出消息。](./images/access/modal-one.png)

>[!TAB 您没有正确的权限]

如果您的组织在法律上符合使用AI助手（旧版）的资格，但仍无法访问该功能，则您将在Experience Platform UI上看到以下消息。 这种情况意味着您没有足够的权限访问该功能，因此必须联系管理员以解决权限问题。

![如果您没有AI助手（旧版）的必要权限，Experience Platform UI上显示的弹出消息。](./images/access/modal-two.png)

>[!ENDTABS]

## 访问AI助手（旧版） {#get-access-to-ai-assistant}

对AI助手（旧版）的访问受以下参数控制：

* **访问应用程序：**&#x200B;您可以在Adobe Experience Platform、Adobe Real-Time CDP、Adobe Journey Optimizer和[Customer Journey Analytics](https://experienceleague.adobe.com/zh-hans/docs/analytics-platform/using/ai-assistant)中访问AI助手（旧版）。
<!-- * **Contractual access:** Your company must agree to certain [!DNL GenAI]-related legal terms before your organization can use AI Assistant (Legacy). Contact your organization's administrator or your Adobe Account Team if you are not able to access AI Assistant (Legacy).  -->
* **权限：**&#x200B;使用[权限UI](../access-control/abac/ui/permissions.md)授予或撤销对贵组织中的AI助手（旧版）的访问权限。 要使用AI助手（旧版），给定用户必须属于设置了&#x200B;**启用AI助手**&#x200B;和&#x200B;**查看操作分析**&#x200B;权限的角色。
   * 作为管理员，您可以将&#x200B;**启用AI助手**&#x200B;添加到给定角色，并将用户添加到该角色，以便他们能够访问您组织中的AI助手（旧版）。 **注意**：此权限允许所述用户访问AI助手（旧版），它不授予他们任何管理能力，因此不会授予其他人访问AI助手（旧版）的权限。
   * 作为管理员，您可以将&#x200B;**查看运营分析**&#x200B;添加到给定角色，并将用户添加到该角色，以便他们能够使用AI助手（旧版）的操作分析功能。

使用[权限UI](../access-control/abac/ui/roles.md)授予在Experience Platform和Journey Optimizer中使用AI助手（旧版）的权限。 有关如何在Customer Journey Analytics中访问AI助手（旧版）的信息。 阅读[Customer Journey Analytics](https://experienceleague.adobe.com/zh-hans/docs/analytics-platform/using/ai-assistant)中的文档。

![具有给定角色中包含的“启用AI助手（旧版）”和“查看操作分析”权限的权限UI页面。](./images/access/access-permissions.png)

获得必要权限后，您可以通过选择正在使用的应用程序顶部标题上的AI助手（旧版）图标来访问AI助手（旧版）。

![具有首次用户体验的AI助手（旧版）。](./images/access/access-home.png)

观看以下视频，了解如何为组织和用户配置对AI助手（旧版）的访问权限。

>[!VIDEO](https://video.tv.adobe.com/v/3436470/?learn=on)

## 后续步骤

一旦您拥有对AI助手（旧版）的完全访问权限，您便可以在工作流中继续使用该功能，请阅读[AI助手（旧版）UI指南](./ui-guide.md)以了解更多信息。
