---
keywords: Experience Platform;home;popular topics;FTP;ftp
solution: Experience Platform
title: 在UI中创建FTP源连接器
topic: overview
type: Tutorial
description: 本教程提供了使用平台用户界面创建FTP源连接器的步骤。
translation-type: tm+mt
source-git-commit: e28a3ec2d4330f0e9f3895e0236c9ebea2ef2776
workflow-type: tm+mt
source-wordcount: '456'
ht-degree: 1%

---


# 在UI中创建FTP源连接器

>[!NOTE]
>
>FTP连接器处于测试状态。 有关使用 [测试版标记](../../../../home.md#terms-and-conditions) 的连接器的更多信息，请参阅源概述。

本教程提供了使用平台用户界面创建FTP源连接器的步骤。

## 入门指南

本教程需要对Adobe Experience Platform的以下组件进行有效的理解：

* [[!DNL Experience Data Model (XDM)] 系统](../../../../../xdm/home.md):Experience Platform组织客户体验数据的标准化框架。
   * [模式合成基础](../../../../../xdm/schema/composition.md):了解XDM模式的基本构件，包括模式构成的主要原则和最佳做法。
   * [模式编辑器教程](../../../../../xdm/tutorials/create-schema-ui.md):了解如何使用模式编辑器UI创建自定义模式。
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md):基于来自多个来源的聚集数据提供统一、实时的消费者用户档案。

如果您已经有有效的FTP连接，您可以跳过此文档的其余部分，继续学习有关配置 [数据流的教程](../../dataflow/batch/cloud-storage.md)。

### 收集所需的凭据

要连接到FTP，您必须提供以下连接属性的值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `host` | 与您的FTP服务器关联的名称或IP地址。 |
| `username` | 有权访问FTP服务器的用户名。 |
| `password` | FTP服务器的密码。 |

## 连接到FTP服务器

收集所需凭据后，您可以按照以下步骤创建新FTP帐户以连接到平台。

登录到 [Adobe Experience Platform](https://platform.adobe.com) ，然后从左 **[!UICONTROL 侧导航栏]** 中选择 [!UICONTROL “源”以访问] “源”工作区。 “ [!UICONTROL 目录] ”屏幕显示可为其创建入站帐户的各种源。

您可以从屏幕左侧的目录中选择适当的类别。 或者，您也可以使用搜索选项找到要使用的特定源。

在“云 [!UICONTROL 存储] ”类别下 **[!UICONTROL ，选择FTP]**。 如果这是您首次使用此连接器，请选择“ **[!UICONTROL 配置]**”。 否则，选 **[!UICONTROL 择“添加]** ”以创建新FTP连接。

![目录](../../../../images/tutorials/create/ftp/catalog.png)

此时 **[!UICONTROL 将显示“连接到]** FTP”页。 在此页上，您可以使用新凭据或现有凭据。

### 新帐户

如果您使用新凭据，请选择“ **[!UICONTROL 新帐户]**”。 在显示的输入表单上，提供名称、可选说明和凭据。 完成后，选 **[!UICONTROL 择]** Connect，然后允许一段时间建立新连接。

![新](../../../../images/tutorials/create/ftp/new.png)

### 现有帐户

要连接现有帐户，请选择要连接的FTP帐户，然后选择“下 **[!UICONTROL 一步]** ”继续。

![现有](../../../../images/tutorials/create/ftp/existing.png)

## 后续步骤

按照本教程，您已建立了与FTP帐户的连接。 您现在可以继续阅读下一个教程 [并配置数据流，将数据从云存储引入平台](../../dataflow/batch/cloud-storage.md)。