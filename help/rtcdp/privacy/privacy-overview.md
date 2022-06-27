---
keywords: 数据管理rtcdp;rtcdp数据管理；实时客户数据配置文件数据管理；隐私rtcdp;rtcdp隐私
title: Real-time Customer Data Platform中的隐私
description: Real-time Customer Data Platform使您能够简化保持数据操作符合隐私法规的流程。
exl-id: bcb0e42e-4549-4952-bb69-5534aee353f8
source-git-commit: ad0d38cbd249642d582a807c5679065827f57717
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 0%

---

# Real-time Customer Data Platform中的隐私

[!DNL Real-time Customer Data Platform] ([!DNL Real-time CDP])可帮助营销人员将多个企业系统中的数据整合在一起，以便他们更好地识别、了解和吸引客户。 Adobe将消费者数据隐私视为一项基本设计原则，并提供各种控件来帮助营销人员管理其客户的数据隐私。

大多数 [!DNL Real-time CDP] 功能由Adobe Experience Platform提供支持。 本文档提供了有关支持的各种隐私增强技术的信息 [!DNL Real-time CDP]，且链接指向 [!DNL Experience Platform] 文档以了解更多信息。

## 响应客户访问和删除请求

法律隐私法规，例如 [!DNL General Data Protection Regulation] (GDPR)和 [!DNL California Consumer Privacy Act] (CCPA)授予客户请求访问或删除您从他们那里收集的个人数据的权利。 自 [!DNL Real-time CDP] 利用 [!DNL Experience Platform] 数据收集和存储功能、客户访问和删除其个人数据的请求应在 [!DNL Platform]. 请参阅 [Adobe Experience Platform Privacy Service](../../privacy-service/home.md) 以了解更多信息。

>[!IMPORTANT]
>
> 通过Adobe Experience Platform Privacy Service提交的Adobe Marketo Engage隐私请求仅适用于实时CDP B2B客户。

## 选择退出功能

[!DNL Real-time CDP] 允许客户选择禁止在分段用例中包含其个人数据。 客户的选择退出首选项由 [!DNL Real-time Customer Profile]，并可以通过在区段谓词中使用布尔逻辑(“AND NOT”)排除已选择退出区段的用户来强制执行。

请参阅 [响应选择退出请求](../../segmentation/consents.md) (位于Adobe Experience Platform Segmentation Service文档中)以了解更多信息。

## 支持IAB TCF 2.0

[!DNL Real-time CDP] 构建于Adobe Experience Platform上，该网站是已注册的 [供应商列表](https://iabeurope.eu/vendor-list-tcf-v2-0/) 对于 [!DNL Transparency & Consent Framework (TCF)]，如 [!DNL Interactive Advertising Bureau (IAB)]. 根据TCF 2.0要求，Platform允许您收集详细的客户同意数据并将其集成到存储的客户配置文件中。 然后，可以根据特定用户档案的用例，在导出的受众区段中是否包含特定用户档案时，可以将此同意数据考虑在内。

请参阅 [IAB TCF 2.0支持Experience Platform](../../landing/governance-privacy-security/consent/iab/overview.md) 以了解更多信息。

## 后续步骤

本文档简要介绍 [!DNL Real-time CDP]. 有关每项功能的更多信息，请参阅本指南中链接的文档。
