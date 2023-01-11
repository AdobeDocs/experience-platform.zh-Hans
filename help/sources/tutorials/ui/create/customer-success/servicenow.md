---
keywords: Experience Platform；主页；热门主题；ServiceNow;Servicenow
solution: Experience Platform
title: 在UI中创建ServiceNow源连接
type: Tutorial
description: 了解如何使用Adobe Experience Platform UI创建ServiceNow源连接。
exl-id: 66c12f4d-8b0c-4bb2-910d-9e09fa364c94
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '457'
ht-degree: 1%

---

# 创建 [!DNL ServiceNow] UI中的源连接

Adobe Experience Platform中的源连接器提供了按计划摄取外部源数据的功能。 本教程提供了创建 [!DNL ServiceNow] 源连接器使用 [!DNL Platform] 用户界面。

## 快速入门

本教程需要对Adobe Experience Platform的以下组件有一定的了解：

* [[!DNL Experience Data Model (XDM)] 系统](../../../../../xdm/home.md):标准化框架， [!DNL Experience Platform] 组织客户体验数据。
   * [架构组合的基础知识](../../../../../xdm/schema/composition.md):了解XDM模式的基本构建块，包括模式组合中的关键原则和最佳实践。
   * [模式编辑器教程](../../../../../xdm/tutorials/create-schema-ui.md):了解如何使用模式编辑器UI创建自定义模式。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md):根据来自多个来源的汇总数据提供统一的实时客户资料。

如果您已经拥有 [!DNL ServiceNow] 连接时，您可以跳过本文档的其余部分，并继续阅读上的教程 [配置数据流](../../dataflow/customer-success.md)

### 收集所需的凭据

为了访问 [!DNL ServiceNow] 帐户 [!DNL Platform]，则必须提供以下值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `endpoint` | 的端点 [!DNL ServiceNow] 服务器。 |
| `username` | 用于连接到的用户名 [!DNL ServiceNow] 服务器进行身份验证。 |
| `password` | 连接到的密码 [!DNL ServiceNow] 服务器进行身份验证。 |

有关入门的更多信息，请参阅 [此 [!DNL ServiceNow] 文档](https://developer.servicenow.com/app.do#!/rest_api_doc?v=newyork&amp;id=r_TableAPI-GET).

## 连接 [!DNL ServiceNow] 帐户

收集所需的凭据后，您可以按照以下步骤链接 [!DNL ServiceNow] 帐户 [!DNL Platform].

登录到 [Adobe Experience Platform](https://platform.adobe.com) 然后选择 **[!UICONTROL 源]** 从左侧导航栏访问 **[!UICONTROL 源]** 工作区。 的 **[!UICONTROL 目录]** 屏幕会显示您可为其创建帐户的各种源。

您可以从屏幕左侧的目录中选择相应的类别。 或者，您可以使用搜索选项找到要处理的特定源。

在 **[!UICONTROL 客户成功]** 类别，选择 **[!UICONTROL ServiceNow]**. 如果这是您首次使用此连接器，请选择 **[!UICONTROL 配置]**. 否则，请选择 **[!UICONTROL 连接源]** 创建新 [!DNL ServiceNow] 连接器。

![](../../../../images/tutorials/create/servicenow/catalog.png)

的 **[!UICONTROL 连接到ServiceNow]** 页面。 在此页面上，您可以使用新凭据或现有凭据。

### 新帐户

如果您使用新凭据，请选择 **[!UICONTROL 新帐户]**. 在显示的输入窗体中，提供名称、可选描述以及 [!DNL ServiceNow] 凭据。 完成后，选择 **[!UICONTROL 连接]** 然后，再留出一些时间建立新连接。

![](../../../../images/tutorials/create/servicenow/new.png)

### 现有帐户

要连接现有帐户，请选择 [!DNL ServiceNow] 要连接的帐户，然后选择 **[!UICONTROL 下一个]** 以继续。

![](../../../../images/tutorials/create/servicenow/existing.png)

## 后续步骤

通过阅读本教程，您已经与 [!DNL ServiceNow] 帐户。 您现在可以继续下一个教程和 [配置数据流以将数据导入 [!DNL Platform]](../../dataflow/customer-success.md).
