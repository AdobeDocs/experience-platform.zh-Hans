---
keywords: Experience Platform；主页；热门主题；Apache Hive；Azure HDInsights；Azure hdinsights
solution: Experience Platform
title: 在UI中的Azure HDInsights Source连接上创建Apache配置单元
type: Tutorial
description: 了解如何使用Adobe Experience Platform UI在Azure HDInsights源连接上创建Apache Hive。
exl-id: 3eb3cb02-9867-451a-b847-ab895310eedf
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '479'
ht-degree: 2%

---

# 在UI中的[!DNL Azure HDInsights]源连接上创建[!DNL Apache Hive]

>[!NOTE]
>
> [!DNL Azure HDInsights]连接器上的[!DNL Apache Hive]处于Beta状态。 有关使用带有Beta标记的连接器的更多信息，请参阅[源概述](../../../../home.md#terms-and-conditions)。

Adobe Experience Platform中的Source连接器提供了按计划摄取外部来源数据的功能。 本教程提供了使用[!DNL Experience Platform]用户界面在[!DNL Azure HDInsights]源连接器上创建[!DNL Apache Hive]的步骤。

## 快速入门

本教程需要对以下Adobe Experience Platform组件有一定的了解：

* [[!DNL Experience Data Model (XDM)] 系统](../../../../../xdm/home.md)： [!DNL Experience Platform]用于组织客户体验数据的标准化框架。
   * [架构组合的基础知识](../../../../../xdm/schema/composition.md)：了解XDM架构的基本构建块，包括架构组合中的关键原则和最佳实践。
   * [架构编辑器教程](../../../../../xdm/tutorials/create-schema-ui.md)：了解如何使用架构编辑器UI创建自定义架构。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md)：根据来自多个源的汇总数据，提供统一的实时使用者个人资料。

如果您已经拥有有效的[!DNL Hive]连接，则可以跳过本文档的其余部分，并转到有关[配置数据流](../../dataflow/databases.md)的教程

### 收集所需的凭据

要在[!DNL Experience Platform]上访问您的[!DNL Hive]帐户，必须提供以下值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `host` | [!DNL Hive]服务器的IP地址或主机名。 |
| `username` | 用于访问[!DNL Hive]服务器的用户名。 |
| `password` | 对应于用户的密码。 |

有关入门的详细信息，请参阅[此 [!DNL Hive] 文档](https://cwiki.apache.org/confluence/display/Hive/Tutorial#Tutorial-GettingStarted)。

## 连接您的[!DNL Hive]帐户

收集所需的凭据后，您可以按照以下步骤将您的[!DNL Hive]帐户关联到[!DNL Experience Platform]。

登录到[Adobe Experience Platform](https://platform.adobe.com)，然后从左侧导航栏中选择&#x200B;**[!UICONTROL 源]**&#x200B;以访问&#x200B;**[!UICONTROL 源]**&#x200B;工作区。 **[!UICONTROL Catalog]**&#x200B;屏幕显示您可以为其创建帐户的各种源。

您可以从屏幕左侧的目录中选择相应的类别。 或者，您可以使用搜索选项查找您要使用的特定源。

在&#x200B;**[!UICONTROL 数据库]**&#x200B;类别下，选择&#x200B;**[!UICONTROL 配置单元]**。 如果这是您第一次使用此连接器，请选择&#x200B;**[!UICONTROL 配置]**。 否则，请选择&#x200B;**[!UICONTROL 添加数据]**&#x200B;以创建新的[!DNL Hive]连接器。

![目录](../../../../images/tutorials/create/hive/catalog.png)

此时会显示&#x200B;**[!UICONTROL 连接到配置单元]**&#x200B;页面。 在此页上，您可以使用新凭据或现有凭据。

### 新帐户

如果您正在使用新凭据，请选择&#x200B;**[!UICONTROL 新帐户]**。 在显示的输入表单上，提供名称、可选描述和您的[!DNL Hive]凭据。 完成后，选择&#x200B;**[!UICONTROL 连接]**，然后留出一些时间来建立新连接。

![连接](../../../../images/tutorials/create/hive/new.png)

### 现有账户

若要连接现有帐户，请选择您要连接的[!DNL Hive]帐户，然后选择&#x200B;**[!UICONTROL 下一步]**&#x200B;以继续。

![现有](../../../../images/tutorials/create/hive/existing.png)

## 后续步骤

通过学习本教程，您已建立与[!DNL Hive]帐户的连接。 您现在可以继续下一教程，并[配置数据流以将数据导入 [!DNL Experience Platform]](../../dataflow/databases.md)。
