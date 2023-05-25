---
keywords: Experience Platform；主页；热门主题；Google Big Query；google big query；GBQ；gbq
solution: Experience Platform
title: 在UI中创建Google大型查询源连接
type: Tutorial
description: 了解如何使用Google UI创建Adobe Experience Platform Big Query源连接。
exl-id: 3c0902de-48b9-42d8-a4bd-0213ca85fc7f
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '450'
ht-degree: 1%

---

# 创建 [!DNL Google Big Query] UI中的源连接

Adobe Experience Platform中的源连接器提供了按计划摄取外部来源数据的功能。 本教程提供了用于创建 [!DNL Google Big Query] 源连接，使用Platform用户界面。

## 快速入门

本教程需要对以下Experience Platform组件有一定的了解：

* [[!DNL Experience Data Model (XDM)] 系统](../../../../../xdm/home.md)：Experience Platform用于组织客户体验数据的标准化框架。
   * [模式组合基础](../../../../../xdm/schema/composition.md)：了解XDM架构的基本构建基块，包括架构构成中的关键原则和最佳实践。
   * [架构编辑器教程](../../../../../xdm/tutorials/create-schema-ui.md)：了解如何使用架构编辑器UI创建自定义架构。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md)：根据来自多个来源的汇总数据提供统一的实时使用者个人资料。

如果您已经拥有有效的 [!DNL Google BigQuery] 连接，您可以跳过本文档的其余部分，并继续阅读以下教程： [配置数据流](../../dataflow/databases.md).

### 收集所需的凭据

要访问您的 [!DNL Google BigQuery] 帐户，您必须提供以下OAuth 2.0身份验证值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `project` | 默认的项目ID [!DNL Google BigQuery] 要查询的项目。 |
| `clientID` | 用于生成刷新令牌的ID值。 |
| `clientSecret` | 用于生成刷新令牌的机密值。 |
| `refreshToken` | 刷新令牌获取自 [!DNL Google] 用于授权访问 [!DNL Google BigQuery]. |

有关这些值的更多信息，请参阅 [此 [!DNL Google BigQuery] 文档](https://cloud.google.com/storage/docs/json_api/v1/how-tos/authorizing).

## 连接您的Google BigQuery帐户

在Platform UI中，选择 **[!UICONTROL 源]** 从左侧导航访问 [!UICONTROL 源] 工作区。 此 [!UICONTROL 目录] 屏幕显示您可以用来创建帐户的各种源。

您可以从屏幕左侧的目录中选择相应的类别。 或者，您可以使用搜索栏查找要使用的特定源。

在 [!UICONTROL 数据库] 类别，选择 **[!UICONTROL Google BigQuery]** 然后选择 **[!UICONTROL 添加数据]**.

![](../../../../images/tutorials/create/google-big-query/catalog.png)

此 **[!UICONTROL 连接到Google Big Query]** 页面。 在此页上，您可以使用新凭据或现有凭据。

### 现有帐户

要连接现有帐户，请选择 [!DNL Google BigQuery] 要连接的帐户，然后选择 **[!UICONTROL 下一个]** 以继续。

![](../../../../images/tutorials/create/google-big-query/existing.png)

### 新帐户

如果您使用的是新凭据，请选择 **[!UICONTROL 新帐户]**. 在出现的输入表单上，提供名称、可选描述以及 [!DNL Google BigQuery] 凭据。 完成后，选择 **[!UICONTROL 连接到源]** 然后留出一些时间来建立新连接。

![](../../../../images/tutorials/create/google-big-query/new.png)

## 后续步骤

按照本教程，您已建立与的连接 [!DNL Google BigQuery] 帐户。 您现在可以继续下一教程和 [配置数据流以将数据引入平台](../../dataflow/databases.md).
