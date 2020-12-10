---
keywords: Experience Platform;home;popular topics;SFTP;sftp
solution: Experience Platform
title: 在UI中创建SFTP源连接器
topic: overview
type: Tutorial
description: 本教程提供了使用平台用户界面创建SFTP源连接器的步骤。
translation-type: tm+mt
source-git-commit: 7b638f0516804e6a2dbae3982d6284a958230f42
workflow-type: tm+mt
source-wordcount: '659'
ht-degree: 0%

---


# 在UI中创建SFTP源连接器

>[!NOTE]
>
>SFTP连接器处于测试状态。 有关使用 [测试版标记](../../../../home.md#terms-and-conditions) 的连接器的更多信息，请参阅源概述。

本教程提供了使用平台用户界面创建SFTP源连接器的步骤。

## 入门指南

本教程需要对Adobe Experience Platform的以下组件进行有效的理解：

* [[!DNL Experience Data Model (XDM)] 系统](../../../../../xdm/home.md):Experience Platform组织客户体验数据的标准化框架。
   * [模式合成基础](../../../../../xdm/schema/composition.md):了解XDM模式的基本构件，包括模式构成的主要原则和最佳做法。
   * [模式编辑器教程](../../../../../xdm/tutorials/create-schema-ui.md):了解如何使用模式编辑器UI创建自定义模式。
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md):基于来自多个来源的聚集数据提供统一、实时的消费者用户档案。

如果您已经有有效的SFTP连接，您可以跳过本文档的其余部分，继续学习有关配置 [数据流的教程](../../dataflow/batch/cloud-storage.md)。

### 收集所需的凭据

要连接到SFTP，必须为以下连接属性提供值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `host` | 与您的SFTP服务器关联的名称或IP地址。 |
| `username` | 有权访问SFTP服务器的用户名。 |
| `password` | SFTP服务器的口令。 |
| `privateKeyContent` | Base64编码的SSH私钥内容。 SSH私钥OpenSSH(RSA/DSA)格式。 |
| `passPhrase` | 如果密钥文件或密钥内容受密码短语保护，则用于解密私钥的密码或密码。 如果PrivateKeyContent是密码保护的，则此参数需要与PrivateKeyContent的密码短语一起使用作值。 |

收集所需凭据后，您可以按照以下步骤创建新SFTP帐户以连接到平台。

## 连接到SFTP服务器

登录到 [Adobe Experience Platform](https://platform.adobe.com) ，然后从左 **[!UICONTROL 侧导航栏]** 中选择 [!UICONTROL “源”以访问] “源”工作区。 “ [!UICONTROL 目录] ”屏幕显示可为其创建入站帐户的各种源。

您可以从屏幕左侧的目录中选择适当的类别。 或者，您也可以使用搜索选项找到要使用的特定源。

在“云 [!UICONTROL 存储] ”类别下 **[!UICONTROL ，选择SFTP]**。 如果这是您首次使用此连接器，请选择“ **[!UICONTROL 配置]**”。 否则，选 **[!UICONTROL 择“添加数]** 据”以创建新SFTP连接。

![目录](../../../../images/tutorials/create/sftp/catalog.png)

此时 **[!UICONTROL 将显示“连接到]** SFTP”页。 在此页上，您可以使用新凭据或现有凭据。

### 新帐户

如果您使用新凭据，请选择“ **[!UICONTROL 新帐户]**”。 在显示的输入表单上，提供名称、可选说明和凭据。 完成后，选 **[!UICONTROL 择]** Connect，然后允许一段时间建立新连接。

SFTP连接器为您提供不同的身份验证类型以供访问。 在“ **[!UICONTROL 帐户身份]** ” **[!UICONTROL 下]** ，选择“口令”以使用基于口令的凭据。

![connect-password](../../../../images/tutorials/create/sftp/password.png)

或者，您也可以选 **[择SSH公钥]** ，并使用私钥内容和密码短语 [!UICONTROL 组合连接您的SFTP] 帐户 。

>[!IMPORTANT]
>
>SFTP连接器支持RSA/DSA OpenSSH密钥。 确保关键文件内容与开始 `"-----BEGIN [RSA/DSA] PRIVATE KEY-----"`。 如果私钥文件是PPK格式文件，请使用PuTTY工具从PPK格式转换为OpenSSH格式。

![connect-ssh](../../../../images/tutorials/create/sftp/ssh.png)

| 凭据 | 描述 |
| ---------- | ----------- |
| 私钥内容 | Base64编码的SSH私钥内容。 SSH私钥应为OpenSSH格式。 |
| 密码短语 | 指定密码短语或密码，以便在密钥文件或密钥内容受密码短语保护时解密私钥。 如果PrivateKeyContent是密码保护的，则此参数需要与PrivateKeyContent的密码短语一起使用作值。 |

### 现有帐户

要连接现有帐户，请选择要连接的FTP或SFTP帐户，然后选择下 **[!UICONTROL 一]** 步以继续。

![现有](../../../../images/tutorials/create/sftp/existing.png)

## 后续步骤

按照本教程，您已建立了与FTP或SFTP帐户的连接。 您现在可以继续阅读下一个教程 [并配置数据流，将数据从云存储引入平台](../../dataflow/batch/cloud-storage.md)。