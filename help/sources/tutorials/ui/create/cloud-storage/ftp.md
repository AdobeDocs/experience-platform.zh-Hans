---
keywords: Experience Platform；主页；热门主题；FTP；ftp
solution: Experience Platform
title: 在UI中创建FTP Source连接
type: Tutorial
description: 了解如何使用Adobe Experience Platform UI创建FTP源连接。
exl-id: 8e505ead-4bae-43fe-830b-75620e8fba28
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '464'
ht-degree: 2%

---

# 在UI中创建FTP源连接

>[!NOTE]
>
>FTP连接器处于测试阶段。 有关使用带有Beta标记的连接器的更多信息，请参阅[源概述](../../../../home.md#terms-and-conditions)。

本教程提供了使用Adobe Experience Platform UI创建FTP源连接的步骤。

## 快速入门

本教程需要对以下Adobe Experience Platform组件有一定的了解：

* [[!DNL Experience Data Model (XDM)] 系统](../../../../../xdm/home.md)： Experience Platform用于组织客户体验数据的标准化框架。
   * [架构组合的基础知识](../../../../../xdm/schema/composition.md)：了解XDM架构的基本构建块，包括架构组合中的关键原则和最佳实践。
   * [架构编辑器教程](../../../../../xdm/tutorials/create-schema-ui.md)：了解如何使用架构编辑器UI创建自定义架构。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md)：根据来自多个源的汇总数据，提供统一的实时使用者个人资料。

如果您已经拥有有效的FTP连接，则可以跳过本文档的其余部分，并转到有关[配置数据流](../../dataflow/batch/cloud-storage.md)的教程。

### 收集所需的凭据

要连接到FTP，您必须提供以下连接属性的值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `host` | 与FTP服务器关联的名称或IP地址。 |
| `username` | 有权访问FTP服务器的用户名。 |
| `password` | FTP服务器的密码。 |

## 连接到FTP服务器

收集所需的凭据后，您可以按照以下步骤创建新的FTP帐户以连接到Experience Platform。

登录到[Adobe Experience Platform](https://platform.adobe.com)，然后从左侧导航栏中选择&#x200B;**[!UICONTROL 源]**&#x200B;以访问[!UICONTROL 源]工作区。 [!UICONTROL Catalog]屏幕显示您可以为其创建入站帐户的各种源。

您可以从屏幕左侧的目录中选择相应的类别。 或者，您可以使用搜索选项查找您要使用的特定源。

在[!UICONTROL 云存储]类别下，选择&#x200B;**[!UICONTROL FTP]**。 如果这是您第一次使用此连接器，请选择&#x200B;**[!UICONTROL 配置]**。 否则，请选择&#x200B;**[!UICONTROL 添加数据]**&#x200B;以创建新的FTP连接。

![目录](../../../../images/tutorials/create/ftp/catalog.png)

出现&#x200B;**[!UICONTROL 连接到FTP]**&#x200B;页面。 在此页上，您可以使用新凭据或现有凭据。

### 新帐户

如果您正在使用新凭据，请选择&#x200B;**[!UICONTROL 新帐户]**。 在出现的输入窗体上，提供名称、可选说明和您的凭据。 完成后，选择&#x200B;**[!UICONTROL 连接]**，然后留出一些时间来建立新连接。

![新](../../../../images/tutorials/create/ftp/new.png)

### 现有账户

要连接现有帐户，请选择您要连接的FTP帐户，然后选择&#x200B;**[!UICONTROL 下一步]**&#x200B;以继续。

![现有](../../../../images/tutorials/create/ftp/existing.png)

## 后续步骤

通过学习本教程，您已建立与FTP帐户的连接。 您现在可以继续阅读下一教程，并[配置数据流以将数据从云存储引入Experience Platform](../../dataflow/batch/cloud-storage.md)。
