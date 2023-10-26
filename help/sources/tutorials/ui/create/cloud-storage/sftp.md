---
title: 在UI中创建SFTP源连接
description: 了解如何使用Adobe Experience Platform UI创建SFTP源连接。
exl-id: 1a00ed27-3c95-4e57-9f94-45ff256bf75c
source-git-commit: e92471b386b857fc21947d352f1c1b88431c68bc
workflow-type: tm+mt
source-wordcount: '820'
ht-degree: 0%

---

# 创建 [!DNL SFTP] UI中的源连接

本教程提供了创建 [!DNL SFTP] 源连接使用Adobe Experience Platform UI。

## 快速入门

本教程需要您对Platform的以下组件有一定的了解：

* [[!DNL Experience Data Model (XDM)] 系统](../../../../../xdm/home.md)：Experience Platform用于组织客户体验数据的标准化框架。
   * [模式组合基础](../../../../../xdm/schema/composition.md)：了解XDM架构的基本构建基块，包括架构构成中的关键原则和最佳实践。
   * [架构编辑器教程](../../../../../xdm/tutorials/create-schema-ui.md)：了解如何使用架构编辑器UI创建自定义架构。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md)：根据来自多个来源的汇总数据提供统一的实时使用者个人资料。

>[!IMPORTANT]
>
>建议在使用引入JSON对象时避免换行符或回车符 [!DNL SFTP] 源连接。 要解决此限制，请每行使用一个JSON对象，并使用多行来生成文件。

如果您已经拥有有效的 [!DNL SFTP] 连接，您可以跳过本文档的其余部分，并继续阅读以下教程： [配置数据流](../../dataflow/batch/cloud-storage.md).

### 收集所需的凭据

为了连接到 [!DNL SFTP]中，您必须提供以下连接属性的值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `host` | 与您的关联的名称或IP地址 [!DNL SFTP] 服务器。 |
| `port` | 此 [!DNL SFTP] 您正在连接的服务器端口。 如果未提供，则值默认为 `22`. |
| `username` | 对您的具有访问权限的用户名 [!DNL SFTP] 服务器。 |
| `password` | 您的密码 [!DNL SFTP] 服务器。 |
| `privateKeyContent` | Base64编码的SSH私钥内容。 OpenSSH密钥类型必须分类为RSA或DSA。 |
| `passPhrase` | 如果密钥文件或密钥内容受密码词组保护，则使用密码词组或密码解密私钥。 如果PrivateKeyContent受密码保护，则此参数需要与PrivateKeyContent的密码短语（值）一起使用。 |
| `maxConcurrentConnections` | 此参数允许您指定在连接到SFTP服务器时，平台将创建的并发连接数的最大限制。 必须将此值设置为小于SFTP设置的限制。 **注意**：为现有SFTP帐户启用此设置时，它仅影响未来的数据流，而不影响现有的数据流。 |
| 文件夹路径 | 要提供访问权限的文件夹的路径。 [!DNL SFTP] 源，您可以提供文件夹路径，以指定用户对所选子文件夹的访问权限。 |

收集所需的凭据后，您可以按照以下步骤创建新凭据 [!DNL SFTP] 用于连接到Platform的帐户。

## 连接到您的 [!DNL SFTP] 服务器

在Platform UI中，选择 **[!UICONTROL 源]** 从左侧导航栏访问 [!UICONTROL 源] 工作区。 此 [!UICONTROL 目录] 屏幕显示了多种来源，您可以使用这些来源创建帐户。

您可以从屏幕左侧的目录中选择相应的类别。 或者，您可以使用搜索选项查找您要使用的特定源。

在 [!UICONTROL 云存储] 类别，选择 **[!UICONTROL SFTP]** 然后选择 **[!UICONTROL 添加数据]**.

![选择了SFTP源的Experience Platform源目录。](../../../../images/tutorials/create/sftp/catalog.png)

此 **[!UICONTROL 连接到SFTP]** 页面。 在此页上，您可以使用新凭据或现有凭据。

### 现有帐户

要连接现有帐户，请选择要连接的FTP或SFTP帐户，然后选择 **[!UICONTROL 下一个]** 以继续。

![Experience PlatformUI上现有SFTP帐户的列表。](../../../../images/tutorials/create/sftp/existing.png)

### 新帐户

>[!TIP]
>
>* 创建后，便无法更改的身份验证类型 [!DNL SFTP] 基本连接。 要更改身份验证类型，必须创建新的基本连接。
>
>* SFTP支持RSA或DSA类型的OpenSSH密钥。 确保您的关键文件内容开头为 `"-----BEGIN [RSA/DSA] PRIVATE KEY-----"` 结束于 `"-----END [RSA/DSA] PRIVATE KEY-----"`. 如果私钥文件是PPK格式文件，请使用PuTTY工具从PPK转换为OpenSSH格式。

如果要创建新帐户，请选择 **[!UICONTROL 新帐户]**，然后为新页面提供名称和可选描述 [!DNL SFTP] 帐户。

![SFTP的新帐户屏幕](../../../../images/tutorials/create/sftp/new.png)

此 [!DNL SFTP] 源支持基本身份验证和通过SSH公钥进行的身份验证。

>[!BEGINTABS]

>[!TAB 基本身份验证]

要使用基本身份验证，请选择 **[!UICONTROL 密码]** 然后提供要连接的主机值和端口值，以及您的用户名和密码。 在此步骤中，您还可以指定要提供访问权限的子文件夹的路径。 完成后，选择 **[!UICONTROL 连接到源]**.

![使用基本身份验证的SFTP源的新帐户屏幕](../../../../images/tutorials/create/sftp/password.png)

>[!TAB SSH公钥身份验证]

要使用基于SSH公钥的凭据，请选择 **[!UICONTROL SSH公钥]**  然后提供主机和端口值，以及您的私钥内容和密码短语组合。 在此步骤中，您还可以指定要提供访问权限的子文件夹的路径。 完成后，选择 **[!UICONTROL 连接到源]**.

![使用SSH公钥的SFTP源的新帐户屏幕。](../../../../images/tutorials/create/sftp/ssh.png)

>[!ENDTABS]

## 后续步骤

通过学习本教程，您已建立与SFTP帐户的连接。 您现在可以继续下一教程和 [配置数据流以将数据从云存储引入Platform](../../dataflow/batch/cloud-storage.md).
