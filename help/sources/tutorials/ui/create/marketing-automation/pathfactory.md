---
title: 通过UI将您的PathFactory帐户连接到Experience Platform
description: 了解如何通过UI将您的PathFactory帐户连接到Experience Platform。
last-substantial-update: 2024-04-30T00:00:00Z
hide: true
hidefromtoc: true
badge: Beta 版
source-git-commit: 18f6c253aec6815cf84272cbce340a9aa7ed8ab9
workflow-type: tm+mt
source-wordcount: '570'
ht-degree: 1%

---

# 连接您的 [!DNL PathFactory] 要通过UIExperience Platform的帐户

本教程提供了有关如何连接 [!DNL PathFactory] 通过UI将访客、会话和页面查看数据发送到Adobe Experience Platform。

## 快速入门

本教程需要对以下Experience Platform组件有一定的了解：

* [[!DNL Experience Data Model (XDM)] 系统](../../../../../xdm/home.md)：用于实现此目标的标准化框架 [!DNL Experience Platform] 组织客户体验数据。
   * [模式组合基础](../../../../../xdm/schema/composition.md)：了解XDM架构的基本构建基块，包括架构构成中的关键原则和最佳实践。
   * [架构编辑器教程](../../../../../xdm/tutorials/create-schema-ui.md)：了解如何使用架构编辑器UI创建自定义架构。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md)：根据来自多个来源的汇总数据提供统一的实时使用者个人资料。

如果您已经拥有 [!DNL PathFactory] 帐户，您可以跳过本文档的其余部分，并继续阅读上的教程 [使用UI将营销自动化数据引入Experience Platform](../../dataflow/marketing-automation.md).

### 收集所需的凭据 {#gather-credentials}

要在平台上访问PathFactory帐户，必须提供以下值：

| 凭据 | 描述 |
| ---------- | ----------- |
| 用户名 | PathFactory帐户用户名。 这对于识别您在系统中的帐户至关重要。 |
| 密码 | 与您的PathFactory帐户关联的密码。 确保此安全设置以防止未经授权的访问。 |
| 域 | 与您的PathFactory帐户关联的域。 这通常指的是PathFactory URL中的唯一标识符。 |
| 访问令牌 | 用于API身份验证的唯一令牌，确保系统与PathFactory之间的安全通信。 |
| API端点 | 用于访问数据的特定API端点：访客、会话和页面查看。 每个端点对应于可检索的不同数据集。 **注意：** 这些规则由预定义 [!DNL PathFactory] 特定于要访问的数据： <ul><li>**访客端点**： `/api/public/v3/data_lake_apis/visitors.json`</li><li>**会话端点**： `/api/public/v3/data_lake_apis/sessions.json`</li><li>**页面查看端点**： `/api/public/v3/data_lake_apis/page_views.json`</li></ul> |

有关如何保护和使用凭据的详细指导，以及有关获取和刷新访问令牌的信息，请访问 [PathFactory支持中心](https://support.pathfactory.com/categories/adobe/). 此资源提供有关管理凭据以及确保有效且安全的API集成的综合指南。


## 连接您的 [!DNL PathFactory] 帐户

在Platform UI中，选择 **[!UICONTROL 源]** 从左侧导航访问 [!UICONTROL 源] 工作区。 此 [!UICONTROL 目录] 显示Experience Platform支持的各种源。

您可以从类别列表中选择相应的类别。 您还可以使用搜索栏筛选特定源。

在 [!UICONTROL 营销自动化] 类别，选择 **[!UICONTROL 路径工厂]** 然后选择 **[!UICONTROL 设置]**.

![已选择PathFactory源的源目录。](../../../../images/tutorials/create/pathfactory/catalog.png)

此 **[!UICONTROL 连接到PathFactory]** 页面。 在此页上，您可以创建新帐户或使用现有帐户。

### 新帐户

要创建新帐户，请选择 **[!UICONTROL 新帐户]** 并提供帐户名称、可选描述以及与您的帐户对应的身份验证凭据。 [!DNL PathFactory] 帐户。

完成后，选择 **[!UICONTROL 连接到源]** 然后等待一段时间以建立新连接。

![新的帐户界面，您可以在其中验证PathFactory的新帐户。](../../../../images/tutorials/create/pathfactory/new.png)

### 现有帐户

如果您已经拥有现有帐户，请选择 **[!UICONTROL 现有帐户]** 然后从显示的列表中选择要使用的帐户。

![可以从现有PathFactory帐户列表中进行选择的现有帐户界面。](../../../../images/tutorials/create/pathfactory/existing.png)

## 后续步骤

通过学习本教程，您已在 [!DNL PathFactory] 帐户和Experience Platform。 您现在可以继续下一教程和 [创建数据流以将您的营销自动化数据引入Experience Platform](../../dataflow/marketing-automation.md).
