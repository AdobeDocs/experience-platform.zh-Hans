---
title: Privacy ServiceAPI指南
description: 了解如何使用Privacy ServiceAPI以编程方式管理受支持的Adobe Experience Cloud应用程序的隐私作业。
role: Developer
exl-id: 665466ac-2447-4a9d-a8cf-62092c09e431
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '261'
ht-degree: 2%

---

# [!DNL Privacy Service] API指南

Privacy ServiceAPI提供了多个端点，允许您以编程方式管理组织的隐私作业。 这些端点概述如下。 有关详细信息，请参阅各个端点指南，并参阅 [快速入门指南](./getting-started.md) 有关所需标头的重要信息，请阅读示例API调用等。

>[!NOTE]
>
>本指南介绍如何使用 [!DNL Privacy Service] API。 有关如何使用UI的详细信息，请参阅 [Privacy ServiceUI概述](../ui/overview.md).

要查看所有可用的端点和CRUD操作，请访问 [Privacy ServiceAPI参考](https://www.adobe.io/experience-platform-apis/references/privacy-service/).

## 隐私任务

当Privacy Service收到访问或删除主体个人数据的请求时，系统创建隐私作业以满足该请求。 每个隐私作业都包含与数据主体相关的身份信息、有关该作业适用的Adobe Experience Cloud产品的元数据以及作业的处理状态。

此 `/jobs` 端点允许您创建和检索组织的隐私作业。 要了解如何使用此端点，请参阅 [隐私作业端点指南](./privacy-jobs.md).

## 同意

某些法规要求客户明确同意才能收集其个人数据。 此 `/consent` 端点允许您处理客户同意请求并将它们集成到隐私工作流中。 请参阅 [同意端点指南](./consent.md) 了解更多信息。

## 后续步骤

要开始使用Privacy ServiceAPI进行调用，请阅读 [快速入门指南](./getting-started.md) 然后选择其中一个端点指南以了解如何使用特定端点。
