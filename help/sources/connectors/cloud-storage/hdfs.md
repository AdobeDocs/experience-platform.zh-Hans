---
keywords: Experience Platform;home;popular topics;HDFS;hdfs;Apache HDFS;apache hdfs
solution: Experience Platform
title: HDFS连接器
topic: overview
description: 以下文档提供了如何使用API或用户界面将Apache HDFS连接到平台的信息。
translation-type: tm+mt
source-git-commit: d42351c194bb5a11f3175535de83fbd3b6ac58d2
workflow-type: tm+mt
source-wordcount: '366'
ht-degree: 0%

---


# （测试版） [!DNL Apache] HDFS连接器

>[!NOTE]
>
>Apache HDFS连接器处于测试状态。 有关使用 [测试版标记](../../home.md#terms-and-conditions) 的连接器的更多信息，请参阅源概述。

Adobe Experience Platform为AWS等云提供商提 [!DNL Google Cloud Platform]供本 [!DNL Azure]机连接，允许您从这些系统获取数据。 收录的数据可以格式化为JSON、镶木地板或分隔。 云存储提供商支持包 [!DNL Apache] 括HDFS。

## IP地址允许列表

在使用源连接器之前，必须将以下IP地址添加到允许列表。 如果无法向允许列表添加特定于区域的IP地址，则在使用源时可能会导致错误或性能不佳。

### 美国东部地区

- `20.41.2.0/23`
- `20.41.4.0/26`
- `20.44.17.80/28`
- `20.49.102.16/29`
- `40.70.148.160/28`
- `52.167.107.224/28`

### 西欧地区

- `13.69.67.192/28`
- `13.69.107.112/28`
- `13.69.112.128/28`
- `40.74.24.192/26`
- `40.74.26.0/23`
- `40.113.176.232/29`
- `52.236.187.112/28`

### 澳大利亚东部

- `13.70.74.144/28`
- `20.37.193.0/25`
- `20.37.193.128/26`
- `20.37.198.224/29`
- `40.79.163.80/28`
- `40.79.171.160/28`

## 文件和目录的命名限制

以下是命名云存储文件或目录时必须考虑的约束列表。

- 目录和文件组件名称不能超过255个字符。
- 目录和文件名不能以正斜杠(`/`)结尾。 如果提供，则会自动删除它。
- 以下保留的URL字符必须正确转义： `! * ' ( ) ; : @ & = + $ , / ? % # [ ]`
- 不允许使用以下字符： `" \ / : | < > * ?`.
- 不允许使用非法的URL路径字符。 像这样的代 `\uE000`码点在NTFS文件名中有效，但不是有效的Unicode字符。 此外，某些ASCII或Unicode字符，如控制字符（0x00到0x1F、\u0081等）也不允许使用。 有关HTTP/1.1中管理Unicode字符串的规则，请 [参阅RFC 2616，第2.2节：基本规则](https://www.ietf.org/rfc/rfc2616.txt) 和 [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt)。
- 不允许使用以下文件名：LPT1、LPT2、LPT3、LPT4、LPT5、LPT6、LPT7、LPT8、LPT9、COM1、COM2、COM3、COM4、COM5、COM6、COM7、COM8、COM9prn, AUX, NUL, CON, CLOCK$，点字符(.)和两个点字符(..)。

## 将 [!DNL Apache] HDFS连接到 [!DNL Platform]

以下文档提供如何将HDFS连 [!DNL Apache] 接到 [!DNL Platform] 使用API或用户界面的信息：

### 使用API

- [使用Flow Service API创建HDFS连接器](../../tutorials/api/create/cloud-storage/hdfs.md)
- [使用Flow Service API浏览云存储系统](../../tutorials/api/explore/cloud-storage.md)
- [使用流服务API收集云存储数据](../../tutorials/api/collect/cloud-storage.md)

### 使用UI

- [在UI中创建Apache HDFS源连接器](../../tutorials/ui/create/cloud-storage/hdfs.md)
- [在UI中为云存储连接器配置数据流](../../tutorials/ui/dataflow/batch/cloud-storage.md)