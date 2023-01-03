---
keywords: Experience Platform；主页；热门主题；FTP;FTP
solution: Experience Platform
title: 在UI中创建FTP源连接
topic-legacy: overview
type: Tutorial
description: 了解如何使用Adobe Experience Platform UI创建FTP源连接。
exl-id: 8e505ead-4bae-43fe-830b-75620e8fba28
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '463'
ht-degree: 1%

---

# 在UI中创建FTP源连接

>[!NOTE]
>
>FTP连接器处于测试阶段。 请参阅 [源概述](../../../../home.md#terms-and-conditions) 有关使用测试版标签的连接器的更多信息。

本教程提供了使用Adobe Experience Platform UI创建FTP源连接的步骤。

## 快速入门

本教程需要对Adobe Experience Platform的以下组件有一定的了解：

* [[!DNL Experience Data Model (XDM)] 系统](../../../../../xdm/home.md):Experience Platform组织客户体验数据的标准化框架。
   * [架构组合的基础知识](../../../../../xdm/schema/composition.md):了解XDM模式的基本构建块，包括模式组合中的关键原则和最佳实践。
   * [模式编辑器教程](../../../../../xdm/tutorials/create-schema-ui.md):了解如何使用模式编辑器UI创建自定义模式。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md):根据来自多个来源的汇总数据提供统一的实时客户资料。

如果您已经拥有有效的FTP连接，则可以跳过本文档的其余部分，并继续阅读上的教程 [配置数据流](../../dataflow/batch/cloud-storage.md).

### 收集所需的凭据

要连接到FTP，必须为以下连接属性提供值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `host` | 与FTP服务器关联的名称或IP地址。 |
| `username` | 有权访问您的FTP服务器的用户名。 |
| `password` | FTP服务器的密码。 |

## 连接到FTP服务器

收集所需的凭据后，可以按照以下步骤创建新的FTP帐户以连接到平台。

登录到 [Adobe Experience Platform](https://platform.adobe.com) 然后选择 **[!UICONTROL 源]** 从左侧导航栏访问 [!UICONTROL 源] 工作区。 的 [!UICONTROL 目录] 屏幕会显示您可为其创建入站帐户的各种源。

您可以从屏幕左侧的目录中选择相应的类别。 或者，您可以使用搜索选项找到要处理的特定源。

在 [!UICONTROL 云存储] 类别，选择 **[!UICONTROL FTP]**. 如果这是您首次使用此连接器，请选择 **[!UICONTROL 配置]**. 否则，请选择 **[!UICONTROL 添加数据]** 创建新的FTP连接。

![目录](../../../../images/tutorials/create/ftp/catalog.png)

的 **[!UICONTROL 连接到FTP]** 页面。 在此页面上，您可以使用新凭据或现有凭据。

### 新帐户

如果您使用新凭据，请选择 **[!UICONTROL 新帐户]**. 在显示的输入窗体中，提供名称、可选描述和您的凭据。 完成后，选择 **[!UICONTROL 连接]** 然后，再留出一些时间建立新连接。

![新建](../../../../images/tutorials/create/ftp/new.png)

### 现有帐户

要连接现有帐户，请选择要连接的FTP帐户，然后选择 **[!UICONTROL 下一个]** 以继续。

![现有](../../../../images/tutorials/create/ftp/existing.png)

## 后续步骤

在本教程中，您已建立与FTP帐户的连接。 您现在可以继续下一个教程和 [配置数据流，以将云存储中的数据引入平台](../../dataflow/batch/cloud-storage.md).
