---
keywords: Experience Platform；主页；热门主题；SFTP;SFTP
solution: Experience Platform
title: 在UI中创建SFTP源连接
type: Tutorial
description: 了解如何使用Adobe Experience Platform UI创建SFTP源连接。
exl-id: 1a00ed27-3c95-4e57-9f94-45ff256bf75c
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '785'
ht-degree: 0%

---

# 创建 [!DNL SFTP] UI中的源连接

本教程提供了创建 [!DNL SFTP] 源连接。

## 快速入门

本教程需要对Platform的以下组件有一定的了解：

* [[!DNL Experience Data Model (XDM)] 系统](../../../../../xdm/home.md):Experience Platform组织客户体验数据的标准化框架。
   * [架构组合的基础知识](../../../../../xdm/schema/composition.md):了解XDM模式的基本构建块，包括模式组合中的关键原则和最佳实践。
   * [模式编辑器教程](../../../../../xdm/tutorials/create-schema-ui.md):了解如何使用模式编辑器UI创建自定义模式。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md):根据来自多个来源的汇总数据提供统一的实时客户资料。

>[!IMPORTANT]
>
>在使用 [!DNL SFTP] 源连接。 要绕过限制，请每行使用一个JSON对象，并使用多行来生成后续文件。

如果您已经拥有 [!DNL SFTP] 连接时，您可以跳过本文档的其余部分，并继续阅读上的教程 [配置数据流](../../dataflow/batch/cloud-storage.md).

### 收集所需的凭据

为了连接到 [!DNL SFTP]，则必须为以下连接属性提供值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `host` | 与您的 [!DNL SFTP] 服务器。 |
| `port` | 的 [!DNL SFTP] 您连接到的服务器端口。 如果未提供，则值默认为 `22`. |
| `username` | 有权访问您的 [!DNL SFTP] 服务器。 |
| `password` | 您的密码 [!DNL SFTP] 服务器。 |
| `privateKeyContent` | Base64编码的SSH私钥内容。 OpenSSH密钥的类型必须分类为RSA或DSA。 |
| `passPhrase` | 如果密钥文件或密钥内容受密码短语的保护，则解密私钥的密码短语或密码。 如果PrivateKeyContent受密码保护，则此参数需要与PrivateKeyContent的密码短语一起用作值。 |
| `maxConcurrentConnections` | 此参数允许您为平台在连接到SFTP服务器时将创建的并发连接数指定最大限制。 您必须将此值设置为小于SFTP设置的限制。 **注意**:为现有SFTP帐户启用此设置后，它只会影响将来的数据流，而不会影响现有的数据流。 |

收集所需的凭据后，您可以按照以下步骤创建新凭据 [!DNL SFTP] 帐户连接到平台。

## 连接到 [!DNL SFTP] 服务器

在平台UI中，选择 **[!UICONTROL 源]** 从左侧导航栏访问 [!UICONTROL 源] 工作区。 的 [!UICONTROL 目录] 屏幕会显示您可为其创建入站帐户的各种源。

您可以从屏幕左侧的目录中选择相应的类别。 或者，您可以使用搜索选项找到要处理的特定源。

在 [!UICONTROL 云存储] 类别，选择 **[!UICONTROL SFTP]** 然后选择 **[!UICONTROL 添加数据]**.

![选择SFTP源的Experience Platform源目录。](../../../../images/tutorials/create/sftp/catalog.png)

的 **[!UICONTROL 连接到SFTP]** 页面。 在此页面上，您可以使用新凭据或现有凭据。

### 现有帐户

要连接现有帐户，请选择要连接的FTP或SFTP帐户，然后选择 **[!UICONTROL 下一个]** 以继续。

![Experience PlatformUI中现有SFTP帐户的列表。](../../../../images/tutorials/create/sftp/existing.png)

### 新帐户

如果要创建新帐户，请选择 **[!UICONTROL 新帐户]**，然后为新用户提供名称和可选描述 [!DNL SFTP] 帐户。

![SFTP的新帐户屏幕](../../../../images/tutorials/create/sftp/new.png)

#### 使用密码进行身份验证

[!DNL SFTP] 支持不同的身份验证类型进行访问。 在 **[!UICONTROL 帐户身份验证]** 选择 **[!UICONTROL 密码]** 然后，提供要连接到的主机和端口值以及您的用户名和密码。

![SFTP源使用基本身份验证的新帐户屏幕](../../../../images/tutorials/create/sftp/password.png)

#### 使用SSH公钥进行身份验证

要使用基于SSH公钥的凭据，请选择 **[!UICONTROL SSH公钥]**  然后提供主机和端口值，以及私钥内容和密码组合。

>[!IMPORTANT]
>
>SFTP支持RSA或DSA类型OpenSSH密钥。 确保关键文件内容以 `"-----BEGIN [RSA/DSA] PRIVATE KEY-----"` 结尾为 `"-----END [RSA/DSA] PRIVATE KEY-----"`. 如果私钥文件是PPK格式的文件，请使用PuTTY工具将PPK格式转换为OpenSSH格式。

![使用SSH公钥的SFTP源的新帐户屏幕。](../../../../images/tutorials/create/sftp/ssh.png)

| 凭据 | 描述 |
| ---------- | ----------- |
| 私钥内容 | Base64编码的SSH私钥内容。 OpenSSH密钥的类型必须分类为RSA或DSA。 |
| 密码短语 | 如果密钥文件或密钥内容受密码短语保护，则指定用于解密私钥的密码或密码。 如果PrivateKeyContent受密码保护，则此参数需要与PrivateKeyContent的密码短语一起用作其值。 |


## 后续步骤

在本教程中，您已建立与SFTP帐户的连接。 您现在可以继续下一个教程和 [配置数据流，以将云存储中的数据引入平台](../../dataflow/batch/cloud-storage.md).
