---
keywords: Experience Platform；主页；热门主题；DB2；db2；IBM DB2；ibm db2
solution: Experience Platform
title: 在UI中创建IBM DB2 Source连接
type: Tutorial
description: 了解如何使用Adobe Experience Platform UI创建IBM DB2源连接。
exl-id: 69c99f94-9cb9-43ff-9315-ce166ab35a60
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '527'
ht-degree: 1%

---

# 在UI中创建IBM DB2源连接

>[!NOTE]
>
> IBM DB2连接器处于测试阶段。 有关使用带有Beta标记的连接器的更多信息，请参阅[源概述](../../../../home.md#terms-and-conditions)。

Adobe Experience Platform中的Source连接器提供了按计划摄取外部来源数据的功能。 本教程提供了使用[!DNL Experience Platform]用户界面创建IBM DB2（以下称为“DB2”）源连接器的步骤。

## 快速入门

本教程需要对以下Adobe Experience Platform组件有一定的了解：

* [[!DNL Experience Data Model (XDM)] 系统](../../../../../xdm/home.md)： [!DNL Experience Platform]用于组织客户体验数据的标准化框架。
   * [架构组合的基础知识](../../../../../xdm/schema/composition.md)：了解XDM架构的基本构建块，包括架构组合中的关键原则和最佳实践。
   * [架构编辑器教程](../../../../../xdm/tutorials/create-schema-ui.md)：了解如何使用架构编辑器UI创建自定义架构。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md)：根据来自多个源的汇总数据，提供统一的实时使用者个人资料。

如果您已经具有有效的DB2连接，则可以跳过本文档的其余部分，并转到有关[配置数据流](../../dataflow/databases.md)的教程。

### 收集所需的凭据

以下部分提供了使用[!DNL Flow Service] API成功连接到DB2所需了解的其他信息。

| 凭据 | 描述 |
| ---------- | ----------- |
| `server` | DB2服务器的名称。 您可以在用冒号分隔的服务器名称后面指定端口号。 例如：server：port。 |
| `database` | DB2数据库的名称。 |
| `username` | 用于连接到DB2数据库的用户名。 |
| `password` | 您为用户名指定的用户帐户的密码。 |

有关入门的详细信息，请参阅[此DB2文档](https://www.ibm.com/support/knowledgecenter/SSFMBX/com.ibm.swg.im.dashdb.doc/connecting/connect_credentials.html)。

## 连接您的IBM DB2帐户

收集所需的凭据后，您可以按照以下步骤将DB2帐户链接到[!DNL Experience Platform]。

登录到[Adobe Experience Platform](https://platform.adobe.com)，然后从左侧导航栏中选择&#x200B;**[!UICONTROL 源]**&#x200B;以访问&#x200B;**[!UICONTROL 源]**&#x200B;工作区。 **[!UICONTROL Catalog]**&#x200B;屏幕显示您可以为其创建帐户的各种源。

您可以从屏幕左侧的目录中选择相应的类别。 或者，您可以使用搜索选项查找您要使用的特定源。

在&#x200B;**[!UICONTROL 数据库]**&#x200B;类别下，选择&#x200B;**[!UICONTROL IBM DB2]**。 如果这是您第一次使用此连接器，请选择&#x200B;**[!UICONTROL 配置]**。 否则，请选择&#x200B;**[!UICONTROL 添加数据]**&#x200B;以创建新的DB2连接器。

![目录](../../../../images/tutorials/create/ibm-db2/catalog.png)

此时会显示&#x200B;**[!UICONTROL 连接到IBM DB2]**&#x200B;页。 在此页上，您可以使用新凭据或现有凭据。

### 新帐户

如果您正在使用新凭据，请选择&#x200B;**[!UICONTROL 新帐户]**。 在出现的输入窗体上，提供名称、可选说明和DB2凭据。 完成后，选择&#x200B;**[!UICONTROL 连接]**，然后留出一些时间来建立新连接。

![连接](../../../../images/tutorials/create/ibm-db2/new.png)

### 现有账户

若要连接现有帐户，请选择要连接的DB2帐户，然后选择&#x200B;**[!UICONTROL 下一步]**&#x200B;以继续。

![现有](../../../../images/tutorials/create/ibm-db2/existing.png)

## 后续步骤

通过学习本教程，您已建立与DB2帐户的连接。 您现在可以继续下一教程，并[配置数据流以将数据导入 [!DNL Experience Platform]](../../dataflow/databases.md)。
