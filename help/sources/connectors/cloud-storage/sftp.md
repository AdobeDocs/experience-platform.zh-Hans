---
keywords: Experience Platform；主页；热门主题；SFTP;sftp
solution: Experience Platform
title: SFTP连接器
topic: overview
description: 以下文档提供了如何使用API或用户界面将SFTP服务器连接到平台的信息。
translation-type: tm+mt
source-git-commit: 2940f030aa21d70cceeedc7806a148695f68739e
workflow-type: tm+mt
source-wordcount: '469'
ht-degree: 0%

---


# （测试版）SFTP连接器

>[!NOTE]
>
>SFTP连接器处于测试状态。 有关使用测试版标签的连接器的详细信息，请参见[源概述](../../home.md#terms-and-conditions)。

Adobe Experience Platform为AWS、[!DNL Google Cloud Platform]和[!DNL Azure]等云提供商提供本机连接，让您能够从这些系统中获取数据。

云存储源可以将您自己的数据导入[!DNL Platform]，而无需下载、格式化或上传。 摄取的数据可格式化为XDM JSON、XDM Perface或分隔。 流程的每个步骤都集成到源工作流中。 [!DNL Platform] 允许您通过批量从FTP或SFTP服务器导入数据。

## IP地址允许列表

在使用源连接器之前，必须向允许列表添加IP地址列表。 如果无法向允许列表添加特定于区域的IP地址，则在使用源时可能会导致错误或性能不佳。 有关详细信息，请参阅[ IP地址允许列表](../../ip-address-allow-list.md)页。

## 文件和目录的命名限制

以下是命名云存储文件或目录时必须考虑的约束列表。

- 目录和文件组件名称不能超过255个字符。
- 目录和文件名不能以正斜杠(`/`)结尾。 如果提供，则会自动删除它。
- 以下保留的URL字符必须正确转义：`! * ' ( ) ; : @ & = + $ , / ? % # [ ]`
- 不允许使用以下字符：`" \ / : | < > * ?`。
- 不允许使用非法的URL路径字符。 像`\uE000`这样的代码点在NTFS文件名中有效，但不是有效的Unicode字符。 此外，某些ASCII或Unicode字符，如控制字符（0x00到0x1F、\u0081等）也不允许使用。 有关HTTP/1.1中管理Unicode字符串的规则，请参阅[RFC 2616，第2.2节：基本规则](https://www.ietf.org/rfc/rfc2616.txt)和[RFC 3987](https://www.ietf.org/rfc/rfc3987.txt)。
- 不允许使用以下文件名：LPT1、LPT2、LPT3、LPT4、LPT5、LPT6、LPT7、LPT8、LPT9、COM1、COM2、COM3、COM4、COM5、COM6、COM7、COM8、COM9prn, AUX, NUL, CON, CLOCK$，点字符(.)和两个点字符(..)。

## 将SFTP连接到[!DNL Platform]

>[!IMPORTANT]
>
>在连接之前，用户必须在SFTP服务器配置中禁用键盘交互身份验证。 禁用此设置将允许手动输入密码，而不是通过服务或项目输入。 有关键盘交互式身份验证的详细信息，请参阅[组件Pro文档](https://doc.componentpro.com/ComponentPro-Sftp/authenticating-with-a-keyboard-interactive-authentication)。

以下文档提供了如何使用API或用户界面将SFTP服务器连接到[!DNL Platform]的信息：

### 使用API

- [使用流服务API创建SFTP连接器](../../tutorials/api/create/cloud-storage/sftp.md)
- [使用Flow Service API浏览云存储系统](../../tutorials/api/explore/cloud-storage.md)
- [使用流服务API收集云存储数据](../../tutorials/api/collect/cloud-storage.md)

### 使用UI

- [在UI中创建SFTP源连接器](../../tutorials/ui/create/cloud-storage/sftp.md)
- [在UI中为云存储连接器配置数据流](../../tutorials/ui/dataflow/batch/cloud-storage.md)