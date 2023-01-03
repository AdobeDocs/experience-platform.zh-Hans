---
keywords: Experience Platform；主页；热门主题；DB2;DB2;IBM DB2;IBM db2
solution: Experience Platform
title: 在UI中创建IBM DB2源连接
topic-legacy: overview
type: Tutorial
description: 了解如何使用IBM UI创建Adobe Experience Platform DB2源连接。
exl-id: 69c99f94-9cb9-43ff-9315-ce166ab35a60
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '536'
ht-degree: 0%

---

# 在UI中创建IBM DB2源连接

>[!NOTE]
>
> IBM DB2连接器为测试版。 请参阅 [源概述](../../../../home.md#terms-and-conditions) 有关使用测试版标签的连接器的更多信息。

Adobe Experience Platform中的源连接器提供了按计划摄取外部源数据的功能。 本教程提供了使用 [!DNL Platform] 用户界面。

## 快速入门

本教程需要对Adobe Experience Platform的以下组件有一定的了解：

* [[!DNL Experience Data Model (XDM)] 系统](../../../../../xdm/home.md):标准化框架， [!DNL Experience Platform] 组织客户体验数据。
   * [架构组合的基础知识](../../../../../xdm/schema/composition.md):了解XDM模式的基本构建块，包括模式组合中的关键原则和最佳实践。
   * [模式编辑器教程](../../../../../xdm/tutorials/create-schema-ui.md):了解如何使用模式编辑器UI创建自定义模式。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md):根据来自多个来源的汇总数据提供统一的实时客户资料。

如果您已经拥有有效的DB2连接，则可以跳过本文档的其余部分并继续阅读上的教程 [配置数据流](../../dataflow/databases.md).

### 收集所需的凭据

以下部分提供了使用成功连接到DB2所需了解的其他信息 [!DNL Flow Service] API。

| 凭据 | 描述 |
| ---------- | ----------- |
| `server` | DB2服务器的名称。 您可以在服务器名称后面指定端口号，该名称以冒号分隔。 例如：server:port。 |
| `database` | DB2数据库的名称。 |
| `username` | 用于连接到DB2数据库的用户名。 |
| `password` | 您为用户名指定的用户帐户的密码。 |

有关入门的更多信息，请参阅 [此DB2文档](https://www.ibm.com/support/knowledgecenter/SSFMBX/com.ibm.swg.im.dashdb.doc/connecting/connect_credentials.html).

## 连接IBM DB2帐户

收集所需凭据后，可按照以下步骤将DB2帐户关联到 [!DNL Platform].

登录到 [Adobe Experience Platform](https://platform.adobe.com) 然后选择 **[!UICONTROL 源]** 从左侧导航栏访问 **[!UICONTROL 源]** 工作区。 的 **[!UICONTROL 目录]** 屏幕会显示您可为其创建帐户的各种源。

您可以从屏幕左侧的目录中选择相应的类别。 或者，您可以使用搜索选项找到要处理的特定源。

在 **[!UICONTROL 数据库]** 类别，选择 **[!UICONTROL IBM DB2]**. 如果这是您首次使用此连接器，请选择 **[!UICONTROL 配置]**. 否则，请选择 **[!UICONTROL 添加数据]** 创建新的DB2连接器。

![目录](../../../../images/tutorials/create/ibm-db2/catalog.png)

的 **[!UICONTROL 连接到IBM DB2]** 页面。 在此页面上，您可以使用新凭据或现有凭据。

### 新帐户

如果您使用新凭据，请选择 **[!UICONTROL 新帐户]**. 在显示的输入窗体中，提供名称、可选描述和您的DB2凭据。 完成后，选择 **[!UICONTROL 连接]** 然后，再留出一些时间建立新连接。

![connect](../../../../images/tutorials/create/ibm-db2/new.png)

### 现有帐户

要连接现有帐户，请选择要连接的DB2帐户，然后选择 **[!UICONTROL 下一个]** 以继续。

![现有](../../../../images/tutorials/create/ibm-db2/existing.png)

## 后续步骤

在本教程中，您已建立与DB2帐户的连接。 您现在可以继续下一个教程和 [配置数据流以将数据导入 [!DNL Platform]](../../dataflow/databases.md).
