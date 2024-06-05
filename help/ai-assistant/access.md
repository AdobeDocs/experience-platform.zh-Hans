---
title: 访问Experience Platform中的AI助手
description: 了解如何在Experience CloudUI中访问AI助手。
source-git-commit: b51291e6c3663c6d6e6d416f0d2c37563c852155
workflow-type: tm+mt
source-wordcount: '341'
ht-degree: 0%

---

# 访问Experience Platform中的AI助手

您可以在Adobe Experience Cloud中的多个应用程序中访问AI Assistant。

>[!IMPORTANT]
>
>如果您在权限UI中收到弹出消息，通知您组织必须首先同意其他法律条款才能访问AI助手，请联系您的Adobe客户团队以获得这些条款的指导。

对AI Assistant的访问受以下参数控制：

* **访问应用程序：** 您可以在Adobe Experience Platform、Adobe Real-Time CDP、Adobe Journey Optimizer和 [Customer Journey Analytics](https://experienceleague.adobe.com/en/docs/analytics-platform/using/ai-assistant).
<!-- * **Contractual access:** Your company must agree to certain [!DNL GenAI]-related legal terms before your organization can use AI Assistant. Contact your organization's administrator or your Adobe Account Team if you are not able to access AI Assistant.  -->
* **权限：** 使用 [权限UI](../access-control/abac/ui/permissions.md) 授予或撤销对贵组织中AI助理的访问权限。 要使用AI助手，给定用户必须属于使用 **启用AI助手** 和 **查看运营分析** 权限。
   * 作为管理员，您可以添加 **启用AI助手** 并将用户添加到给定角色，以允许用户访问组织中的AI助手。
   * 作为管理员，您可以添加 **查看运营分析** 将用户添加到给定角色中，以让他们使用AI助手的操作分析功能。 操作见解当前为测试版。

![具有给定角色中包含的启用AI助手和查看操作分析权限的权限UI页面。](./images/permissions.png)

使用权限UI授予在Experience Platform和Journey Optimizer中使用AI助手权限。 有关如何在Customer Journey Analytics中访问AI助手的信息。 请阅读以下文档： [Customer Journey Analytics](https://experienceleague.adobe.com/en/docs/analytics-platform/using/ai-assistant).

获得必要权限后，您可以通过选择正在使用的应用程序顶部标题上的AI助手图标来访问AI助手。

![具有首次用户体验的AI助手。](./images/ai-assistant.png)

## 后续步骤

获得AI助理的完全访问权限后，您可以在工作流中继续使用该功能，阅读 [AI助手UI指南](./ui-guide.md) 以了解更多信息。