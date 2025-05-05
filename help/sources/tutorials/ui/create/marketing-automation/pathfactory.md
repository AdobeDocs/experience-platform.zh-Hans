---
title: 通过UI将您的PathFactory帐户连接到Experience Platform
description: 了解如何通过UI将您的PathFactory帐户连接到Experience Platform。
badge: Beta 版
exl-id: 859dd0c1-8c4b-43e3-a87b-84c879460bc0
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '572'
ht-degree: 2%

---

# 通过UI将您的[!DNL PathFactory]帐户连接到Experience Platform

本教程提供了有关如何通过UI将[!DNL PathFactory]访客、会话和页面查看数据连接到Adobe Experience Platform的步骤。

## 快速入门

本教程需要对以下Experience Platform组件有一定的了解：

* [[!DNL Experience Data Model (XDM)] 系统](../../../../../xdm/home.md)： [!DNL Experience Platform]用于组织客户体验数据的标准化框架。
   * [架构组合的基础知识](../../../../../xdm/schema/composition.md)：了解XDM架构的基本构建块，包括架构组合中的关键原则和最佳实践。
   * [架构编辑器教程](../../../../../xdm/tutorials/create-schema-ui.md)：了解如何使用架构编辑器UI创建自定义架构。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md)：根据来自多个源的汇总数据，提供统一的实时使用者个人资料。

如果您已经拥有[!DNL PathFactory]帐户，则可以跳过本文档的其余部分，并继续学习关于使用UI[&#128279;](../../dataflow/marketing-automation.md)将营销自动化数据引入Experience Platform的教程。

### 收集所需的凭据 {#gather-credentials}

要在Experience Platform上访问PathFactory帐户，必须提供以下值：

| 凭据 | 描述 |
| ---------- | ----------- |
| 用户名 | PathFactory帐户用户名。 这对于识别您在系统中的帐户至关重要。 |
| 密码 | 与您的PathFactory帐户关联的密码。 确保此安全设置以防止未经授权的访问。 |
| 域 | 与您的PathFactory帐户关联的域。 这通常指的是PathFactory URL中的唯一标识符。 |
| 访问令牌 | 用于API身份验证的唯一令牌，确保系统与PathFactory之间的安全通信。 |
| API端点 | 用于访问数据的特定API端点：访客、会话和页面查看。 每个端点对应于可检索的不同数据集。 **注意：**&#x200B;这些由[!DNL PathFactory]预定义，特定于您要访问的数据： <ul><li>**访客终结点**： `/api/public/v3/data_lake_apis/visitors.json`</li><li>**会话终结点**： `/api/public/v3/data_lake_apis/sessions.json`</li><li>**页面查看终结点**： `/api/public/v3/data_lake_apis/page_views.json`</li></ul> |

有关如何保护和使用凭据的详细指导，以及有关获取和刷新访问令牌的信息，请访问[PathFactory支持中心](https://support.pathfactory.com/categories/adobe/)。 此资源提供有关管理凭据以及确保有效且安全的API集成的综合指南。


## 连接您的[!DNL PathFactory]帐户

在Experience Platform UI中，从左侧导航中选择&#x200B;**[!UICONTROL 源]**&#x200B;以访问[!UICONTROL 源]工作区。 [!UICONTROL 目录]显示Experience Platform支持的各种源。

您可以从类别列表中选择相应的类别。 您还可以使用搜索栏筛选特定源。

在[!UICONTROL 营销自动化]类别下，选择&#x200B;**[!UICONTROL PathFactory]**，然后选择&#x200B;**[!UICONTROL 设置]**。

![已选择PathFactory源的源目录。](../../../../images/tutorials/create/pathfactory/catalog.png)

此时会显示&#x200B;**[!UICONTROL 连接到PathFactory]**&#x200B;页。 在此页上，您可以创建新帐户或使用现有帐户。

### 新帐户

要创建新帐户，请选择&#x200B;**[!UICONTROL 新帐户]**，并提供帐户的名称、可选描述以及与您的[!DNL PathFactory]帐户对应的身份验证凭据。

完成后，选择&#x200B;**[!UICONTROL 连接到源]**，然后留出一些时间来建立新连接。

![新帐户接口，您可以在其中验证PathFactory的新帐户。](../../../../images/tutorials/create/pathfactory/new.png)

### 现有账户

如果您已经拥有现有帐户，请选择&#x200B;**[!UICONTROL 现有帐户]**，然后从显示的列表中选择您要使用的帐户。

![可以从现有PathFactory帐户的列表中选择的现有帐户接口。](../../../../images/tutorials/create/pathfactory/existing.png)

## 后续步骤

通过学习本教程，您已在[!DNL PathFactory]帐户与Experience Platform之间建立连接。 您现在可以继续下一教程并[创建数据流以将您的营销自动化数据导入Experience Platform](../../dataflow/marketing-automation.md)。
