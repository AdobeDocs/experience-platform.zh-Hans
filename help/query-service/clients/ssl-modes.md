---
keywords: Experience Platform；主页；热门主题；查询服务；查询服务；连接；连接到查询服务；SSL；ssl；sslmode；
title: 查询服务SSL选项
description: 了解对Adobe Experience Platform查询服务的第三方连接的SSL支持，以及如何使用验证完全SSL模式进行连接。
exl-id: 41b0a71f-165e-49a2-8a7d-d809f5f683ae
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1011'
ht-degree: 1%

---

# [!DNL Query Service] SSL选项

为了提高安全性，Adobe Experience Platform [!DNL Query Service]为SSL连接提供本机支持，以加密客户端/服务器通信。 本文档介绍了用于连接到[!DNL Query Service]的第三方客户端的可用SSL选项，以及如何使用`verify-full` SSL参数值连接。

## 先决条件

本文档假设您已经下载了第三方桌面客户端应用程序以用于Experience Platform数据。 有关在与第三方客户端连接时如何合并SSL安全性的具体说明，请参阅各自的连接指南文档。 有关所有[!DNL Query Service]支持的客户端的列表，请参阅[客户端连接概述](./overview.md)。

## 可用的SSL选项 {#available-ssl-options}

Experience Platform支持各种SSL选项，以满足您的数据安全需求并平衡加密和密钥交换的处理开销。

不同的`sslmode`参数值提供了不同的保护级别。 通过使用SSL证书对您的数据进行动态加密，这有助于防止“中间人”(MITM)攻击、窃听和模拟。 下表提供了可用不同SSL模式的划分以及它们提供的保护级别。

>[!NOTE]
>
> 由于符合数据保护要求，Adobe Experience Platform不支持SSL值`disable`。

| sslmode | 窃听保护 | MITM保护 | 描述 |
|---|---|---|---|
| `allow` | 是 | 否 | 所有通信都需要加密。 该网络被信任连接到正确的服务器。 |
| `prefer` | 是 | 否 | 所有通信都需要加密。 该网络被信任连接到正确的服务器。 |
| `require` | 是 | 否 | 所有通信都需要加密。 该网络被信任连接到正确的服务器。 不需要验证服务器SSL证书。 |
| `verify-ca` | 是 | 依赖于CA策略 | 所有通信都需要加密。 在共享数据之前，需要服务器验证。 这要求您在[!DNL PostgreSQL]主目录中设置根证书。 [详情如下](#instructions) |
| `verify-full` | 是 | 是 | 所有通信都需要加密。 在共享数据之前，需要服务器验证。 这要求您在[!DNL PostgreSQL]主目录中设置根证书。 [详情如下](#instructions)。 |

>[!NOTE]
>
>`verify-ca`和`verify-full`之间的差异取决于根证书颁发机构(CA)的策略。 如果您已经创建自己的本地CA来为您的应用程序颁发私有证书，则使用`verify-ca`通常会提供足够的保护。 如果使用公共CA，`verify-ca`允许连接到其他人可能已向CA注册的服务器。 `verify-full`应始终与公共根CA一起使用。

在建立与Experience Platform数据库的第三方连接时，建议您至少使用`sslmode=require`，以确保移动数据的安全连接。 建议将`verify-full` SSL模式用于大多数安全敏感型环境。

## 设置根证书以进行服务器验证 {#root-certificate}

>[!IMPORTANT]
>
>查询服务Interactive Postgres API的生产环境上的TLS/SSL证书已于2024年1月24日星期三更新。<br>尽管这是年度要求，但此时链中的根证书也已更改，因为Adobe的TLS/SSL证书提供商已更新其证书层次结构。 如果某些Postgres客户端的证书颁发机构列表缺少根证书，这可能会影响这些客户端。 例如，PSQL CLI客户端可能需要将根证书添加到显式文件`~/postgresql/root.crt`中，否则可能会导致错误。 例如：`psql: error: SSL error: certificate verify failed`。有关此问题的更多信息，请参阅[官方的PostgreSQL文档](https://www.postgresql.org/docs/current/libpq-ssl.html#LIBQ-SSL-CERTIFICATES)。<br>可以从[https://cacerts.digicert.com/DigiCertGlobalRootG2.crt.pem](https://cacerts.digicert.com/DigiCertGlobalRootG2.crt.pem)下载要添加的根证书。

为确保安全连接，在连接之前，必须在客户端和服务器上配置SSL用法。 如果只在服务器上配置了SSL，则客户端可能会在确定服务器要求高安全性之前发送敏感信息，如密码。

默认情况下，[!DNL PostgreSQL]不对服务器证书执行任何验证。 若要验证服务器的身份并确保在发送任何敏感数据之前建立安全连接（作为SSL `verify-full`模式的一部分），您必须在本地计算机(`root.crt`)上放置根（自签名）证书，并在服务器上放置由根证书签名的叶证书。

如果`sslmode`参数设置为`verify-full`，则libpq将通过检查证书链以检查客户端上存储的根证书来验证服务器是否可信。 然后，它验证主机名是否与服务器证书中存储的名称匹配。

要允许服务器证书验证，您必须在主目录的[!DNL PostgreSQL]文件中放置一个或多个根证书(`root.crt`)。 文件路径将类似于`~/.postgresql/root.crt`。

## 启用验证完全SSL模式以用于第三方[!DNL Query Service]连接 {#instructions}

如果您需要比`sslmode=require`更严格的安全控制，则可以按照突出显示的步骤使用`verify-full` SSL模式将第三方客户端连接到[!DNL Query Service]。

>[!NOTE]
>
>要获取SSL证书，有许多选项可用。 由于无管理证书呈增长趋势，本指南使用DigiCert，因为它们是高保证TLS/SSL、PKI、物联网和签名解决方案的可信全球提供商。

1. 导航到[可用DigiCert根证书列表](https://www.digicert.com/kb/digicert-root-certificates.htm)
1. 从可用证书列表中搜索“[!DNL DigiCert Global Root G2]”。
1. 选择&#x200B;[!DNL **下载PEM**]以将文件下载到本地计算机。
   ![已突出显示下载PEM的可用DigiCert根证书列表。](../images/clients/ssl-modes/digicert.png)
1. 将安全证书文件重命名为`root.crt`。
1. 将文件复制到[!DNL PostgreSQL]文件夹。 必需的文件路径因您的操作系统而异。 如果该文件夹尚不存在，请创建该文件夹。
   - 如果您使用的是macOS，则路径为`/Users/<username>/.postgresql`
   - 如果您使用的是Windows，则路径为`%appdata%\postgresql`

>[!TIP]
>
>要在Windows操作系统中查找`%appdata%`文件位置，请按⊞ **Win + R**&#x200B;并在搜索字段中输入`%appdata%`。

在您的[!DNL PostgreSQL]文件夹中提供[!DNL DigiCert Global Root G2] CRT文件后，您可以使用`sslmode=verify-full`或`sslmode=verify-ca`选项连接到[!DNL Query Service]。

## 后续步骤

通过阅读本文档，您可以更好地了解用于将第三方客户端连接到[!DNL Query Service]的可用SSL选项，以及如何启用`verify-full` SSL选项以动态加密您的数据。

如果您尚未这样做，请按照[将第三方客户端连接到 [!DNL Query Service]](./overview.md)上的指南进行操作。
