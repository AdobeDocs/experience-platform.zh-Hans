---
title: Data Lake迁移到Gen2
description: 了解Adobe Experience Platform中将Data Lake迁移到Gen2提供的新功能。
exl-id: 56d9c77a-d7eb-498d-994f-b15d150dedb7
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '285'
ht-degree: 0%

---

# Adobe Experience Platform Data Lake迁移到Gen2

Adobe Experience Platform正在迁移到Gen2数据湖。 这是新一代的数据湖，可为Platform用户提供地域复制、更精细的基于角色的访问控制(RBAC)和更强大的扩展能力等优势。

## 用户影响

当Adobe将数据湖从Gen1迁移到Gen 2时，用户将能够 **读取** 来自数据湖，但所有功能 **写入** 到数据湖的操作将受影响。 以下是受影响的功能列表：

- **源**：从源和各种数据摄取工作流传入的数据将延迟。 迁移完成后，用户将看到其数据。
- **查询服务**：用户可以执行查询，但无法将查询输出写入数据集。
- **Real-time Customer Profile**：通过摄取到配置文件存储的数据 **批次** 在迁移期间，摄取将不可用。 但是，摄取的数据来自 **流** 可在迁移期间进行摄取。 此外，配置文件导出在迁移期间不可用。
- **数据科学工作区**：从Data Science Workspace写入数据将失败。
- **分段服务**：受众派生自 **批次** 无法在迁移期间激活分段。 受众派生自 **流** 分段不会受到影响。
- **Customer Journey Analytics**：Customer Journey Analytics报表数据可能已过期，在迁移期间不会刷新，因为批次未摄取到Data Lake。

## 与Platform用户的通信

Adobe将与系统管理员联系以详细讨论迁移的影响，并确认特定组织的迁移日期和时间。
