---
keywords: Experience Platform;home;popular topics;Azure Data Lake Storage Gen2;ADLS-Gen2;adls gen2;ADLS Gen2
solution: Experience Platform
title: Azure Data Lake存储Gen2连接器
topic: overview
description: 以下文档提供了如何使用API或用户界面将Azure Data Lake存储Gen2连接到平台的信息。
translation-type: tm+mt
source-git-commit: 6934bfeee84f542558894bbd4ba5759891cd17f3
workflow-type: tm+mt
source-wordcount: '224'
ht-degree: 0%

---


# Azure Data Lake存储Gen2连接器

Adobe Experience Platform为AWS等云提供商提 [!DNL Google Cloud Platform]供本 [!DNL Azure]机连接，允许您从这些系统获取数据。

云存储源无需下载、格式化 [!DNL Platform] 或上传即可将您自己的数据导入其中。 摄取的数据可格式化为XDM JSON、XDM镶木地板或分隔。 流程的每个步骤都集成到源工作流中。 [!DNL Platform] 允许您从(ADLS- [!DNL Azure Data Lake Storage Gen2] Gen2)到批量导入数据。

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

## 连接 [!DNL Azure Data Lake Storage Gen2] 到 [!DNL Platform]

以下文档提供了如何使用API [!DNL Azure Data Lake Storage Gen2] 或 [!DNL Platform] 用户界面连接的信息：

### 使用API

- [使用Flow Service API创建ADLS-Gen2连接器](../../tutorials/api/create/cloud-storage/adls-gen2.md)
- [使用Flow Service API浏览云存储系统](../../tutorials/api/explore/cloud-storage.md)
- [使用流服务API收集云存储数据](../../tutorials/api/collect/cloud-storage.md)

## 使用UI

- [在UI中创建ADLS-Gen2源连接器](../../tutorials/ui/create/cloud-storage/adls-gen2.md)
- [在UI中为云存储连接器配置数据流](../../tutorials/ui/dataflow/batch/cloud-storage.md)