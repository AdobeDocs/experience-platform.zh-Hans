---
title: 在UI中创建SFTP Source连接
description: 了解如何使用Adobe Experience Platform UI创建SFTP源连接。
exl-id: 1a00ed27-3c95-4e57-9f94-45ff256bf75c
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '665'
ht-degree: 1%

---

# 在用户界面中创建[!DNL SFTP]源连接

本教程提供了使用Adobe Experience Platform UI创建[!DNL SFTP]源连接的步骤。

## 快速入门

本教程需要对以下Experience Platform组件有一定的了解：

* [[!DNL Experience Data Model (XDM)] 系统](../../../../../xdm/home.md)： Experience Platform用于组织客户体验数据的标准化框架。
   * [架构组合的基础知识](../../../../../xdm/schema/composition.md)：了解XDM架构的基本构建块，包括架构组合中的关键原则和最佳实践。
   * [架构编辑器教程](../../../../../xdm/tutorials/create-schema-ui.md)：了解如何使用架构编辑器UI创建自定义架构。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md)：根据来自多个源的汇总数据，提供统一的实时使用者个人资料。

>[!IMPORTANT]
>
>建议在摄取具有[!DNL SFTP]源连接的JSON对象时避免换行符或回车符。 要解决此限制，请每行使用一个JSON对象，并使用多行来生成文件。

如果您已经拥有有效的[!DNL SFTP]连接，则可以跳过本文档的其余部分，并转到有关[配置数据流](../../dataflow/batch/cloud-storage.md)的教程。

### 收集所需的凭据

有关如何检索身份验证凭据的详细步骤，请阅读[[!DNL SFTP] 身份验证指南](../../../../connectors/cloud-storage/sftp.md#gather-required-credentials)。

## 连接到[!DNL SFTP]服务器

在Experience Platform UI中，从左侧导航栏中选择&#x200B;**[!UICONTROL 源]**&#x200B;以访问[!UICONTROL 源]工作区。 [!UICONTROL Catalog]屏幕显示您可以用来创建帐户的各种源。

您可以从屏幕左侧的目录中选择相应的类别。 或者，您可以使用搜索选项查找您要使用的特定源。

在[!UICONTROL 云存储]类别下，选择&#x200B;**[!UICONTROL SFTP]**，然后选择&#x200B;**[!UICONTROL 添加数据]**。

![已选择SFTP源的Experience Platform源目录。](../../../../images/tutorials/create/sftp/catalog.png)

出现&#x200B;**[!UICONTROL 连接到SFTP]**&#x200B;页面。 在此页上，您可以使用新凭据或现有凭据。

### 现有账户

要连接现有帐户，请选择您要连接的FTP或SFTP帐户，然后选择&#x200B;**[!UICONTROL 下一步]**&#x200B;以继续。

![Experience Platform UI上现有SFTP帐户的列表。](../../../../images/tutorials/create/sftp/existing.png)

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

若要使用基本身份验证，请选择&#x200B;**[!UICONTROL 密码]**，然后为以下凭据提供相应的值：

* 主机
* 端口
* 用户名
* 密码

在此步骤中，您还可以配置最大并发连接数、定义文件夹路径以及启用或禁用[!DNL SFTP]服务器的分块。 完成后，选择&#x200B;**[!UICONTROL 连接到源]**，等待一段时间以建立连接。

有关身份验证的详细信息，请阅读有关[收集 [!DNL SFTP]](../../../../connectors/cloud-storage/sftp.md#gather-required-credentials)所需凭据的指南。

![使用基本身份验证的SFTP源的新帐户屏幕](../../../../images/tutorials/create/sftp/password.png)

>[!TAB SSH公钥身份验证]

要使用基于SSH公钥的凭据，请选择&#x200B;**[!UICONTROL SSH公钥]**，然后为以下凭据提供相应的值：

* 主机
* 端口
* 用户名
* 私钥内容
* 密码短语

在此步骤中，您还可以配置最大并发连接数、定义文件夹路径以及启用或禁用[!DNL SFTP]服务器的分块。 完成后，选择&#x200B;**[!UICONTROL 连接到源]**，等待一段时间以建立连接。

有关身份验证的详细信息，请阅读有关[收集 [!DNL SFTP]](../../../../connectors/cloud-storage/sftp.md#gather-required-credentials)所需凭据的指南。

![使用SSH公钥的SFTP源的新帐户屏幕。](../../../../images/tutorials/create/sftp/ssh.png)

>[!ENDTABS]

## 后续步骤

通过学习本教程，您已建立与SFTP帐户的连接。 您现在可以继续阅读下一教程，并[配置数据流以将数据从云存储引入Experience Platform](../../dataflow/batch/cloud-storage.md)。
