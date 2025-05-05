---
keywords: 数据治理rtcdp；rtcdp数据治理；实时客户数据配置文件数据治理；隐私rtcdp；rtcdp隐私
title: Real-Time Customer Data Platform中的隐私
description: Adobe Real-Time Customer Data Platform允许您简化使数据操作符合隐私法规的过程。
feature: Get Started, Privacy
exl-id: bcb0e42e-4549-4952-bb69-5534aee353f8
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '387'
ht-degree: 0%

---

# Real-Time Customer Data Platform中的隐私

[!DNL Adobe Real-Time Customer Data Platform] ([!DNL Real-Time CDP])可帮助营销人员将来自多个企业系统的数据汇集在一起，使他们能够更好地识别、理解和吸引客户。 Adobe将消费者数据隐私视为基本设计原则，并提供各种控制以帮助营销人员管理其客户的数据隐私。

大多数[!DNL Real-Time CDP]功能由Adobe Experience Platform提供支持。 本文档提供了有关[!DNL Real-Time CDP]支持的各种隐私增强技术的信息，以及指向[!DNL Experience Platform]文档的链接以获取更多信息。

## 接受客户访问和删除请求

法律隐私法规(如[!DNL General Data Protection Regulation] (GDPR)和[!DNL California Consumer Privacy Act] (CCPA))授予客户请求访问或删除您从他们那里收集的个人数据的权利。 由于[!DNL Real-Time CDP]利用了[!DNL Experience Platform]的数据收集和存储功能，因此应在[!DNL Experience Platform]内管理客户访问和删除其个人数据的请求。 有关详细信息，请参阅[Adobe Experience Platform Privacy Service](../../privacy-service/home.md)的概述。

>[!IMPORTANT]
>
> 通过Adobe Experience Platform Privacy Service for Adobe Marketo Engage提交的隐私请求仅适用于Real-Time CDP B2B客户。

## 选择退出功能

[!DNL Real-Time CDP]允许客户选择不将其个人数据包含在分段用例中。 客户的选择退出偏好设置由[!DNL Real-Time Customer Profile]捕获和存储，并且可以通过在区段谓词中使用布尔逻辑(“AND NOT”)排除已选择退出受众的用户来强制执行。

有关详细信息，请参阅Adobe Experience Platform Segmentation Service文档中有关[接受选择退出请求](../../segmentation/tutorials/consents.md)的文档。

## IAB TCF 2.0支持

[!DNL Real-Time CDP]基于Adobe Experience Platform构建，该列表是[!DNL Transparency & Consent Framework (TCF)]的已注册[供应商列表](https://iabeurope.eu/vendor-list-tcf/)的一部分，如[!DNL Interactive Advertising Bureau (IAB)]所述。 为符合TCF 2.0要求，Experience Platform允许您收集详细的客户同意数据，并将其集成到存储的客户配置文件中。 然后，可以根据导出受众的用例将这些同意数据纳入特定用户档案是否包含在导出受众中。

有关详细信息，请参阅Experience Platform[&#128279;](../../landing/governance-privacy-security/consent/iab/overview.md)中对IAB TCF 2.0支持的概述。

## 后续步骤

本文档简要介绍了[!DNL Real-Time CDP]的隐私功能。 请查看本指南中链接的文档以了解有关每个功能的更多信息。
