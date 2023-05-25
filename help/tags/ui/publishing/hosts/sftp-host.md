---
title: SFTP 主机
description: 了解如何在Adobe Experience Platform中配置标记以将库内部版本交付到安全的自托管SFTP服务器。
exl-id: 3c1dc43b-291c-4df4-94f7-a03b25dbb44c
source-git-commit: 8ded2aed32dffa4f0923fedac7baf798e68a9ec9
workflow-type: tm+mt
source-wordcount: '820'
ht-degree: 19%

---

# SFTP主机

>[!NOTE]
>
>Adobe Experience Platform Launch已更名为Adobe Experience Platform中的一套数据收集技术。 因此，产品文档中的术语有一些改动。有关术语更改的综合参考，请参阅以下[文档](../../../term-updates.md)。

通过Adobe Experience Platform，您可以将标记库内部版本交付到您托管的安全SFTP服务器，从而更好地控制如何存储和管理内部版本。 本指南介绍如何在Experience PlatformUI或数据收集UI中为标记属性设置SFTP主机。

>[!NOTE]
>
>您还可以选择改用由Adobe管理的主机。 请参阅指南，网址为 [Adobe管理的主机](./managed-by-adobe-host.md) 了解更多信息。
>
>有关自托管库的好处和限制的信息，请参阅 [自托管指南](./self-hosting-libraries.md).

## 为您的服务器设置访问密钥 {#access-key}

Platform 会使用加密密钥连接到 SFTP 站点。可以通过以下几步来正确设置此操作：

### 创建公钥/私钥对

您必须在 SFTP 服务器上安装公钥/私钥对。您可以在服务器上生成这些密钥，也可以在其他位置生成这些密钥并将其安装在服务器上。 请参阅GitHub文档，了解 [如何生成SSH密钥](https://help.github.com/cn/github/authenticating-to-github/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent#generating-a-new-ssh-key) 了解更多信息。

### 加密您的密钥

私钥用于加密公钥。 在SFTP主机创建过程中，您需要提供私钥。 请参阅以下部分： [加密值](../../../api/guides/encrypting-values.md) 有关加密公钥的说明，请参见Reactor API指南。 使用生产环境的GPG密钥，除非您知道自己需要特定的GPG密钥。 最后，您可以从任何计算机加密私钥，您无需在服务器上安装 GPG 即可完成此步骤。

### 允许列表平台IP地址

您可能需要批准要在公司防火墙内使用的一组IP地址，以允许平台访问您的SFTP服务器并与之建立连接。 这些IP地址包括：

* `184.72.239.68`
* `23.20.85.113`
* `54.226.193.184`

>[!NOTE]
>
>标记构建的结构会随着时间的推移而不断变化。 它们在内部使用符号链接来保持向后兼容性，以便之前嵌入的代码可以继续与最新的内部版本结构配合使用。您的SFTP服务器必须支持使用符号链接，才能用作标记构建的有效目标。

有关更多详细信息，请参阅以下媒体文章： [如何设置SFTP服务器以交付内部版本](https://medium.com/launch-by-adobe/configuring-an-sftp-server-for-use-with-adobe-launch-bc626027e5a6).

## 创建 SFTP 主机 {#create}

选择 **[!UICONTROL 主机]** 在左侧导航中，其后是 **[!UICONTROL 添加主机]**.

![该图像显示了在UI中选择的“添加主机”按钮](../../../images/ui/publishing/sftp-hosts/add-host-button.png)

此时将显示主机创建对话框。 提供主机的名称，并在 **[!UICONTROL 类型]**，选择 **[!UICONTROL SFTP]**.

![显示正在选择的SFTP托管选项的图像](../../../images/ui/publishing/sftp-hosts/select-sftp.png)

### 配置SFTP主机 {#configure}

该对话框随即展开，以包含SFTP主机的其他配置选项。 下文对此予以说明。

![显示SFTP主机连接所需详细信息的图像](../../../images/ui/publishing/sftp-hosts/host-details.png)

| 配置字段 | 描述 |
| --- | --- |
| [!UICONTROL 不使用符号链接] | 默认情况下，所有SFTP主机都使用符号链接（符号链接）来引用库 [内部版本](../builds.md) 保存到服务器的文件。 但是，并非所有服务器都支持使用符号链接。 如果选择此选项，主机将使用复制操作直接更新生成资产，而不是使用符号链接。 |
| [!UICONTROL SFTP服务器URL] | 服务器的URL基本路径。 |
| [!UICONTROL 路径] | 附加到此主机的基本服务器URL的路径。 |
| [!UICONTROL 端口] | 端口必须是以下端口之一：<ul><li>`21`</li><li>`22`</li><li>`80`</li><li>`200-299`</li><li>`443`</li><li>`2000-2999`</li><li>`4343`</li><li>`8080`</li><li>`8888`</li></ul>作为最佳安全做法，Adobe 会限制用于传出流量的端口数量。通常允许所选端口通过公司防火墙，并且这些端口包含一些灵活性范围。 |
| [!UICONTROL 用户名] | 访问服务器时使用的用户名。 |
| [!UICONTROL 加密的私钥] | 您在 [上一步](#access-key). |

选择 **[!UICONTROL 保存]** 创建具有所选配置的主机。

![显示正在保存的SFTP主机的图像](../../../images/ui/publishing/sftp-hosts/save-host.png)

当您选择时 **[!UICONTROL 保存]**，则会测试将文件交付到SFTP服务器的连接和能力。 Platform会创建一个文件夹，在该文件夹中写入文件，检查以确保该文件存在，然后自行清理。 如果SFTP服务器上的用户帐户（连接到您提供给Platform的安全证书的用户帐户）没有执行此操作所需的权限，则主机将进入“失败”状态。

## 后续步骤

本指南介绍了如何设置要在标记中使用的自托管SFTP服务器。 建立主机后，您可以将其与一个或多个关联 [环境](../environments.md) 用于发布标记库。 有关在Web或移动资产上激活标记功能的高级过程的更多信息，请参阅 [发布概述](../overview.md).
