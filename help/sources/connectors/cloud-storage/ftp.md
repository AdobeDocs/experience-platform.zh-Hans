---
keywords: Experience Platform;home;popular topics;FTP;ftp;
solution: Experience Platform
title: FTP连接器
topic: overview
description: 以下文档提供了如何使用API或用户界面将FTP服务器连接到平台的信息。
translation-type: tm+mt
source-git-commit: 5e5ac80e0c79b3cc0354b469edc036523e29b45d
workflow-type: tm+mt
source-wordcount: '440'
ht-degree: 0%

---


# （测试版）FTP连接器

>[!NOTE]
>
>FTP连接器处于测试状态。 有关使用 [测试版标记](../../home.md#terms-and-conditions) 的连接器的更多信息，请参阅源概述。

Adobe Experience Platform为AWS等云提供商提 [!DNL Google Cloud Platform]供本 [!DNL Azure]机连接，允许您从这些系统获取数据。

云存储源无需下载、格式化 [!DNL Platform] 或上传即可将您自己的数据导入其中。 摄取的数据可格式化为XDM JSON、XDM镶木地板或分隔。 流程的每个步骤都集成到源工作流中。 [!DNL Platform] 允许您通过批量从FTP或SFTP服务器导入数据。

>[!IMPORTANT]
>
>当使用FTP源连接器创建数据流时，强烈建议设置一次性摄取计划，因为FTP服务器中遇到的增量更新存在延迟问题。

## IP地址允许列表

在使用源连接器之前，必须向允许列表添加IP地址列表。 如果无法向允许列表添加特定于区域的IP地址，则在使用源时可能会导致错误或性能不佳。 有关详细 [信息，请参阅](../../ip-address-allow-list.md) “IP地址允许列表”页。

## 文件和目录的命名限制

以下是命名云存储文件或目录时必须考虑的约束列表。

- 目录和文件组件名称不能超过255个字符。
- 目录和文件名不能以正斜杠(`/`)结尾。 如果提供，则会自动删除它。
- 以下保留的URL字符必须正确转义： `! * ' ( ) ; : @ & = + $ , / ? % # [ ]`
- 不允许使用以下字符： `" \ / : | < > * ?`.
- 不允许使用非法的URL路径字符。 像这样的代 `\uE000`码点在NTFS文件名中有效，但不是有效的Unicode字符。 此外，某些ASCII或Unicode字符，如控制字符（0x00到0x1F、\u0081等）也不允许使用。 有关HTTP/1.1中管理Unicode字符串的规则，请 [参阅RFC 2616，第2.2节：基本规则](https://www.ietf.org/rfc/rfc2616.txt) 和 [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt)。
- 不允许使用以下文件名：LPT1、LPT2、LPT3、LPT4、LPT5、LPT6、LPT7、LPT8、LPT9、COM1、COM2、COM3、COM4、COM5、COM6、COM7、COM8、COM9prn, AUX, NUL, CON, CLOCK$，点字符(.)和两个点字符(..)。

## 将FTP连接到 [!DNL Platform]

以下文档提供了如何使用API或用户界 [!DNL Platform] 面将FTP服务器连接的信息：

### 使用API

- [使用流服务API创建FTP连接器](../../tutorials/api/create/cloud-storage/ftp.md)
- [使用Flow Service API浏览云存储系统](../../tutorials/api/explore/cloud-storage.md)
- [使用流服务API收集云存储数据](../../tutorials/api/collect/cloud-storage.md)

### 使用UI

- [在UI中创建FTP源连接器](../../tutorials/ui/create/cloud-storage/ftp.md)
- [在UI中为云存储连接器配置数据流](../../tutorials/ui/dataflow/batch/cloud-storage.md)