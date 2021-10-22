---
title: Privacy ServiceAPI指南
description: 了解如何使用Privacy ServiceAPI以编程方式管理受支持Adobe Experience Cloud应用程序的隐私作业。
source-git-commit: 196147e7691010707953561c110a3934fec8ba1b
workflow-type: tm+mt
source-wordcount: '265'
ht-degree: 0%

---

# [!DNL Privacy Service] API指南

Privacy ServiceAPI提供了多个端点，允许您以编程方式管理贵组织的隐私作业。 下面概述了这些端点。 有关详细信息，请访问各个端点指南，并参阅 [入门指南](./getting-started.md) 有关所需标头、读取示例API调用等的重要信息。

>[!NOTE]
>
>本指南介绍如何使用 [!DNL Privacy Service] API。 有关如何使用UI的详细信息，请参阅 [Privacy ServiceUI概述](../ui/overview.md).

要查看所有可用的端点和CRUD操作，请访问 [Privacy ServiceAPI参考](https://www.adobe.io/experience-platform-apis/references/privacy-service/).

## 隐私作业

当Privacy Service收到访问或删除主体个人数据的请求时，系统创建隐私作业以满足该请求。 每个隐私作业都包含与数据主体相关的身份信息、有关作业所应用的Adobe Experience Cloud产品的元数据以及作业的处理状态。

的 `/jobs` 端点允许您为组织创建和检索隐私作业。 要了解如何使用此端点，请参阅 [隐私作业端点指南](./privacy-jobs.md).

## 同意

某些法规要求客户明确同意后才能收集其个人数据。 的 `/consent` 端点允许您处理客户同意请求，并将它们集成到您的隐私工作流程中。 请参阅 [consent endpoint指南](./consent.md) 以了解更多。

## 后续步骤

要开始使用Privacy ServiceAPI进行调用，请阅读 [入门指南](./getting-started.md) 然后，选择一个端点指南以了解如何使用特定端点。
