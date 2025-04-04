---
title: Data Lake迁移到Gen2
description: 了解Adobe Experience Platform中将Data Lake迁移到Gen2提供的新功能。
exl-id: 56d9c77a-d7eb-498d-994f-b15d150dedb7
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '288'
ht-degree: 0%

---

# Adobe Experience Platform Data Lake迁移到Gen2

Adobe Experience Platform正在迁移到Gen2数据湖。 这是新一代的数据湖，可为Experience Platform用户提供地域复制、更精细的基于角色的访问控制(RBAC)和更强大的扩展能力等优势。

## 用户影响

当Adobe将数据湖从Gen1迁移到Gen 2时，用户将能够从Data Lake **读取**，但&#x200B;**写入**&#x200B;到Data Lake的所有功能都将受到影响。 以下是受影响的功能列表：

- **源**：从源和各种数据摄取工作流传入的数据将延迟。 迁移完成后，用户将看到其数据。
- **查询服务**：用户可以执行查询，但无法将查询的输出写入数据集。
- **实时客户个人资料**：在迁移期间，通过&#x200B;**批处理**&#x200B;引入引入到个人资料存储的数据将不可用。 但是，通过&#x200B;**流式摄取**&#x200B;引入的数据将在迁移期间可用。 此外，配置文件导出在迁移期间不可用。
- **数据科学Workspace**：从数据科学Workspace写入将失败。
- **分段服务**：迁移期间无法激活从&#x200B;**批次**&#x200B;分段派生的受众。 从&#x200B;**流**&#x200B;分段派生的受众不会受到影响。
- **Customer Journey Analytics**： Customer Journey Analytics报表数据可能已过期，在迁移期间不会刷新，因为批次未摄取到Data Lake。

## 与Experience Platform用户的通信

Adobe将与系统管理员联系以详细讨论迁移的影响，并确认特定组织的迁移日期和时间。
