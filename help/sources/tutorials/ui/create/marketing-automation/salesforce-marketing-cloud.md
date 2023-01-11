---
keywords: Experience Platform；主页；热门主题；Salesforce Marketing Cloud;Salesforce Marketing Cloud
solution: Experience Platform
title: 在UI中创建SalesforceMarketing Cloud源连接
type: Tutorial
description: 了解如何使用Adobe Experience Platform UI创建SalesforceMarketing Cloud源连接。
exl-id: 1d9bde60-31e0-489c-9c1c-b6471e0ea554
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '499'
ht-degree: 1%

---

# 创建 [!DNL Salesforce Marketing Cloud] UI中的源连接

>[!NOTE]
>
> 的 [!DNL Salesforce Marketing Cloud] 来源为测试版。 请参阅 [源概述](../../../../home.md#terms-and-conditions) 有关使用测试版标记的源的详细信息。

Adobe Experience Platform中的源连接器提供了按计划摄取外部源数据的功能。 本教程提供了创建 [!DNL Salesforce Marketing Cloud] 源连接器。

## 快速入门

本教程需要对Adobe Experience Platform的以下组件有一定的了解：

* [[!DNL Experience Data Model (XDM)] 系统](../../../../../xdm/home.md):标准化框架， [!DNL Experience Platform] 组织客户体验数据。
   * [架构组合的基础知识](../../../../../xdm/schema/composition.md):了解XDM模式的基本构建块，包括模式组合中的关键原则和最佳实践。
   * [模式编辑器教程](../../../../../xdm/tutorials/create-schema-ui.md):了解如何使用模式编辑器UI创建自定义模式。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md):根据来自多个来源的汇总数据提供统一的实时客户资料。

如果您已经 [!DNL Salesforce Marketing Cloud] 连接时，您可以跳过本文档的其余部分，并继续阅读上的教程 [配置数据流](../../dataflow/marketing-automation.md).

### 收集所需的凭据

为了访问 [!DNL Salesforce Marketing Cloud] 帐户时，必须提供以下值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `host` | 应用程序的主机服务器。 这通常是您的子域。 **注意：** 在输入 `host` 值时，您只需指定子域，而不需要指定整个URL。 例如，如果您的主机URL为 `https://abcd-ab12c3d4e5fg6hijk7lmnop8qrst.auth.marketingcloudapis.com/`，则只需输入 `abcd-ab12c3d4e5fg6hijk7lmnop8qrst` 作为您的主机值。 |
| `clientId` | 与 [!DNL Salesforce Marketing Cloud] 应用程序。 |
| `clientSecret` | 与 [!DNL Salesforce Marketing Cloud] 应用程序。 |

有关入门的更多信息，请参阅此 [[!DNL Salesforce Marketing Cloud] 文档](https://developer.salesforce.com/docs/atlas.en-us.mc-apis.meta/mc-apis/authentication.htm).

## 连接 [!DNL Salesforce Marketing Cloud] 帐户

收集所需的凭据后，您可以按照以下步骤链接 [!DNL Salesforce Marketing Cloud] 帐户到平台。

在平台UI中，选择 **[!UICONTROL 源]** 从左侧导航访问 [!UICONTROL 源] 工作区。 的 [!UICONTROL 目录] 屏幕会显示您可为其创建帐户的各种源。

您可以从屏幕左侧的目录中选择相应的类别。 您还可以使用搜索栏缩小显示的连接器。

在 [!UICONTROL 营销自动化] 类别，选择 **[!UICONTROL SalesforceMarketing Cloud]** 然后选择 **[!UICONTROL 设置]**.

![目录](../../../../images/tutorials/create/salesforce-marketing-cloud/catalog.png)

的 **[!UICONTROL 连接到SalesforceMarketing Cloud]** 页面。 在此页面上，您可以使用新凭据或现有凭据。

### 新帐户

如果您使用新凭据，请选择 **[!UICONTROL 新帐户]**. 在显示的输入窗体中，提供名称、可选描述以及 [!DNL Salesforce Marketing Cloud] 凭据。 完成后，选择 **[!UICONTROL 连接]** 然后，再留出一些时间建立新连接。

![新建](../../../../images/tutorials/create/salesforce-marketing-cloud/new.png)

### 现有帐户

要连接现有帐户，请选择 [!DNL Salesforce Marketing Cloud] 要连接的帐户，然后选择 **[!UICONTROL 下一个]** 以继续。

![现有](../../../../images/tutorials/create/salesforce-marketing-cloud/existing.png)

## 后续步骤

通过阅读本教程，您已经与 [!DNL Salesforce Marketing Cloud] 帐户。 您现在可以继续下一个教程和 [配置数据流，将营销自动化系统数据引入平台](../../dataflow/marketing-automation.md).
