---
title: Acxiom 数据摄取
description: 了解如何将 [!DNL Acxiom] 数据摄取到Real-time Customer Data Platform、丰富第一方配置文件以及改进受众并在营销渠道之间激活。
badge: Beta 版
exl-id: 3bbbe4e1-5e34-4104-bf39-2c452865b807
source-git-commit: 62bcaa532cdec68a2f4f62e5784c35b91b7d5743
workflow-type: tm+mt
source-wordcount: '473'
ht-degree: 2%

---

# [!DNL Acxiom Data Ingestion]

>[!NOTE]
>
>[!DNL Acxiom Prospecting Data Import]源为测试版。 有关使用测试版标记源的更多信息，请阅读[源概述](../../home.md#terms-and-conditions)。

使用[!DNL Acxiom Data Ingestion]源将[!DNL Acxiom]数据摄取到Real-time Customer Data Platform中并扩充第一方配置文件。 然后，您可以使用丰富[!DNL Acxiom]的第一方配置文件来改进受众并在营销渠道之间激活。

![acxiom-data-ingestion-workflow](../../images/tutorials/create/acxiom-data-enhancement-import/acxiom-data-ingestion.png)

请阅读下面的文档，了解有关如何设置[!DNL Acxiom Data Ingestion]源帐户的信息。

## 先决条件 {#prerequisites}

为了将您的[!DNL Acxiom Data Ingestion]帐户连接到Experience Platform，您必须提供以下身份验证凭据的值：

| 凭据 | 描述 |
| --- | --- |
| [!DNL Acxiom]身份验证密钥 | 身份验证密钥。 您可以从[!DNL Acxiom]团队中检索此值。 |
| [!DNL Amazon S3]访问密钥 | 存储段的访问密钥ID。 您可以从[!DNL Acxiom]团队中检索此值。 |
| [!DNL Amazon S3]密钥 | 存储桶的密钥ID。 您可以从[!DNL Acxiom]团队中检索此值。 |
| 存储桶名称 | 这是将共享文件的存储段。 您可以从[!DNL Acxiom]团队中检索此值。 |

## IP地址允许列表

在使用源连接器之前，必须将IP地址列表添加到允许列表中。 未能将特定于区域的IP地址添加到允许列表中，可能会导致使用源时出现错误或性能不佳。 有关详细信息，请参阅[IP地址允许列表](../../ip-address-allow-list.md)页。

### 配置Experience Platform权限

若要将您的[!DNL Acxiom Data Ingestion]帐户连接到Experience Platform，您必须同时为您的帐户启用&#x200B;**[!UICONTROL 查看源]**&#x200B;和&#x200B;**[!UICONTROL 管理源]**&#x200B;权限。 请联系您的产品管理员以获取必要的权限。 有关详细信息，请阅读[访问控制UI指南](../../../access-control/ui/overview.md)。

### 文件和目录的命名约束

在命名云存储文件或目录时，必须考虑以下列出的限制：

- 目录和文件组件名称不能超过255个字符。
- 目录和文件名不能以正斜杠(`/`)结尾。 如果提供，它将自动删除。
- 以下保留URL字符必须正确转义： `! ' ( ) ; @ & = + $ , % # [ ]`
- 不允许使用以下字符： `" \ / : | < > * ?`。
- 不允许使用非法的URL路径字符。 诸如`\uE000`之类的代码点虽然在NTFS文件名中有效，但不是有效的Unicode字符。 此外，不允许使用某些ASCII或Unicode字符，如控制字符（0x00到0x1F、\u0081等）。 有关HTTP/1.1中Unicode字符串的规则，请参阅[RFC 2616，第2.2节：基本规则](https://www.ietf.org/rfc/rfc2616.txt)和[RFC 3987](https://www.ietf.org/rfc/rfc3987.txt)。
- 不允许使用以下文件名：LPT1、LPT2、LPT3、LPT4、LPT5、LPT6、LPT7、LPT8、LPT9、COM1、COM2、COM3、COM4、COM5、COM6、COM7、COM8、COM9、PRN、AUX、NUL、CON、CLOCK$、点字符(.)和两个点字符(..)。

## 后续步骤

通过阅读本文档，您已完成将[!DNL Acxiom]帐户中的数据导入Experience Platform所需的先决条件设置。 现在，您可以继续阅读[使用用户界面](../../tutorials/ui/create/data-partners/acxiom-data-ingestion.md)连接 [!DNL Acxiom Data Ingestion] 以Experience Platform的指南。
