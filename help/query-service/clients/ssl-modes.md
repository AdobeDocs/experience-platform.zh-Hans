---
keywords: Experience Platform；主页；热门主题；查询服务；查询服务；连接；连接到查询服务；SSL;sslmode;
title: 查询服务SSL选项
description: 了解对与Adobe Experience Platform查询服务的第三方连接的SSL支持，以及如何使用验证完全SSL模式进行连接。
source-git-commit: 92dac8e75e1ddda860d255ce1b7d278041c89325
workflow-type: tm+mt
source-wordcount: '905'
ht-degree: 1%

---

# [!DNL Query Service] SSL选项

为了提高安全性，Adobe Experience Platform [!DNL Query Service] 为加密客户端/服务器通信的SSL连接提供本机支持。 本文档介绍用于与的第三方客户端连接的可用SSL选项 [!DNL Query Service] 以及如何使用 `verify-full` SSL参数值。

## 先决条件

本文档假定您已下载第三方桌面客户端应用程序以用于您的平台数据。 有关在与第三方客户端连接时如何整合SSL安全性的具体说明，请参阅其各自的连接指南文档。 要获取所有 [!DNL Query Service] 支持的客户端，请参阅 [客户端连接概述](./overview.md).

## 可用的SSL选项 {#available-ssl-options}

平台支持各种SSL选项，以满足您的数据安全需求，并平衡加密和密钥交换的处理开销。

不同 `sslmode` 参数值提供不同级别的保护。 通过使用SSL证书对移动的数据进行加密，有助于防止“中间人”(MITM)攻击、窃听和模拟。 下表列出了各种可用的SSL模式及其提供的保护级别。

>[!NOTE]
>
> SSL值 `disable` 由于符合必需的数据保护法规，Adobe Experience Platform不提供支持。

| sslmode | 窃听保护 | MITM保护 | 描述 |
|---|---|---|---|
| `allow` | 部分 | 否 | 安全性不是优先事项，速度和低处理开销更为重要。 此模式仅在服务器坚持加密的情况下才会选择加密。 |
| `prefer` | 部分 | 否 | 不需要加密，但如果服务器支持，通信将被加密。 |
| `require` | 是 | 否 | 所有通信都需要加密。 信任网络连接到正确的服务器。 不需要服务器SSL证书验证。 |
| `verify-ca` | 是 | 取决于CA策略 | 所有通信都需要加密。 共享数据之前需要进行服务器验证。 这要求您在PostgreSQL主目录中设置根证书。 [详情如下](#instructions) |
| `verify-full` | 是 | 是 | 所有通信都需要加密。 共享数据之前需要进行服务器验证。 这要求您在PostgreSQL主目录中设置根证书。 [详情如下](#instructions). |

>[!NOTE]
>
>两者之间的差异 `verify-ca` 和 `verify-full` 取决于根证书颁发机构(CA)的策略。 如果您已创建自己的本地CA，以使用 `verify-ca` 通常提供足够的保护。 如果使用公共CA， `verify-ca` 允许连接到其他人可能已向CA注册的服务器。 `verify-full` 应始终与公共根CA一起使用。

在建立与Platform数据库的第三方连接时，建议您使用 `sslmode=require` 至少要确保正在运行的数据的安全连接。 的 `verify-full` 建议在大多数安全敏感型环境中使用SSL模式。

## 为服务器验证设置根证书 {#root-certificate}

为确保安全连接，必须在客户端和服务器上都配置SSL使用情况，然后才能进行连接。 如果SSL仅在服务器上配置，则客户端可能会发送敏感信息（如密码），然后才能建立服务器要求高安全性。

默认情况下， [!DNL PostgreSQL] 不对服务器证书执行任何验证。 在发送任何敏感数据之前（作为SSL的一部分），验证服务器的身份并确保安全连接 `verify-full` 模式)，则必须在本地计算机(`root.crt`)和由服务器上的根证书签名的叶证书。

如果 `sslmode` 参数设置为 `verify-full`, libpq将通过检查存储在客户端上的根证书上的证书链来验证服务器是否可信。 然后验证主机名是否与服务器证书中存储的名称匹配。

要允许服务器证书验证，必须放置一个或多个根证书(`root.crt`) [!DNL PostgreSQL] 文件。 文件路径类似于 `~/.postgresql/root.crt`.

## 启用验证完全SSL模式以与第三方一起使用 [!DNL Query Service] 连接 {#instructions}

如果你需要比 `sslmode=require`，则可以按照突出显示的步骤将第三方客户端连接到 [!DNL Query Service] 使用 `verify-full` SSL模式。

>[!NOTE]
>
>可使用许多选项来获取SSL证书。 由于无管理证书的趋势日益增长，本指南中使用了DigiCert ，因为它们是高保证TLS/SSL、PKI、IoT和签名解决方案的可信全局提供商。

1. 导航到 [可用DigiCert根证书列表](https://www.digicert.com/kb/digicert-root-certificates.htm)
1. 搜索“[!DNL DigiCert Global Root CA]“ ”。
1. 选择 [!DNL **下载PEM**] 将文件下载到本地计算机。
   ![突出显示了“Download PEM（下载PEM）”的可用DigiCert根证书列表。](../images/clients/ssl-modes/digicert.png)
1. 将安全证书文件重命名为 `root.crt`.
1. 将文件复制到 [!DNL PostgreSQL] 文件夹。 必需的文件路径因操作系统而异。 如果文件夹不存在，请创建文件夹。
   - 如果您使用的是macOS，则路径为 `/Users/<username>/.postgresql`
   - 如果您使用的是Windows，则路径为 `%appdata%\postgresql`

>[!TIP]
>
>查找 `%appdata%` 文件位置，按⊞ **Win + R** 输入 `%appdata%` 中。

在 [!DNL DigiCert Global Root CA] CRT文件在 [!DNL PostgreSQL] 文件夹，您可以连接到 [!DNL Query Service] 使用 `sslmode=verify-full` 或 `sslmode=verify-ca` 选项。

## 后续步骤

通过阅读本文档，您可以更好地了解将第三方客户端连接到 [!DNL Query Service]，以及如何启用 `verify-full` 用于加密正在移动的数据的SSL选项。

如果您尚未执行此操作，请遵循 [将第三方客户端连接到 [!DNL Query Service]](./overview.md).
