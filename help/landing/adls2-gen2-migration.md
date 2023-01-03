---
title: 从Data Lake迁移到Gen2
description: 了解Adobe Experience Platform中将数据湖迁移到Gen2所提供的新功能。
exl-id: 56d9c77a-d7eb-498d-994f-b15d150dedb7
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '286'
ht-degree: 0%

---

# Adobe Experience Platform数据湖迁移到Gen2

Adobe Experience Platform正在迁移到Gen2 Data Lake。 这是新一代数据湖，它为Platform用户提供了诸如地理区域复制、更精细的基于角色的访问控制(RBAC)和更好的扩展等优势。

## 用户影响

当Adobe将数据湖从第1代迁移到第2代时，用户将能够 **读取** 数据湖，但所有 **写入** 数据湖中的受众将会受到影响。 以下是受影响的功能列表：

- **源**:来自源和各种数据获取工作流的数据将会延迟。 迁移完成后，用户将看到其数据。
- **查询服务**:用户可以执行查询，但无法将查询的输出写入数据集。
- **实时客户资料**:通过 **批次** 迁移期间将不提供摄取。 但是，通过 **流** 迁移期间将可以使用摄取。 此外，配置文件导出在迁移期间将不可用。
- **数据科学工作区**:从数据科学工作区写入操作将失败。
- **Segmentation Service**:从 **批次** 迁移期间无法激活分段。 从 **流** 区段不会受到影响。
- **Customer Journey Analytics**:Customer Journey Analytics报表数据可能已过期，在迁移期间不会刷新，因为未将批次摄取到数据湖中。

## 与平台用户的通信

Adobe将联系系统管理员以详细讨论迁移的影响，并确认特定IMS组织的迁移日期和时间。
