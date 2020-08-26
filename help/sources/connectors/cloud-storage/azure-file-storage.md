---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Azure文件存储连接器
topic: overview
translation-type: tm+mt
source-git-commit: 690ddbd92f0a2e4e06b988e761dabff399cd2367
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 0%

---


# （测试版）Azure文件存储连接器

>[!NOTE]
>
>Azure文件存储连接器处于测试状态。 有关使用 [测试版标记](../../home.md#terms-and-conditions) 的连接器的更多信息，请参阅源概述。

Adobe Experience Platform为AWS等云提供商提 [!DNL Google Cloud Platform]供本 [!DNL Azure]机连接，允许您从这些系统获取数据。

云存储源无需下载、格式化 [!DNL Platform] 或上传即可将您自己的数据导入其中。 摄取的数据可格式化为XDM JSON、XDM镶木地板或分隔。 流程的每个步骤都集成到源工作流中。 [!DNL Platform] 允许您从批中导入 [!DNL Azure File Storage] 数据。

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

以下文档提供了如何使用API [!DNL Azure File Storage] 或 [!DNL Platform] 用户界面连接的信息：

## 连接 [!DNL Azure File Storage] 到 [!DNL Platform] 使用API

- [使用Flow Service API创建Azure文件存储连接器](../../tutorials/api/create/cloud-storage/azure-file-storage.md)
- [使用Flow Service API浏览云存储系统](../../tutorials/api/explore/cloud-storage.md)
- [使用流服务API收集云存储数据](../../tutorials/api/collect/cloud-storage.md)

## 连接 [!DNL Azure File Storage] 到 [!DNL Platform] 使用UI

- [在UI中创建Azure文件存储源连接器](../../tutorials/ui/create/cloud-storage/azure-file-storage.md)
- [在UI中为云存储连接器配置数据流](../../tutorials/ui/dataflow/batch/cloud-storage.md)