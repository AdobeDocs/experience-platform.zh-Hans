---
title: 在UI中创建SFTP Source连接
description: 了解如何使用Adobe Experience Platform UI创建SFTP源连接。
exl-id: 1a00ed27-3c95-4e57-9f94-45ff256bf75c
source-git-commit: f6d1cc811378f2f37968bf0a42b428249e52efd8
workflow-type: tm+mt
source-wordcount: '820'
ht-degree: 1%

---

# 在用户界面中创建[!DNL SFTP]源连接

本教程提供了使用Adobe Experience Platform UI创建[!DNL SFTP]源连接的步骤。

## 快速入门

本教程需要您对Platform的以下组件有一定的了解：

* [[!DNL Experience Data Model (XDM)] 系统](../../../../../xdm/home.md)：Experience Platform用于组织客户体验数据的标准化框架。
   * [架构组合的基础知识](../../../../../xdm/schema/composition.md)：了解XDM架构的基本构建块，包括架构组合中的关键原则和最佳实践。
   * [架构编辑器教程](../../../../../xdm/tutorials/create-schema-ui.md)：了解如何使用架构编辑器UI创建自定义架构。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md)：根据来自多个源的汇总数据，提供统一的实时使用者个人资料。

>[!IMPORTANT]
>
>建议在摄取具有[!DNL SFTP]源连接的JSON对象时避免换行符或回车符。 要解决此限制，请每行使用一个JSON对象，并使用多行来生成文件。

如果您已经拥有有效的[!DNL SFTP]连接，则可以跳过本文档的其余部分，并转到有关[配置数据流](../../dataflow/batch/cloud-storage.md)的教程。

### 收集所需的凭据

要连接到[!DNL SFTP]，您必须提供以下连接属性的值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `host` | 与您的[!DNL SFTP]服务器关联的名称或IP地址。 |
| `port` | 您正在连接的[!DNL SFTP]服务器端口。 如果未提供，则值默认为`22`。 |
| `username` | 有权访问您的[!DNL SFTP]服务器的用户名。 |
| `password` | [!DNL SFTP]服务器的密码。 |
| `privateKeyContent` | Base64编码的SSH私钥内容。 OpenSSH密钥类型必须分类为RSA或DSA。 |
| `passPhrase` | 如果密钥文件或密钥内容受密码词组保护，则使用密码词组或密码解密私钥。 如果PrivateKeyContent受密码保护，则此参数需要与PrivateKeyContent的密码短语（值）一起使用。 |
| `maxConcurrentConnections` | 此参数允许您指定在连接到SFTP服务器时，平台将创建的并发连接数的最大限制。 必须将此值设置为小于SFTP设置的限制。 **注意**：为现有SFTP帐户启用此设置时，它只影响未来的数据流，而不影响现有的数据流。 |
| 文件夹路径 | 要提供访问权限的文件夹的路径。 [!DNL SFTP]源，您可以提供文件夹路径，以指定用户对所选子文件夹的访问权限。 |

收集完所需的凭据后，您可以按照以下步骤创建新的[!DNL SFTP]帐户以连接到Platform。

## 连接到[!DNL SFTP]服务器

在Platform UI中，从左侧导航栏中选择&#x200B;**[!UICONTROL 源]**&#x200B;以访问[!UICONTROL 源]工作区。 [!UICONTROL Catalog]屏幕显示您可以用来创建帐户的各种源。

您可以从屏幕左侧的目录中选择相应的类别。 或者，您可以使用搜索选项查找您要使用的特定源。

在[!UICONTROL 云存储]类别下，选择&#x200B;**[!UICONTROL SFTP]**，然后选择&#x200B;**[!UICONTROL 添加数据]**。

![已选择SFTP源的Experience Platform源目录。](../../../../images/tutorials/create/sftp/catalog.png)

出现&#x200B;**[!UICONTROL 连接到SFTP]**&#x200B;页面。 在此页上，您可以使用新凭据或现有凭据。

### 现有账户

要连接现有帐户，请选择您要连接的FTP或SFTP帐户，然后选择&#x200B;**[!UICONTROL 下一步]**&#x200B;以继续。

![Experience PlatformUI上现有SFTP帐户的列表。](../../../../images/tutorials/create/sftp/existing.png)

### 新帐户

>[!TIP]
>
>* 创建后，无法更改[!DNL SFTP]基本连接的身份验证类型。 要更改身份验证类型，必须创建新的基本连接。
>
>* SFTP支持RSA或DSA类型的OpenSSH密钥。 确保您的密钥文件内容以`"-----BEGIN [RSA/DSA] PRIVATE KEY-----"`开头并以`"-----END [RSA/DSA] PRIVATE KEY-----"`结尾。 如果私钥文件是PPK格式文件，请使用PuTTY工具从PPK转换为OpenSSH格式。

如果要创建新帐户，请选择&#x200B;**[!UICONTROL 新帐户]**，然后为您的新[!DNL SFTP]帐户提供名称和可选描述。

![SFTP的新帐户屏幕](../../../../images/tutorials/create/sftp/new.png)

[!DNL SFTP]源支持基本身份验证和通过SSH公钥的身份验证。

>[!BEGINTABS]

>[!TAB 基本身份验证]

要使用基本身份验证，请选择&#x200B;**[!UICONTROL 密码]**，然后提供要连接的主机值和端口值，以及您的用户名和密码。 在此步骤中，您还可以指定要提供访问权限的子文件夹的路径。 完成后，选择&#x200B;**[!UICONTROL 连接到源]**。

![使用基本身份验证的SFTP源的新帐户屏幕](../../../../images/tutorials/create/sftp/password.png)

>[!TAB SSH公钥身份验证]

要使用基于SSH公钥的凭据，请选择&#x200B;**[!UICONTROL SSH公钥]**，然后提供主机和端口值以及私钥内容和密码组合。 在此步骤中，您还可以指定要提供访问权限的子文件夹的路径。 完成后，选择&#x200B;**[!UICONTROL 连接到源]**。

![使用SSH公钥的SFTP源的新帐户屏幕。](../../../../images/tutorials/create/sftp/ssh.png)

>[!ENDTABS]

## 后续步骤

通过学习本教程，您已建立与SFTP帐户的连接。 您现在可以继续下一教程，并[配置数据流以将数据从云存储引入Platform](../../dataflow/batch/cloud-storage.md)。
