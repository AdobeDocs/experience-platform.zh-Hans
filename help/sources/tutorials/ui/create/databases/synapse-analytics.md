---
keywords: Experience Platform；主页；热门主题；Azure synapse分析；Synapse;Synapse;azure synapse分析
solution: Experience Platform
title: 在UI中创建Azure synapse分析源连接
topic-legacy: overview
type: Tutorial
description: 了解如何使用Adobe Experience Platform UI创建Azure synapseAnalytics（以下简称“Synapse”）源连接。
exl-id: 1f1ce317-eaaf-4ad2-a5fb-236983220bd7
source-git-commit: e150f05df2107d7b3a2e95a55dc4ad072294279e
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 1%

---

# 在UI中创建[!DNL Azure Synapse Analytics]源连接

Adobe Experience Platform中的源连接器提供了按计划摄取外部源数据的功能。 本教程提供了使用[!DNL Platform]用户界面创建[!DNL Azure Synapse Analytics]（以下称“[!DNL Synapse]”）源连接器的步骤。

## 入门指南

本教程需要对Adobe Experience Platform的以下组件有一定的了解：

* [[!DNL Experience Data Model (XDM)] 系统](../../../../../xdm/home.md):用于组织客户体验数 [!DNL Experience Platform] 据的标准化框架。
   * [架构组合的基础知识](../../../../../xdm/schema/composition.md):了解XDM模式的基本构建块，包括模式组合中的关键原则和最佳实践。
   * [模式编辑器教程](../../../../../xdm/tutorials/create-schema-ui.md):了解如何使用模式编辑器UI创建自定义模式。
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md):根据来自多个来源的汇总数据提供统一的实时客户资料。

如果您已经拥有有效的[!DNL Synapse]连接，则可以跳过本文档的其余部分，继续阅读有关[配置数据流](../../dataflow/databases.md)的教程。

### 收集所需的凭据

要在[!DNL Platform]上访问您的[!DNL Synapse]帐户，必须提供以下值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `connectionString` | 与您的[!DNL Synapse]身份验证关联的连接字符串。 [!DNL Synapse]连接字符串模式为`Server=tcp:{SERVER_NAME}.database.windows.net,1433;Database={DATABASE};User ID={USERNAME}@{SERVER_NAME};Password={PASSWORD};Trusted_Connection=False;Encrypt=True;Connection Timeout=30`。 |

有关此值的更多信息，请参见[this [!DNL Synapse] document](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-sql-data-warehouse)。

## 连接[!DNL Synapse]帐户

收集所需凭据后，可以按照以下步骤将[!DNL Synapse]帐户关联到[!DNL Platform]。

登录到[Adobe Experience Platform](https://platform.adobe.com)，然后从左侧导航栏中选择&#x200B;**[!UICONTROL 源]**&#x200B;以访问&#x200B;**[!UICONTROL 源]**&#x200B;工作区。 **[!UICONTROL Catalog]**&#x200B;屏幕显示可为其创建帐户的各种源。

您可以从屏幕左侧的目录中选择相应的类别。 或者，您可以使用搜索选项找到要处理的特定源。

在&#x200B;**[!UICONTROL 数据库]**&#x200B;类别下，选择&#x200B;**[!UICONTROL Azure synapseAnalytics]**。 如果这是您首次使用此连接器，请选择&#x200B;**[!UICONTROL 配置]**。 否则，请选择&#x200B;**[!UICONTROL Add data]**&#x200B;以创建新的[!DNL Synapse]连接器。

![](../../../../images/tutorials/create/azure-synapse-analytics/catalog.png)

此时会显示&#x200B;**[!UICONTROL 连接到Azure synapse分析]**&#x200B;页面。 在此页面上，您可以使用新凭据或现有凭据。

### 新帐户

如果您使用的是新凭据，请选择&#x200B;**[!UICONTROL 新帐户]**。 在显示的输入窗体中，提供名称、可选描述和您的[!DNL Synapse]凭据。 完成后，选择&#x200B;**[!UICONTROL 连接]**，然后允许一些时间建立新连接。

![](../../../../images/tutorials/create/azure-synapse-analytics/new.png)

### 现有帐户

要连接现有帐户，请选择要连接的[!DNL Synapse]帐户，然后选择&#x200B;**[!UICONTROL Next]**&#x200B;以继续。

![](../../../../images/tutorials/create/azure-synapse-analytics/existing.png)

## 后续步骤

在本教程中，您已建立与[!DNL Synapse]帐户的连接。 您现在可以继续阅读下一个教程，并[配置数据流以将数据导入 [!DNL Platform]](../../dataflow/databases.md)。
