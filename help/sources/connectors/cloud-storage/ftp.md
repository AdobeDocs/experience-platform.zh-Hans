---
keywords: Experience Platform；主页；热门主题；FTP;FTP;
solution: Experience Platform
title: FTP源连接器概述
description: 了解如何使用API或用户界面将FTP服务器连接到Adobe Experience Platform。
exl-id: a6186fad-8a7b-4103-80c7-a522ff69fe9e
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '457'
ht-degree: 0%

---

# （测试版）FTP连接器

>[!NOTE]
>
>FTP连接器处于测试阶段。 请参阅 [源概述](../../home.md#terms-and-conditions) 有关使用测试版标签的连接器的更多信息。

Adobe Experience Platform为AWS等云提供商提供本机连接， [!DNL Google Cloud Platform]和 [!DNL Azure]，允许您从这些系统中导入数据。

云存储源可以将您自己的数据引入 [!DNL Platform] 无需下载、设置格式或上传。 摄取的数据可以格式为XDM JSON、XDM Parquet或分隔。 流程的每个步骤都会集成到源工作流中。 [!DNL Platform] 允许您通过批量从FTP或SFTP服务器导入数据。

>[!IMPORTANT]
>
>使用FTP源连接器创建数据流时，强烈建议设置一次性摄取计划，因为FTP服务器中遇到的增量更新存在延迟问题。

## IP地址允许列表

在使用源连接器之前，必须将IP地址列表添加到允许列表。 无法将特定于区域的IP地址添加到允许列表，在使用源时可能会导致错误或性能不佳。 请参阅 [IP地址允许列表](../../ip-address-allow-list.md) 页面以了解更多信息。

## 文件和目录的命名限制

以下是在命名云存储文件或目录时必须考虑的限制列表。

- 目录和文件组件名称不能超过255个字符。
- 目录和文件名不能以正斜杠(`/`)。 如果提供，则会自动将其删除。
- 以下保留的URL字符必须正确转义： `! ' ( ) ; @ & = + $ , % # [ ]`
- 不允许使用以下字符： `" \ / : | < > * ?`.
- 不允许使用非法的URL路径字符。 代码点，如 `\uE000`，但在NTFS文件名中有效，是无效的Unicode字符。 此外，还不允许使用某些ASCII或Unicode字符，如控制字符（0x00到0x1F、\u0081等）。 有关HTTP/1.1中控制Unicode字符串的规则，请参阅 [RFC 2616，第2.2节：基本规则](https://www.ietf.org/rfc/rfc2616.txt) 和 [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- 不允许使用以下文件名：LPT1、LPT2、LPT3、LPT4、LPT5、LPT6、LPT7、LPT8、LPT9、COM1、COM2、COM3、COM4、COM5、COM6、COM7、COM8、COM9、PRN、NUL、CON、CLOK$、点(.)字符和两个点(.)字符。

## 将FTP连接到 [!DNL Platform]

以下文档提供了如何将FTP服务器连接到 [!DNL Platform] 使用API或用户界面：

### 使用API

- [使用流量服务API创建FTP基连接](../../tutorials/api/create/cloud-storage/ftp.md)
- [使用流量服务API探索云存储源的数据结构和内容](../../tutorials/api/explore/cloud-storage.md)
- [使用流服务API为云存储源创建数据流](../../tutorials/api/collect/cloud-storage.md)

### 使用UI

- [在UI中创建FTP源连接](../../tutorials/ui/create/cloud-storage/ftp.md)
- [在UI中为云存储连接创建数据流](../../tutorials/ui/dataflow/batch/cloud-storage.md)
