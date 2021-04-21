---
keywords: Experience Platform；主页；热门主题；SFTP;sftp
solution: Experience Platform
title: 在UI中创建SFTP源连接
topic-legacy: overview
type: Tutorial
description: 了解如何使用Adobe Experience Platform UI创建SFTP源连接。
exl-id: 1a00ed27-3c95-4e57-9f94-45ff256bf75c
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '676'
ht-degree: 0%

---

# 在UI中创建SFTP源连接

本教程提供了使用Adobe Experience Platform UI创建SFTP源连接的步骤。

## 入门指南

本教程需要对Adobe Experience Platform的以下组件有充分的了解：

* [[!DNL Experience Data Model (XDM)] 系统](../../../../../xdm/home.md):Experience Platform组织客户体验数据的标准化框架。
   * [模式合成的基础](../../../../../xdm/schema/composition.md):了解XDM模式的基本构建基块，包括模式构成的主要原则和最佳做法。
   * [模式编辑器教程](../../../../../xdm/tutorials/create-schema-ui.md):了解如何使用模式编辑器UI创建自定义模式。
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md):根据来自多个来源的汇总数据提供统一、实时的消费者用户档案。

>[!IMPORTANT]
>
>建议在使用SFTP源连接引入JSON对象时避免换行或回车。 要解决限制问题，请对每行使用一个JSON对象，并对后续文件使用多行。

如果您已有有效的SFTP连接，则可以跳过此文档的其余部分，继续学习有关配置数据流](../../dataflow/batch/cloud-storage.md)的教程。[

### 收集所需凭据

要连接到SFTP，您必须为以下连接属性提供值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `host` | 与SFTP服务器关联的名称或IP地址。 |
| `username` | 有权访问您的SFTP服务器的用户名。 |
| `password` | SFTP服务器的密码。 |
| `privateKeyContent` | Base64编码的SSH私钥内容。 OpenSSH密钥的类型必须归类为RSA或DSA。 |
| `passPhrase` | 如果密钥文件或密钥内容受密码短语保护，则用于解密私钥的密码短语或密码。 如果PrivateKeyContent受口令保护，则此参数需要与PrivateKeyContent的密码短语一起使用作为值。 |

收集所需凭据后，您可以按照以下步骤创建新的SFTP帐户以连接到平台。

## 连接到SFTP服务器

登录到[Adobe Experience Platform](https://platform.adobe.com)，然后从左侧导航栏中选择&#x200B;**[!UICONTROL Sources]**&#x200B;以访问[!UICONTROL Sources]工作区。 [!UICONTROL Catalog]屏幕显示各种源，您可以为其创建入站帐户。

您可以从屏幕左侧的目录中选择适当的类别。 或者，您也可以使用搜索选项找到要使用的特定源。

在[!UICONTROL Cloud storage]类别下，选择&#x200B;**[!UICONTROL SFTP]**。 如果这是您首次使用此连接器，请选择&#x200B;**[!UICONTROL Configure]**。 否则，选择&#x200B;**[!UICONTROL Add data]**&#x200B;以创建新的SFTP连接。

![目录](../../../../images/tutorials/create/sftp/catalog.png)

将显示&#x200B;**[!UICONTROL Connect to SFTP]**&#x200B;页。 在此页上，您可以使用新凭据或现有凭据。

### 新帐户

如果您使用新凭据，请选择&#x200B;**[!UICONTROL New account]**。 在显示的输入表单上，提供名称、可选说明和凭据。 完成后，选择&#x200B;**[!UICONTROL Connect]**，然后为新连接建立留出一些时间。

SFTP连接器为您提供了不同的身份验证类型以供访问。 在&#x200B;**[!UICONTROL Account authentication]**&#x200B;下，选择&#x200B;**[!UICONTROL Password]**&#x200B;以使用基于口令的凭据。

![connect-password](../../../../images/tutorials/create/sftp/password.png)

或者，您也可以选择&#x200B;**[SSH公钥]**，并使用[!UICONTROL Private key content]和[!UICONTROL Passphrase]的组合连接您的SFTP帐户。

>[!IMPORTANT]
>
>SFTP连接器支持RSA或DSA类型的OpenSSH密钥。 确保关键文件内容开始为`"-----BEGIN [RSA/DSA] PRIVATE KEY-----"`，以`"-----END [RSA/DSA] PRIVATE KEY-----"`结尾。 如果私钥文件是PPK格式文件，请使用PuTTY工具从PPK格式转换为OpenSSH格式。

![connect-ssh](../../../../images/tutorials/create/sftp/ssh.png)

| 凭据 | 描述 |
| ---------- | ----------- |
| 私钥内容 | Base64编码的SSH私钥内容。 OpenSSH密钥的类型必须归类为RSA或DSA。 |
| 密码短语 | 指定密码短语或密码，以在密钥文件或密钥内容受密码短语保护时解密私钥。 如果PrivateKeyContent受口令保护，则此参数需要与PrivateKeyContent的密码短语一起使用作为值。 |

### 现有帐户

要连接现有帐户，请选择要连接的FTP或SFTP帐户，然后选择&#x200B;**[!UICONTROL Next]**&#x200B;以继续。

![现有](../../../../images/tutorials/create/sftp/existing.png)

## 后续步骤

通过本教程，您已建立了与FTP或SFTP帐户的连接。 您现在可以继续下一个教程，并[配置一个数据流，以将来自您的云存储的数据引入Platform](../../dataflow/batch/cloud-storage.md)。
