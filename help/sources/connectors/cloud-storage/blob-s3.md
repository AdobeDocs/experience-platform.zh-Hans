---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Azure Blob和Amazon S3连接器
topic: overview
translation-type: tm+mt
source-git-commit: 340f5d0611e9e9eb4676018ee10c8a8aa08dbb2d
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 0%

---


# Azure Blob和Amazon S3连接器

Adobe Experience Platform为AWS、和等云提供商提供 [!DNL Google Cloud Platform]本机连 [!DNL Azure]接。 您可以将数据从这些系统导入 [!DNL Platform]。

云存储源无需下载、格式化 [!DNL Platform] 或上传即可将您自己的数据导入其中。 摄取的数据可格式化为XDM JSON、XDM镶木地板或分隔。 流程的每个步骤都集成到源工作流中。 [!DNL Platform] 允许您从S3和 [!DNL Azure Blob] S3批量导入数据。

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

以下文档提供了如何使用API或用户界面将Azure Blob和S3连接到平台的信息：

## 连接 [!DNL Azure Blob] 和S3以使用 [!DNL Platform] API

- [使用流服务API创建Azure Blob连接器](../../tutorials/api/create/cloud-storage/blob.md)
- [使用Flow Service API创建S3连接器](../../tutorials/api/create/cloud-storage/s3.md)
- [使用Flow Service API浏览云存储系统](../../tutorials/api/explore/cloud-storage.md)
- [使用流服务API收集云存储数据](../../tutorials/api/collect/cloud-storage.md)

## 连接 [!DNL Blob] 和S3以使 [!DNL Platform] 用UI

- [在UI中创建Azure Blob或Amazon S3源连接器](../../tutorials/ui/create/cloud-storage/blob-s3.md)
- [在UI中为云存储连接器配置数据流](../../tutorials/ui/dataflow/batch/cloud-storage.md)