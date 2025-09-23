---
title: Acxiom 潜在客户数据导入
description: 了解如何使用 UI 将 Acxiom 潜在客户数据连接到 Adobe Experience Platform 和 Adobe Real-Time Customer Data Platform。
exl-id: 6df674d9-c14b-42ea-a287-5377484e567d
source-git-commit: e402a58f51de49b26f9d279cebf551ec11e4698f
workflow-type: tm+mt
source-wordcount: '544'
ht-degree: 5%

---

# [!DNL Acxiom Prospecting Data Import]

Adobe Experience Platform支持从数据合作伙伴应用程序中摄取数据。 对数据和身份合作伙伴的支持包括[!DNL Acxiom Prospecting Data Import]。

[!DNL Acxiom]的Adobe Real-Time Customer Data Platform潜在客户数据导入是一个尽可能提供最多生产力的潜在客户受众的过程。 [!DNL Acxiom]通过安全导出获取Real-Time CDP第一方数据，并通过屡获殊荣的卫生和身份解析系统运行该数据。 生成可用作禁止列表的数据文件。 然后，此数据文件与[!DNL Acxiom Global]数据库匹配，这样可以自定义目标客户列表以进行导入。

您可以使用[!DNL Acxiom]源检索和映射[!DNL Acxiom]目标客户服务的响应，并将[!DNL Amazon S3]用作放置点。

![acxiom-prospecting-workflow](../../images/tutorials/create/acxiom-prospect-suppression-data-sourcing/acxiom-prospecting.png)

请阅读下面的文档，了解有关如何设置[!DNL Acxiom Prospecting Data Import]源帐户的信息。

## 先决条件

要在Experience Platform上访问存储段，您需要为以下凭据提供有效值：

| 凭据 | 描述 |
| --- | --- |
| [!DNL Acxiom]身份验证密钥 | 身份验证密钥。 您可以从[!DNL Acxiom]团队中检索此值。 |
| [!DNL Amazon S3]访问密钥 | 存储段的访问密钥ID。 您可以从[!DNL Acxiom]团队中检索此值。 |
| [!DNL Amazon S3]密钥 | 存储桶的密钥ID。 您可以从[!DNL Acxiom]团队中检索此值。 |
| 存储桶名称 | 这是将共享文件的存储段。 您可以从[!DNL Acxiom]团队中检索此值。 |

## IP地址允许列表

在使用源连接器之前，必须将您所在地区所需的IP地址添加到允许列表。 如果不添加这些IP地址，源连接器可能无法正确工作或可能产生错误。 列入允许列表有关详细说明和允许的IP地址列表，请阅读[IP地址](../../ip-address-allow-list.md)页。

### 在Experience Platform上配置权限

若要将您的&#x200B;**[!UICONTROL 帐户连接到Experience Platform，您必须同时为您的帐户启用]**&#x200B;查看源&#x200B;**[!UICONTROL 和]**&#x200B;管理源[!DNL Acxiom Prospecting Data Import]权限。 请联系您的产品管理员以获取必要的权限。 有关详细信息，请阅读[访问控制UI指南](../../../access-control/abac/ui/permissions.md)。

## 文件和目录的命名约束

在命名云存储文件或目录时，必须考虑以下列出的限制：

- 目录和文件组件名称不能超过255个字符。
- 目录和文件名不能以正斜杠(`/`)结尾。 如果提供，它将自动删除。
- 以下保留URL字符必须正确转义： `! ' ( ) ; @ & = + $ , % # [ ]`
- 不允许使用以下字符： `" \ / : | < > * ?`。
- 不允许使用非法的URL路径字符。 诸如`\uE000`之类的代码点虽然在NTFS文件名中有效，但不是有效的Unicode字符。 此外，不允许使用某些ASCII或Unicode字符，如控制字符（0x00到0x1F、\u0081等）。 有关HTTP/1.1中Unicode字符串的规则，请参阅[RFC 2616，第2.2节：基本规则](https://www.ietf.org/rfc/rfc2616.txt)和[RFC 3987](https://www.ietf.org/rfc/rfc3987.txt)。
- 不允许使用以下文件名：LPT1、LPT2、LPT3、LPT4、LPT5、LPT6、LPT7、LPT8、LPT9、COM1、COM2、COM3、COM4、COM5、COM6、COM7、COM8、COM9、PRN、AUX、NUL、CON、CLOCK$、点字符(.)和两个点字符(..)。

## 后续步骤

通过阅读本文档，您已完成将[!DNL Acxiom]帐户中的数据导入Experience Platform所需的先决条件设置。 现在，您可以使用用户界面[在 [!DNL Acxiom Prospecting Data Import] 连接](../../tutorials/ui/create/data-partners/acxiom-prospecting-data-import.md)到Experience Platform时继续阅读指南。
