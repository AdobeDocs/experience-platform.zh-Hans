---
keywords: Experience Platform；主页；热门主题；Greenplum;Greenplum
solution: Experience Platform
title: 在UI中创建GreenPlum源连接
topic-legacy: overview
type: Tutorial
description: 了解如何使用Adobe Experience Platform UI创建GreenPlum源连接。
exl-id: e6c6a495-25ce-4497-b20e-91374c7bb548
source-git-commit: e150f05df2107d7b3a2e95a55dc4ad072294279e
workflow-type: tm+mt
source-wordcount: '465'
ht-degree: 1%

---

# 在UI中创建[!DNL GreenPlum]源连接

Adobe Experience Platform中的源连接器提供了按计划摄取外部源数据的功能。 本教程提供了使用[!DNL Platform]用户界面创建[!DNL GreenPlum]源连接器的步骤。

## 入门指南

本教程需要对Adobe Experience Platform的以下组件有一定的了解：

* [[!DNL Experience Data Model (XDM)] 系统](../../../../../xdm/home.md):用于组织客户体验数 [!DNL Experience Platform] 据的标准化框架。
   * [架构组合的基础知识](../../../../../xdm/schema/composition.md):了解XDM模式的基本构建块，包括模式组合中的关键原则和最佳实践。
   * [模式编辑器教程](../../../../../xdm/tutorials/create-schema-ui.md):了解如何使用模式编辑器UI创建自定义模式。
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md):根据来自多个来源的汇总数据提供统一的实时客户资料。

如果您已经拥有有效的[!DNL GreenPlum]连接，则可以跳过本文档的其余部分，继续阅读有关[配置数据流](../../dataflow/databases.md)的教程。

### 收集所需的凭据

以下部分提供了您需要了解的其他信息，以便您能够使用[!DNL Flow Service] API成功连接到[!DNL GreenPlum]。

| 凭据 | 描述 |
| ---------- | ----------- |
| `connectionString` | 用于连接到[!DNL GreenPlum]实例的连接字符串。 [!DNL GreenPlum]的连接字符串模式为`Server={SERVER};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}` |

有关入门的更多信息，请参阅[此GreenPlum文档](https://gpdb.docs.pivotal.io/580/security-guide/topics/Authenticate.html#topic_fzv_wb2_jr__config_ssl_client_conn)。

## 连接[!DNL GreenPlum]帐户

收集所需凭据后，可以按照以下步骤将[!DNL GreenPlum]帐户关联到[!DNL Platform]。

登录到[Adobe Experience Platform](https://platform.adobe.com)，然后从左侧导航栏中选择&#x200B;**[!UICONTROL 源]**&#x200B;以访问&#x200B;**[!UICONTROL 源]**&#x200B;工作区。 **[!UICONTROL Catalog]**&#x200B;屏幕显示可为其创建帐户的各种源。

您可以从屏幕左侧的目录中选择相应的类别。 或者，您可以使用搜索选项找到要处理的特定源。

在&#x200B;**[!UICONTROL Databases]**&#x200B;类别下，选择&#x200B;**[!UICONTROL GreenPlum]**。 如果这是您首次使用此连接器，请选择&#x200B;**[!UICONTROL 配置]**。 否则，请选择&#x200B;**[!UICONTROL Add data]**&#x200B;以创建新的[!DNL GreenPlum]连接器。

![目录](../../../../images/tutorials/create/greenplum/catalog.png)

出现&#x200B;**[!UICONTROL Connect to GreenPlum]**&#x200B;页面。 在此页面上，您可以使用新凭据或现有凭据。

### 新帐户

如果您使用的是新凭据，请选择&#x200B;**[!UICONTROL 新帐户]**。 在显示的输入窗体中，提供名称、可选描述和您的[!DNL GreenPlum]凭据。 完成后，选择&#x200B;**[!UICONTROL 连接]**，然后允许一些时间建立新连接。

![connect](../../../../images/tutorials/create/greenplum/new.png)

### 现有帐户

要连接现有帐户，请选择要连接的[!DNL GreenPlum]帐户，然后选择右上角的&#x200B;**[!UICONTROL Next]**&#x200B;以继续。

![现有](../../../../images/tutorials/create/greenplum/existing.png)

## 后续步骤

在本教程中，您已建立与[!DNL GreenPlum]帐户的连接。 您现在可以继续阅读下一个教程，并[配置数据流以将数据导入 [!DNL Platform]](../../dataflow/databases.md)。
