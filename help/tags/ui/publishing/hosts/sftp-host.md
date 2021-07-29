---
title: SFTP 主机
description: 了解如何在Adobe Experience Platform中配置标记，以将库内部版本交付到安全的自托管SFTP服务器。
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '527'
ht-degree: 39%

---

# SFTP主机

>[!NOTE]
>
>Adobe Experience Platform Launch已在Adobe Experience Platform中重新命名为一套数据收集技术。 因此，在产品文档中推出了一些术语更改。 有关术语更改的统一参考，请参阅以下[文档](../../../term-updates.md)。

如果您不希望 Adobe 管理您的托管文件库，那么还有另外一个选项，即让 Adobe Experience Platform 将内部版本交付到您托管的安全 SFTP 服务器。

Platform 会使用加密密钥连接到 SFTP 站点。可以通过以下几步来正确设置此操作：

1. 您必须在 SFTP 服务器上安装公钥/私钥对。您可以在服务器上生成这些密钥，也可以在其他位置生成这些密钥，然后在服务器上安装它们。 有关更多信息，请参阅有关[如何生成SSH密钥](https://help.github.com/cn/github/authenticating-to-github/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent#generating-a-new-ssh-key)的GitHub文档。
1. 私钥用于加密公共GPG密钥。 在SFTP主机创建过程中，您需要提供私钥。 有关对公共GPG密钥进行加密的说明，请参阅Reactor API文档中的[Encrypt values](https://developer.adobelaunch.com/api/guides/encrypting_values/)部分。 除非您知道自己需要特定的GPG密钥，否则请使用生产环境的GPG密钥。 最后，您可以从任何计算机加密私钥，您无需在服务器上安装 GPG 即可完成此步骤。
1. 您可能需要批准在公司防火墙中使用的IP地址，以便Platform能够访问您的SFTP服务器并连接到该服务器。 这些 IP 地址为：
   * `184.72.239.68`
   * `23.20.85.113`
   * `54.226.193.184`

>[!NOTE]
>
>标记内部版本的结构会随着时间的推移而发生更改。 它们在内部使用符号链接来保持向后兼容性，以便之前嵌入的代码可以继续与最新的内部版本结构配合使用。您的SFTP服务器必须支持使用符号链接，才能用作标记生成的有效目标。

有关更多详细信息，请参阅以下关于[如何设置SFTP服务器以交付内部版本](https://medium.com/launch-by-adobe/configuring-an-sftp-server-for-use-with-adobe-launch-bc626027e5a6)的媒体文章。

## 创建 SFTP 主机

1. 打开[!UICONTROL Hosts]选项卡。
1. 创建新主机。
1. 命名该主机。
1. 选择&#x200B;**[!UICONTROL SFTP]**&#x200B;作为主机类型。
1. 输入主机、路径、端口、用户名和加密私钥。

   端口必须是以下端口之一：

   * 21
   * 22
   * 80
   * 200-299
   * 443
   * 2000-2999
   * 4343
   * 8080
   * 8888

   >[!NOTE]
   >
   >作为最佳安全做法，Adobe 会限制用于传出流量的端口数量。通常，允许所选端口通过公司防火墙，另外，这些端口还包含一定范围的灵活性。

1. 选择 **[!UICONTROL Save]**。

选择&#x200B;**[!UICONTROL Save]**&#x200B;后，将测试将文件传送到SFTP服务器的连接和功能。 平台会创建一个文件夹，在该文件夹中写入文件，检查以确保文件存在，然后自行清理。 如果SFTP服务器上的用户帐户（附加到您提供给平台的安全证书的用户帐户）没有执行此操作所需的权限，则主机将进入“失败”状态。
