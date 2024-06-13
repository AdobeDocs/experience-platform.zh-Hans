---
title: AI助手中的隐私、安全和管理
description: 了解AI Assistant的隐私、安全和治理实践。
exl-id: 371e065d-c2dd-4233-b78e-a42757fce853
source-git-commit: e14bf4191319d646c6c4bfd55656fc6de141e9ca
workflow-type: tm+mt
source-wordcount: '292'
ht-degree: 0%

---

# AI助手中的隐私、安全和管理

Adobe Experience Platform中的AI助手以隐私、安全和治理为原则。

请阅读本文档，了解您可以期待从AI Assistant获得的以客户信任为中心的功能：

* 目前，AI助手没有使用任何个人数据，即使用于培训目的也是如此。
* AI助手不知道消费者数据。
* 所有现有 [访问控制](../access-control/home.md) AI助手将遵循策略。
   * 任何基于属性的新访问控制策略在最多24小时后反映在AI助手中*
* 必须向您授予显式权限才能与AI助手交互。
   * 您可以使用为Experience Platform和Journey Optimizer设置不同的权限 [权限UI](../access-control/abac/ui/permissions.md) 你可以使用 [Admin Console](../access-control/ui/browse.md) 以为Customer Journey Analytics分配权限。
   * 权限是细粒度的，沙盒管理员可以配置哪些用户可以询问不同类别的问题（使用AI助手基于产品知识的问题或有关操作见解的问题）。
* 在与Adobe Experience Platform Healthcare Shield结合使用时，AI Assistant是HIPAA就绪功能。
* 您可以查看之前与AI助手进行的交互的日志，保留策略为30天。
* 在响应Adobe提示时，AI助手基于特定于沙盒的数据和公共用户文档。 数据不会在沙盒之间共享。
* 您提供给AI助理的提示不会共享给其他客户。

**这意味着，如果向字段和对象添加任何新标签或创建任何新策略，则AI助手最多需要24小时才能遵循它们。 在这24小时内，新受限制访问的用户仍然可以访问这些字段和对象。*
