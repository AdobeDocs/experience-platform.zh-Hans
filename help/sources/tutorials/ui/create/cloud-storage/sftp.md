---
keywords: Experience Platform；主页；热门主题；SFTP;SFTP
solution: Experience Platform
title: 在UI中创建SFTP源连接
topic-legacy: overview
type: Tutorial
description: 了解如何使用Adobe Experience Platform UI创建SFTP源连接。
exl-id: 1a00ed27-3c95-4e57-9f94-45ff256bf75c
source-git-commit: ade0da445b18108a7f8720404cc7a65139ed42b1
workflow-type: tm+mt
source-wordcount: '680'
ht-degree: 0%

---

# 在UI中创建[!DNL SFTP]源连接

本教程提供了使用Adobe Experience Platform UI创建[!DNL SFTP]源连接的步骤。

## 快速入门

本教程需要对Platform的以下组件有一定的了解：

* [[!DNL Experience Data Model (XDM)] 系统](../../../../../xdm/home.md):Experience Platform组织客户体验数据的标准化框架。
   * [架构组合的基础知识](../../../../../xdm/schema/composition.md):了解XDM模式的基本构建块，包括模式组合中的关键原则和最佳实践。
   * [模式编辑器教程](../../../../../xdm/tutorials/create-schema-ui.md):了解如何使用模式编辑器UI创建自定义模式。
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md):根据来自多个来源的汇总数据提供统一的实时客户资料。

>[!IMPORTANT]
>
>建议在摄取具有[!DNL SFTP]源连接的JSON对象时避免换行符或回车符。 要绕过限制，请每行使用一个JSON对象，并使用多行来生成后续文件。

如果您已经拥有有效的[!DNL SFTP]连接，则可以跳过本文档的其余部分，继续阅读有关[配置数据流](../../dataflow/batch/cloud-storage.md)的教程。

### 收集所需的凭据

要连接到[!DNL SFTP]，必须为以下连接属性提供值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `host` | 与[!DNL SFTP]服务器关联的名称或IP地址。 |
| `port` | 您正在连接的[!DNL SFTP]服务器端口。 如果未提供，则该值默认为`22`。 |
| `username` | 具有[!DNL SFTP]服务器访问权限的用户名。 |
| `password` | [!DNL SFTP]服务器的密码。 |
| `privateKeyContent` | Base64编码的SSH私钥内容。 OpenSSH密钥的类型必须分类为RSA或DSA。 |
| `passPhrase` | 如果密钥文件或密钥内容受密码短语的保护，则解密私钥的密码短语或密码。 如果PrivateKeyContent受密码保护，则此参数需要与PrivateKeyContent的密码短语一起用作值。 |

收集所需凭据后，您可以按照以下步骤创建新的[!DNL SFTP]帐户以连接到平台。

## 连接到[!DNL SFTP]服务器

在平台UI中，从左侧导航栏中选择&#x200B;**[!UICONTROL Sources]**&#x200B;以访问[!UICONTROL Sources]工作区。 [!UICONTROL Catalog]屏幕显示各种源，您可以为其创建入站帐户。

您可以从屏幕左侧的目录中选择相应的类别。 或者，您可以使用搜索选项找到要处理的特定源。

在[!UICONTROL 云存储]类别下，选择&#x200B;**[!UICONTROL SFTP]**，然后选择&#x200B;**[!UICONTROL 添加数据]**。

![目录](../../../../images/tutorials/create/sftp/catalog.png)

此时会显示&#x200B;**[!UICONTROL 连接到SFTP]**&#x200B;页面。 在此页面上，您可以使用新凭据或现有凭据。

### 现有帐户

要连接现有帐户，请选择要连接的FTP或SFTP帐户，然后选择&#x200B;**[!UICONTROL Next]**&#x200B;以继续。

![现有](../../../../images/tutorials/create/sftp/existing.png)

### 新帐户

如果要创建新帐户，请选择&#x200B;**[!UICONTROL 新建帐户]**，然后为新[!DNL SFTP]帐户提供名称和可选描述。

#### 使用密码进行身份验证

[!DNL SFTP] 支持不同的身份验证类型进行访问。在&#x200B;**[!UICONTROL 帐户身份验证]**&#x200B;下，选择&#x200B;**[!UICONTROL 密码]**，然后提供主机和端口值以连接到，同时提供您的用户名和密码。

![connect-password](../../../../images/tutorials/create/sftp/password.png)

#### 使用SSH公钥进行身份验证

要使用基于SSH公钥的凭据，请选择&#x200B;**[!UICONTROL SSH公钥]** ，然后提供主机和端口值以及私钥内容和密码组合。

>[!IMPORTANT]
>
>SFTP支持RSA或DSA类型OpenSSH密钥。 确保您的关键文件内容以`"-----BEGIN [RSA/DSA] PRIVATE KEY-----"`开头并以`"-----END [RSA/DSA] PRIVATE KEY-----"`结尾。 如果私钥文件是PPK格式的文件，请使用PuTTY工具将PPK格式转换为OpenSSH格式。

![connect-ssh](../../../../images/tutorials/create/sftp/ssh-public-key.png)

| 凭据 | 描述 |
| ---------- | ----------- |
| 私钥内容 | Base64编码的SSH私钥内容。 OpenSSH密钥的类型必须分类为RSA或DSA。 |
| 密码短语 | 如果密钥文件或密钥内容受密码短语保护，则指定用于解密私钥的密码或密码。 如果PrivateKeyContent受密码保护，则此参数需要与PrivateKeyContent的密码短语一起用作其值。 |


## 后续步骤

在本教程中，您已建立与SFTP帐户的连接。 您现在可以继续阅读下一个教程，并[配置数据流，以将云存储中的数据导入Platform](../../dataflow/batch/cloud-storage.md)。
