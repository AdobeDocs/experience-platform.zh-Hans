---
title: Adobe Experience Platform中的客户管理的密钥
description: 了解如何为Adobe Experience Platform中存储的数据设置您自己的加密密钥。
role: Developer
feature: Privacy
exl-id: cd33e6c2-8189-4b68-a99b-ec7fccdc9b91
source-git-commit: f2737355ca0652f434bd5f86acc65139f767e56f
workflow-type: tm+mt
source-wordcount: '828'
ht-degree: 0%

---

# Adobe Experience Platform中的客户管理的密钥

存储在Adobe Experience Platform上的数据使用系统级别密钥静态加密。 如果您使用的是基于Platform构建的应用程序，则可以选择使用自己的加密密钥，从而更好地控制数据安全。

>[!AVAILABILITY]
>
>如果您的Experience Platform实施在Amazon Web Services (AWS)上运行，则您可以选择使用密钥管理服务(KMS)进行平台数据加密。 在AWS上运行的Experience Platform当前仅对有限数量的客户可用。 要了解有关支持的Experience Platform基础架构的更多信息，请参阅[Experience Platform多云概述](https://experienceleague.adobe.com/en/docs/experience-platform/landing/multi-cloud)。 要了解如何在AWS KMS中创建和管理加密密钥，请参阅[AWS KMS数据加密指南](../key-management-service/overview.md)。

>[!NOTE]
>
>存储在Platform [!DNL Azure Data Lake]和[!DNL Azure Cosmos DB]配置文件存储区的客户配置文件数据在启用后将使用CMK进行独占加密。 主数据存储中的密钥吊销可能需要&#x200B;**几分钟到24小时**&#x200B;之间的任何时间，对于临时或辅助数据存储，可能需要更长时间&#x200B;**到7天**。 有关其他详细信息，请参阅[撤销密钥访问权限的影响部分](#revoke-access)。

本文档提供了在Platform中启用客户管理的密钥(CMK)功能的过程的高级概述，以及完成这些步骤所需的先决条件信息。

>[!NOTE]
>
>对于Customer Journey Analytics客户，请按照[Customer Journey Analytics文档](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-privacy/cmk.html?lang=zh-Hans)中的说明操作。

## 先决条件

要查看和访问Adobe Experience Platform中的[!UICONTROL 加密]部分，您必须已创建一个角色，并为其分配了[!UICONTROL 管理客户管理的密钥]权限。 任何具有[!UICONTROL 管理客户管理的密钥]权限的用户都可以为其组织启用CMK。

有关在Experience Platform中分配角色和权限的详细信息，请参阅[配置权限文档](https://experienceleague.adobe.com/docs/platform-learn/getting-started-for-data-architects-and-data-engineers/configure-permissions.html)。

为了启用CMK，必须使用以下设置配置您的[!DNL Azure]密钥库：

* [启用清除保护](https://learn.microsoft.com/en-us/azure/key-vault/general/soft-delete-overview#purge-protection)
* [启用软删除](https://learn.microsoft.com/en-us/azure/key-vault/general/soft-delete-overview)
* [使用基于 [!DNL Azure] 角色的访问控制配置访问](https://learn.microsoft.com/en-us/azure/role-based-access-control/)

请阅读链接的文档，以更好地了解此过程。

## 流程摘要 {#process-summary}

CMK包含在Healthcare Shield以及Adobe的Privacy and Security Shield产品中。 贵组织在购买其中一种产品的许可证后，可以开始一次性流程来设置该功能。

>[!WARNING]
>
>设置CMK后，无法还原为系统管理的密钥。 您有责任安全地管理您的密钥，并在[!DNL Azure]内提供对您的密钥库、密钥和CMK应用程序的访问权限，以防止无法访问您的数据。

该过程如下：

1. [根据您组织的策略配置 [!DNL Azure] 密钥保管库](./azure-key-vault-config.md)，然后[生成最终与Adobe共享的加密密钥](./azure-key-vault-config.md#generate-a-key)。
1. 通过[API调用](./api-set-up.md#register-app)或[UI](./ui-set-up.md#register-app)与您的[!DNL Azure]租户设置CMK应用。
1. 在UI](./ui-set-up.md#send-to-adobe)中或通过[API调用](./api-set-up.md#send-to-adobe)将您的加密密钥ID发送到Adobe并启动该功能的启用过程。[
1. 检查配置的状态，以验证是否已在UI](./ui-set-up.md#check-status)中[或通过[API调用](./api-set-up.md#check-status)启用CMK。

设置过程完成后，所有沙盒上载到Platform的所有数据将使用您的[!DNL Azure]密钥设置进行加密。 若要使用CMK，您将利用可能属于其[公共预览计划](https://azure.microsoft.com/en-ca/support/legal/preview-supplemental-terms/)的[!DNL Microsoft Azure]功能。

## 撤销关键访问权限的影响 {#revoke-access}

撤销或禁用对Key Vault、Key或CMK应用程序的访问权限可能会导致严重中断，包括对您平台操作的重大更改。 禁用这些键后，Platform中的数据可能会变得不可访问，并且任何依赖此数据的下游操作都将停止运行。 在对关键配置进行任何更改之前，充分了解下游影响至关重要。

如果您决定撤销Platform对您的数据的访问权限，可以通过从[!DNL Azure]中的密钥保管库中删除与应用程序关联的用户角色来实现此操作。

### 传播时间线 {#propagation-timelines}

在从[!DNL Azure]密钥保管库撤消密钥访问权限后，更改将按如下方式传播：

| **存储类型** | **描述** | **时间线** |
|---|---|---|
| 主数据存储 | 这些存储包括Azure Data Lake和Azure Cosmos DB配置文件存储。 一旦撤销密钥访问，数据将无法访问。 | **分钟到24小时**。 |
| 缓存/临时数据存储 | 包括用于性能和核心应用程序功能的数据存储。 密钥吊销的影响延迟。 | **最多7天**。 |

例如，配置文件仪表板将继续显示其缓存中的数据，最多显示七天，之后数据将过期并刷新。 同样，重新启用对应用程序的访问需要相同的时间来恢复这些存储中的数据可用性。

>[!NOTE]
>
>对于非主（缓存/临时）数据的7天数据集到期，存在两个特定于用例的异常。 有关这些功能的更多信息，请参阅各自的文档。<ul><li>[Adobe Journey Optimizer URL Shortener](https://experienceleague.adobe.com/docs/journey-optimizer/using/sms/sms-configuration.html?lang=zh-Hans#message-preset-sms)</li><li>[Edge投影](https://experienceleague.adobe.com/docs/experience-platform/profile/home.html#edge-projections)</li></ul>

## 后续步骤

要开始此过程，请[配置 [!DNL Azure] 密钥保管库](./azure-key-vault-config.md)和[生成要与Adobe共享的加密密钥](./azure-key-vault-config.md#generate-a-key)。
