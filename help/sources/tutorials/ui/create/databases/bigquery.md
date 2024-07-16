---
title: 在UI中创建Google Big Query Source连接
description: 了解如何使用Google UI创建Adobe Experience Platform Big Query源连接。
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 3c0902de-48b9-42d8-a4bd-0213ca85fc7f
source-git-commit: 9a8139c26b5bb5ff937a51986967b57db58aab6c
workflow-type: tm+mt
source-wordcount: '449'
ht-degree: 2%

---

# 在用户界面中创建[!DNL Google Big Query]源连接

>[!IMPORTANT]
>
>[!DNL Google BigQuery]源在源目录中可供已购买Real-time Customer Data Platform Ultimate的用户使用。

Adobe Experience Platform中的Source连接器提供了按计划摄取外部来源数据的功能。 本教程提供了使用Platform用户界面创建[!DNL Google Big Query]源连接的步骤。

## 快速入门

本教程需要对以下Experience Platform组件有一定的了解：

* [[!DNL Experience Data Model (XDM)] 系统](../../../../../xdm/home.md)：Experience Platform用于组织客户体验数据的标准化框架。
   * [架构组合的基础知识](../../../../../xdm/schema/composition.md)：了解XDM架构的基本构建块，包括架构组合中的关键原则和最佳实践。
   * [架构编辑器教程](../../../../../xdm/tutorials/create-schema-ui.md)：了解如何使用架构编辑器UI创建自定义架构。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md)：根据来自多个源的汇总数据，提供统一的实时使用者个人资料。

如果您已经拥有有效的[!DNL Google BigQuery]连接，则可以跳过本文档的其余部分，并转到有关[配置数据流](../../dataflow/databases.md)的教程。

### 收集所需的凭据

要在Platform上访问您的[!DNL Google BigQuery]帐户，必须提供以下OAuth 2.0身份验证值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `project` | 要查询的默认[!DNL Google BigQuery]项目的项目ID。 |
| `clientID` | 用于生成刷新令牌的ID值。 |
| `clientSecret` | 用于生成刷新令牌的机密值。 |
| `refreshToken` | 从[!DNL Google]获得的刷新令牌用于授权访问[!DNL Google BigQuery]。 |

有关这些值的详细信息，请参阅[此 [!DNL Google BigQuery] 文档](https://cloud.google.com/storage/docs/json_api/v1/how-tos/authorizing)。

## 连接您的Google BigQuery帐户

在Platform UI中，从左侧导航中选择&#x200B;**[!UICONTROL 源]**&#x200B;以访问[!UICONTROL 源]工作区。 [!UICONTROL Catalog]屏幕显示您可以用来创建帐户的各种源。

您可以从屏幕左侧的目录中选择相应的类别。 或者，您可以使用搜索栏查找要使用的特定源。

在[!UICONTROL 数据库]类别下，选择&#x200B;**[!UICONTROL Google BigQuery]**，然后选择&#x200B;**[!UICONTROL 添加数据]**。

![](../../../../images/tutorials/create/google-big-query/catalog.png)

此时会显示&#x200B;**[!UICONTROL 连接到Google Big Query]**&#x200B;页面。 在此页上，您可以使用新凭据或现有凭据。

### 现有账户

若要连接现有帐户，请选择您要连接的[!DNL Google BigQuery]帐户，然后选择&#x200B;**[!UICONTROL 下一步]**&#x200B;以继续。

![](../../../../images/tutorials/create/google-big-query/existing.png)

### 新帐户

如果您正在使用新凭据，请选择&#x200B;**[!UICONTROL 新帐户]**。 在显示的输入表单上，提供名称、可选描述和您的[!DNL Google BigQuery]凭据。 完成后，选择&#x200B;**[!UICONTROL 连接到源]**，然后留出一些时间来建立新连接。

![](../../../../images/tutorials/create/google-big-query/new.png)

## 后续步骤

通过学习本教程，您已建立与[!DNL Google BigQuery]帐户的连接。 您现在可以继续下一教程，并[配置数据流以将数据导入Platform](../../dataflow/databases.md)。
