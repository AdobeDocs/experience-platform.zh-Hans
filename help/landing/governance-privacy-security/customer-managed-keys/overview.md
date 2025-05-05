---
title: Adobe Experience Platform中的客户管理的密钥
description: 了解如何为Adobe Experience Platform中存储的数据设置您自己的加密密钥。
role: Developer
feature: Privacy
exl-id: cd33e6c2-8189-4b68-a99b-ec7fccdc9b91
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1111'
ht-degree: 0%

---

# Adobe Experience Platform中的客户管理的密钥

存储在Adobe Experience Platform上的数据使用系统级别密钥静态加密。 如果您使用的是基于Experience Platform构建的应用程序，则可以选择使用自己的加密密钥，从而更好地控制数据安全。

>[!AVAILABILITY]
>
>Adobe Experience Platform支持Microsoft Azure和Amazon Web Services (AWS)的客户托管密钥(CMK)。 在AWS上运行的Experience Platform当前仅对有限数量的客户可用。 如果您的实施在AWS上运行，您可以选择使用密钥管理服务(KMS)进行Experience Platform数据加密。 有关所支持的基础结构的更多信息，请参阅[Experience Platform multi-cloud概述](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/landing/multi-cloud)。
>
>要了解如何在AWS KMS中创建和管理加密密钥，请参阅[AWS KMS数据加密指南](./aws/configure-kms.md)。 有关Azure实施的信息，请参阅[Azure Key Vault配置指南](./azure/azure-key-vault-config.md)。

>[!NOTE]
>
>对于[!DNL Azure]托管的Experience Platform实例，存储在Experience Platform的[!DNL Azure Data Lake]和[!DNL Azure Cosmos DB]配置文件存储中的客户配置文件数据在启用后将使用CMK进行独占加密。 对于临时或辅助数据存储，主数据存储中的密钥吊销可能需要&#x200B;**几分钟到24小时**&#x200B;和&#x200B;**最多7天**&#x200B;的时间。 有关其他详细信息，请参阅[撤销密钥访问权限的影响部分](#revoke-access)。

本文档提供了在Experience Platform中通过[!DNL Azure]和AWS启用客户管理的密钥(CMK)功能的过程的高级概述，以及完成这些步骤所需的先决条件信息。

>[!NOTE]
>
>对于Customer Journey Analytics客户，请按照[Customer Journey Analytics文档](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-privacy/cmk.html?lang=zh-Hans)中的说明操作。

## 先决条件

要启用CMK，您平台的托管环境([!DNL Azure]或AWS)必须满足特定的配置要求：

### 一般先决条件

要查看和访问Adobe Experience Platform中的[!UICONTROL 加密]部分，您必须已创建一个角色，并为其分配了[!UICONTROL 管理客户管理的密钥]权限。  任何具有[!UICONTROL 管理客户管理的密钥]权限的用户都可以为其组织启用CMK。

有关在Experience Platform中分配角色和权限的详细信息，请参阅[配置权限文档](https://experienceleague.adobe.com/docs/platform-learn/getting-started-for-data-architects-and-data-engineers/configure-permissions.html?lang=zh-Hans)。

### 特定于Azure的先决条件

对于Azure托管的实施，请使用以下设置配置您的[!DNL Azure]密钥保管库：

- [启用清除保护](https://learn.microsoft.com/en-us/azure/key-vault/general/soft-delete-overview#purge-protection)
- [启用软删除](https://learn.microsoft.com/en-us/azure/key-vault/general/soft-delete-overview)
- [使用基于 [!DNL Azure] 角色的访问控制配置访问](https://learn.microsoft.com/en-us/azure/role-based-access-control/)

### 特定于AWS的先决条件

对于AWS托管的实施，请按照以下方式配置您的AWS环境：

- 确保您有权使用AWS Identity and Access Management (IAM)管理加密密钥。 有关详细信息，请参阅[适用于AWS KMS的IAM策略](https://docs.aws.amazon.com/kms/latest/developerguide/iam-policies.html)。
- 设置支持CMK的AWS KMS。 请参阅[AWS KMS数据加密指南](./aws/configure-kms.md)。

## 流程摘要 {#process-summary}

客户管理的密钥(CMK)可通过Adobe的Healthcare Shield和Privacy and Security Shield产品获取。 在Azure上，Healthcare Shield和Privacy and Security Shield都支持CMK。 在AWS上，CMK仅受Privacy and Security Shield支持，不适用于Healthcare Shield。 贵组织在购买其中一种产品的许可证后，即可开始一次性设置过程以启用CMK。

>[!WARNING]
>
>设置CMK后，无法还原为系统管理的密钥。 您有责任安全地管理您的密钥，以防止无法访问您的数据。

该过程如下：

### 对于Azure {#azure-process-summary}

1. [根据您组织的策略配置 [!DNL Azure] 密钥保管库](./azure/azure-key-vault-config.md)，然后[生成要与Adobe共享的加密密钥](./azure/azure-key-vault-config.md#generate-a-key)。
1. 通过[API调用](./azure/api-set-up.md#register-app)或[UI](./azure/ui-set-up.md#register-app)与您的[!DNL Azure]租户设置CMK应用。
1. 将您的加密密钥ID发送到Adobe，并通过UI[&#128279;](./azure/ui-set-up.md#send-to-adobe)中的或通过[API调用](./azure/api-set-up.md#send-to-adobe)启动该功能的启用过程。
1. 检查配置的状态以验证UI[&#128279;](./azure/ui-set-up.md#check-status)中的或通过[API调用](./azure/api-set-up.md#check-status)是否启用了CMK。

一旦完成Azure托管的Experience Platform实例的设置过程，所有沙盒中载入到Experience Platform的所有数据将使用您的[!DNL Azure]密钥设置进行加密。 若要使用CMK，您将利用可能属于其[公共预览计划](https://azure.microsoft.com/en-ca/support/legal/preview-supplemental-terms/)的[!DNL Microsoft Azure]功能。

### 适用于AWS的 {#aws-process-summary}

1. [通过配置要与AWS共享的加密密钥来设置Adobe KMS](./aws/configure-kms.md)。
2. 按照[UI设置指南](./aws/ui-set-up.md)中特定于AWS的说明进行操作。
3. 验证设置，以确认已使用AWS托管的密钥对Experience Platform数据进行加密。

<!--  Pending: or [API setup guide]() -->

一旦完成AWS托管的Experience Platform实例的设置过程，所有沙盒中载入到Experience Platform的所有数据都将使用您的AWS密钥管理服务(KMS)配置进行加密。 要在AWS上使用CMK，您将使用AWS密钥管理服务根据贵组织的安全要求创建和管理加密密钥。

## 撤销关键访问权限的影响 {#revoke-access}

撤销或禁用对Azure中的密钥保管库、密钥或CMK应用程序或AWS中的加密密钥的访问权限可能会导致严重中断，包括对您的Experience Platform操作进行的重大更改。 禁用键后，Experience Platform中的数据可能会变得不可访问，并且任何依赖此数据的下游操作都将停止运行。 在对关键配置进行任何更改之前，充分了解下游影响至关重要。

要撤销Experience Platform对[!DNL Azure]中数据的访问权限，请从密钥保管库中删除与应用程序关联的用户角色。 对于AWS，您可以禁用键或更新策略语句。 有关AWS进程的详细说明，请参阅[密钥吊销部分](./aws/ui-set-up.md#key-revocation)。


### 传播时间线 {#propagation-timelines}

在从[!DNL Azure]密钥保管库撤消密钥访问权限后，更改将按如下方式传播：

| **存储类型** | **描述** | **时间线** |
|---|---|---|
| 主数据存储 | 包括数据湖(Azure Data Lake、AWS S3)和Azure Cosmos DB配置文件存储。 一旦撤销密钥访问，数据将无法访问。 | **分钟到24小时**。 |
| 缓存/临时数据存储 | 包括用于性能和核心应用程序功能的辅助数据存储。 密钥吊销的影响延迟。 | **最多7天**。 |

例如，配置文件仪表板将继续显示其缓存中的数据，最多显示七天，之后数据将过期并刷新。 同样，重新启用对应用程序的访问需要相同的时间来恢复这些存储中的数据可用性。

>[!NOTE]
>
>重新启用对应用程序的访问可能需要与吊销相同的时间来恢复这些存储中的数据可用性。

>[!TIP]
>
>对于非主（缓存/临时）数据的7天数据集到期，存在两个特定于用例的异常。 有关这些功能的更多信息，请参阅各自的文档。<ul><li>[Adobe Journey Optimizer URL Shortener](https://experienceleague.adobe.com/docs/journey-optimizer/using/sms/sms-configuration.html?lang=zh-Hans#message-preset-sms)</li><li>[Edge投影](https://experienceleague.adobe.com/docs/experience-platform/profile/home.html?lang=zh-Hans#edge-projections)</li></ul>

## 后续步骤

要开始此过程，请执行以下操作：

- 对于Azure：首先由[配置 [!DNL Azure] 密钥保管库](./azure/azure-key-vault-config.md)和[生成要与Adobe共享的加密密钥](./azure/azure-key-vault-config.md#generate-a-key)开始。
- 对于AWS： [在继续阅读UI或API设置指南之前，请设置AWS KMS](./aws/configure-kms.md)并确保正确的IAM和KMS配置。
