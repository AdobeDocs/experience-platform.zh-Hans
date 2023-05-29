---
keywords: Experience Platform；主页；热门主题；DB2；db2；IBM DB2；ibm db2
solution: Experience Platform
title: 在UI中创建IBM DB2源连接
type: Tutorial
description: 了解如何使用Adobe Experience Platform UI创建IBM DB2源连接。
exl-id: 69c99f94-9cb9-43ff-9315-ce166ab35a60
source-git-commit: e37c00863249e677f1645266859bf40fe6451827
workflow-type: tm+mt
source-wordcount: '536'
ht-degree: 0%

---

# 在UI中创建IBM DB2源连接

>[!NOTE]
>
> IBM DB2连接器处于测试阶段。 请参阅 [源概述](../../../../home.md#terms-and-conditions) 有关使用Beta标记的连接器的更多信息。

Adobe Experience Platform中的源连接器提供了按计划摄取外部来源数据的功能。 本教程提供了使用创建IBM DB2（以下称为“DB2”）源连接器的步骤。 [!DNL Platform] 用户界面。

## 快速入门

本教程需要深入了解Adobe Experience Platform的以下组件：

* [[!DNL Experience Data Model (XDM)] 系统](../../../../../xdm/home.md)：用于实现此目标的标准化框架 [!DNL Experience Platform] 组织客户体验数据。
   * [模式组合基础](../../../../../xdm/schema/composition.md)：了解XDM架构的基本构建基块，包括架构构成中的关键原则和最佳实践。
   * [架构编辑器教程](../../../../../xdm/tutorials/create-schema-ui.md)：了解如何使用架构编辑器UI创建自定义架构。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md)：根据来自多个来源的汇总数据提供统一的实时使用者个人资料。

如果您已经拥有有效的DB2连接，则可以跳过本文档的其余部分，并继续阅读上的教程 [配置数据流](../../dataflow/databases.md).

### 收集所需的凭据

以下部分提供了成功连接到DB2之前需要了解的其他信息 [!DNL Flow Service] API。

| 凭据 | 描述 |
| ---------- | ----------- |
| `server` | DB2服务器的名称。 您可以在用冒号分隔的服务器名称后面指定端口号。 例如： server：port。 |
| `database` | DB2数据库的名称。 |
| `username` | 用于连接到DB2数据库的用户名。 |
| `password` | 为用户名指定的用户帐户的密码。 |

有关入门的更多信息，请参阅 [此DB2文档](https://www.ibm.com/support/knowledgecenter/SSFMBX/com.ibm.swg.im.dashdb.doc/connecting/connect_credentials.html).

## 连接您的IBM DB2帐户

收集所需的凭据后，您可以按照以下步骤将DB2帐户关联到 [!DNL Platform].

登录 [Adobe Experience Platform](https://platform.adobe.com) 然后选择 **[!UICONTROL 源]** 以访问 **[!UICONTROL 源]** 工作区。 此 **[!UICONTROL 目录]** 屏幕显示您可以为其创建帐户的各种源。

您可以从屏幕左侧的目录中选择相应的类别。 或者，您可以使用搜索选项查找要使用的特定源。

在 **[!UICONTROL 数据库]** 类别，选择 **[!UICONTROL IBM DB2]**. 如果这是您第一次使用此连接器，请选择 **[!UICONTROL 配置]**. 否则，选择 **[!UICONTROL 添加数据]** 创建新的DB2连接器。

![目录](../../../../images/tutorials/create/ibm-db2/catalog.png)

此 **[!UICONTROL 连接到IBM DB2]** 页面。 在此页上，您可以使用新凭据或现有凭据。

### 新帐户

如果您使用的是新凭据，请选择 **[!UICONTROL 新帐户]**. 在显示的输入表单上，提供名称、可选说明和DB2凭据。 完成后，选择 **[!UICONTROL Connect]** 然后留出一些时间来建立新连接。

![connect](../../../../images/tutorials/create/ibm-db2/new.png)

### 现有帐户

要连接现有帐户，请选择要连接的DB2帐户，然后选择 **[!UICONTROL 下一个]** 以继续。

![现有](../../../../images/tutorials/create/ibm-db2/existing.png)

## 后续步骤

按照本教程，您已建立与DB2帐户的连接。 您现在可以继续下一教程和 [配置数据流以将数据导入 [!DNL Platform]](../../dataflow/databases.md).
