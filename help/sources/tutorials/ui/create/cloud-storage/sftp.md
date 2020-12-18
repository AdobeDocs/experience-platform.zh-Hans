---
keywords: Experience Platform;home;popular topics;SFTP;sftp
solution: Experience Platform
title: 在UI中创建SFTP源连接器
topic: overview
type: Tutorial
description: 本教程提供了使用平台用户界面创建SFTP源连接器的步骤。
translation-type: tm+mt
source-git-commit: 0d0d3aa4213f3a8252de82c47eef6e9caa4d3e9e
workflow-type: tm+mt
source-wordcount: '695'
ht-degree: 0%

---


# 在UI中创建SFTP源连接器

>[!NOTE]
>
>SFTP连接器处于测试状态。 有关使用测试版标签的连接器的详细信息，请参见[源概述](../../../../home.md#terms-and-conditions)。

本教程提供了使用平台用户界面创建SFTP源连接器的步骤。

## 入门指南

本教程需要对Adobe Experience Platform的以下组件进行有效的理解：

* [[!DNL Experience Data Model (XDM)] 系统](../../../../../xdm/home.md):Experience Platform组织客户体验数据的标准化框架。
   * [模式合成基础](../../../../../xdm/schema/composition.md):了解XDM模式的基本构件，包括模式构成的主要原则和最佳做法。
   * [模式编辑器教程](../../../../../xdm/tutorials/create-schema-ui.md):了解如何使用模式编辑器UI创建自定义模式。
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md):基于来自多个来源的聚集数据提供统一、实时的消费者用户档案。

>[!IMPORTANT]
>
>建议在使用SFTP源连接引入JSON对象时避免换行或回车。 要绕过限制，请每行使用一个JSON对象，然后使用多行生成后续文件。

如果您已经有有效的SFTP连接，您可以跳过此文档的其余部分，继续学习有关配置数据流[的教程。](../../dataflow/batch/cloud-storage.md)

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

登录到[Adobe Experience Platform](https://platform.adobe.com)，然后从左侧导航栏中选择&#x200B;**[!UICONTROL 源]**&#x200B;以访问[!UICONTROL 源]工作区。 [!UICONTROL 目录]屏幕显示各种源，您可以为其创建入站帐户。

您可以从屏幕左侧的目录中选择适当的类别。 或者，您也可以使用搜索选项找到要使用的特定源。

在[!UICONTROL 云存储]类别下，选择&#x200B;**[!UICONTROL SFTP]**。 如果这是您首次使用此连接器，请选择&#x200B;**[!UICONTROL 配置]**。 否则，选择&#x200B;**[!UICONTROL 添加数据]**&#x200B;以创建新的SFTP连接。

![目录](../../../../images/tutorials/create/sftp/catalog.png)

将显示&#x200B;**[!UICONTROL 连接到SFTP]**&#x200B;页。 在此页上，您可以使用新凭据或现有凭据。

### 新帐户

如果您使用新凭据，请选择&#x200B;**[!UICONTROL 新建帐户]**。 在显示的输入表单上，提供名称、可选说明和凭据。 完成后，选择&#x200B;**[!UICONTROL Connect]**，然后为新连接建立留出一些时间。

SFTP连接器为您提供不同的身份验证类型以供访问。 在&#x200B;**[!UICONTROL 帐户身份验证]**&#x200B;下，选择&#x200B;**[!UICONTROL 密码]**&#x200B;以使用基于密码的凭据。

![connect-password](../../../../images/tutorials/create/sftp/password.png)

或者，您也可以选择&#x200B;**[SSH公钥]**，并结合使用[!UICONTROL 私钥内容]和[!UICONTROL 密码]连接您的SFTP帐户。

>[!IMPORTANT]
>
>SFTP连接器支持RSA/DSA OpenSSH密钥。 确保关键文件内容开始为`"-----BEGIN [RSA/DSA] PRIVATE KEY-----"`。 如果私钥文件是PPK格式文件，请使用PuTTY工具从PPK格式转换为OpenSSH格式。

![connect-ssh](../../../../images/tutorials/create/sftp/ssh.png)

| 凭据 | 描述 |
| ---------- | ----------- |
| 私钥内容 | Base64编码的SSH私钥内容。 SSH私钥应为OpenSSH格式。 |
| 密码短语 | 指定密码短语或密码，以便在密钥文件或密钥内容受密码短语保护时解密私钥。 如果PrivateKeyContent是密码保护的，则此参数需要与PrivateKeyContent的密码短语一起使用作值。 |

### 现有帐户

要连接现有帐户，请选择要连接的FTP或SFTP帐户，然后选择&#x200B;**[!UICONTROL 下一步]**&#x200B;继续。

![现有](../../../../images/tutorials/create/sftp/existing.png)

## 后续步骤

按照本教程，您已建立了与FTP或SFTP帐户的连接。 您现在可以继续阅读下一个教程，并[配置数据流，将数据从您的云存储引入平台](../../dataflow/batch/cloud-storage.md)。