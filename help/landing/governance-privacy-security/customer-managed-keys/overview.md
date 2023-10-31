---
title: Adobe Experience Platform中的客户管理的密钥
description: 了解如何为Adobe Experience Platform中存储的数据设置您自己的加密密钥。
exl-id: cd33e6c2-8189-4b68-a99b-ec7fccdc9b91
source-git-commit: 930c786db51063c55f731dc90f2ee66e98624555
workflow-type: tm+mt
source-wordcount: '763'
ht-degree: 2%

---

# Adobe Experience Platform中的客户管理的密钥

存储在Adobe Experience Platform上的数据使用系统级别密钥静态加密。 如果您使用的是基于Platform构建的应用程序，则可以选择使用自己的加密密钥，从而更好地控制数据安全。

>[!NOTE]
>
>Adobe Experience Platform Data Lake和Profile Store中的数据是使用CMK加密的。 这些存储区被视为您的主数据存储。

本文档提供了在Platform中启用客户管理的密钥(CMK)功能的过程的高级概述，以及完成这些步骤所需的先决条件信息。

>[!NOTE]
>
>对于Customer Journey Analytics客户，请按照 [Customer Journey Analytics文档](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-privacy/cmk.html?lang=en).

## 先决条件

要查看和访问 [!UICONTROL 加密] Adobe Experience Platform部分，您必须已创建一个角色并分配 [!UICONTROL 管理客户管理的密钥] 该角色的权限。 任何具有 [!UICONTROL 管理客户管理的密钥] 权限可以为他们的组织启用CMK。

有关在Experience Platform中分配角色和权限的详细信息，请参阅 [配置权限文档](https://experienceleague.adobe.com/docs/platform-learn/getting-started-for-data-architects-and-data-engineers/configure-permissions.html).

为了启用CMK，您的 [!DNL Azure] 必须使用以下设置配置密钥保管库：

* [启用清除保护](https://learn.microsoft.com/en-us/azure/key-vault/general/soft-delete-overview#purge-protection)
* [启用软删除](https://learn.microsoft.com/en-us/azure/key-vault/general/soft-delete-overview)
* [使用配置访问 [!DNL Azure] 基于角色的访问控制](https://learn.microsoft.com/en-us/azure/role-based-access-control/)

请阅读链接的文档，以更好地了解此过程。

## 流程摘要 {#process-summary}

CMK包含在Healthcare Shield以及Adobe的Privacy and Security Shield产品中。 贵组织在购买其中一种产品的许可证后，可以开始一次性流程来设置该功能。

>[!WARNING]
>
>设置CMK后，无法还原为系统管理的密钥。 您负责安全地管理您的密钥，并在中提供对您的密钥库、密钥和CMK应用程序的访问权限 [!DNL Azure] 以防止无法访问您的数据。

该过程如下：

1. [配置 [!DNL Azure] 密钥库](./azure-key-vault-config.md) 根据贵组织的策略，则 [生成加密密钥](./azure-key-vault-config.md#generate-a-key) 最终将与Adobe共享。
1. 使用设置CMK应用程序 [!DNL Azure] 通过任一项租户 [API调用](./api-set-up.md#register-app) 或 [UI](./ui-set-up.md#register-app).
1. 将您的加密密钥ID发送到Adobe，然后启动该功能的启用过程 [在UI中](./ui-set-up.md#send-to-adobe) 或使用 [API调用](./api-set-up.md#send-to-adobe).
1. 检查配置的状态以验证是否已启用CMK [在UI中](./ui-set-up.md#check-status) 或使用 [API调用](./api-set-up.md#check-status).

完成设置过程后，所有通过沙盒载入到Platform中的所有数据将使用以下加密： [!DNL Azure] 键设置。 要使用CMK，您将利用 [!DNL Microsoft Azure] 作为其一部分的功能 [公共预览项目](https://azure.microsoft.com/en-ca/support/legal/preview-supplemental-terms/).

## 撤销访问权限 {#revoke-access}

如果要撤销平台对您的数据的访问权限，可以从的密钥保管库中移除与应用程序关联的用户角色 [!DNL Azure].

>[!WARNING]
>
>禁用密钥保险库、密钥或CMK应用程序可能会导致重大更改。 一旦禁用密钥保管库、密钥或CMK应用程序，并且数据在Platform中不再可访问，则与该数据相关的任何下游操作都将不再可能。 在对配置进行任何更改之前，请确保您了解撤销平台对您密钥的访问权限将会产生的下游影响。

删除密钥访问权限或禁用/删除密钥后 [!DNL Azure] 密钥库中，此配置可能需要几分钟到24小时的时间才能传播到主数据存储。 平台工作流还包括性能和核心应用程序功能所需的缓存和临时数据存储。 通过此类缓存和临时存储传播CMK撤销最多可能需要七天，具体取决于其数据处理工作流。 例如，这意味着“配置文件”仪表板将保留并显示其缓存数据存储中的数据，并且作为刷新周期的一部分，需要七天时间使缓存数据存储中保留的数据过期。 在重新启用对应用程序的访问时，数据再次变为可用同样的时间延迟。

>[!NOTE]
>
>对于非主（缓存/临时）数据的7天数据集到期，存在两个特定于用例的异常。 有关这些功能的更多信息，请参阅各自的文档。<ul><li>[Adobe Journey Optimizer URL Shortener](https://experienceleague.adobe.com/docs/journey-optimizer/using/sms/sms-configuration.html?lang=zh-Hans#message-preset-sms)</li><li>[边缘投影](https://experienceleague.adobe.com/docs/experience-platform/profile/home.html#edge-projections)</li></ul>

## 后续步骤

要开始此过程，请首先执行 [配置 [!DNL Azure] 密钥库](./azure-key-vault-config.md) 和 [生成加密密钥](./azure-key-vault-config.md#generate-a-key) 以与Adobe共享。
