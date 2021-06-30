---
title: 从Data Lake迁移到Gen2
description: 了解Adobe Experience Platform中将数据湖迁移到Gen2所提供的新功能。
exl-id: 56d9c77a-d7eb-498d-994f-b15d150dedb7
source-git-commit: 97f803f649b2c42b0449a2f8f0cff370ed1aba93
workflow-type: tm+mt
source-wordcount: '286'
ht-degree: 0%

---

# Adobe Experience Platform数据湖迁移到Gen2

Adobe Experience Platform正在迁移到Gen2 Data Lake。 这是新一代数据湖，它为Platform用户提供了诸如地理区域复制、更精细的基于角色的访问控制(RBAC)和更好的扩展等优势。

## 用户影响

当Adobe将数据湖从Gen1迁移到Gen2时，用户将能够从数据湖中&#x200B;**读取**，但将&#x200B;**写入数据湖中的所有功能都将受到影响。**&#x200B;以下是受影响的功能列表：

- **来源**:来自源和各种数据获取工作流的数据将会延迟。迁移完成后，用户将看到其数据。
- **查询服务**:用户可以执行查询，但无法将查询的输出写入数据集。
- **实时客户资料**:在迁移期间，通过批次摄取 **** 摄取到用户档案存储的数据将不可用。但是，通过&#x200B;**流**&#x200B;摄取的数据将在迁移期间可用。 此外，配置文件导出在迁移期间将不可用。
- **数据科学工作区**:从数据科学工作区写入操作将失败。
- **分段服务**:迁移期间 **** 无法激活从批量分段派生的受众。从&#x200B;**流**&#x200B;分段派生的受众不会受到影响。
- **Customer Journey Analytics**:Customer Journey Analytics报表数据可能已过期，在迁移期间不会刷新，因为未将批次摄取到数据湖中。

## 与平台用户的通信

Adobe将联系系统管理员以详细讨论迁移的影响，并确认特定IMS组织的迁移日期和时间。
