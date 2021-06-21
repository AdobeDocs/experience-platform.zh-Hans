---
keywords: 数据管理rtcdp;rtcdp数据管理；实时客户数据配置文件数据管理；隐私rtcdp;rtcdp隐私
title: 实时客户数据平台中的隐私
seo-title: 实时客户数据平台中的隐私
description: 实时客户数据平台使您能够简化保持数据操作符合隐私法规的流程。
seo-description: 实时客户数据平台使您能够简化保持数据操作符合隐私法规的流程。
exl-id: bcb0e42e-4549-4952-bb69-5534aee353f8
source-git-commit: f193787ac27e30c69d25418656ae9c59c89622dc
workflow-type: tm+mt
source-wordcount: '390'
ht-degree: 0%

---

# 实时客户数据平台中的隐私

[!DNL Real-time Customer Data Platform] ([!DNL Real-time CDP])帮助营销人员将多个企业系统中的数据整合在一起，以便他们更好地识别、了解和吸引客户。Adobe将消费者数据隐私视为一项基本设计原则，并提供各种控件来帮助营销人员管理其客户的数据隐私。

大多数[!DNL Real-time CDP]功能由Adobe Experience Platform提供支持。 本文档提供了有关[!DNL Real-time CDP]支持的各种隐私增强技术的信息，并提供了指向[!DNL Experience Platform]文档的链接以了解更多信息。

## 响应客户访问和删除请求

[!DNL General Data Protection Regulation](GDPR)和[!DNL California Consumer Privacy Act](CCPA)等法律隐私法规规定，客户有权请求访问或删除您从他们那里收集的个人数据。 由于[!DNL Real-time CDP]利用[!DNL Experience Platform]功能进行数据收集和存储，因此应在[!DNL Platform]中管理客户访问和删除其个人数据的请求。 有关更多信息，请参阅[Adobe Experience Platform Privacy Service](../../privacy-service/home.md)上的概述。

## 选择退出功能

[!DNL Real-time CDP] 允许客户选择禁止在分段用例中包含其个人数据。[!DNL Real-time Customer Profile]会捕获并存储客户的选择退出首选项，通过在区段谓词中使用布尔逻辑(“AND NOT”)排除已选择退出区段的用户，可以强制执行这些首选项。

有关更多信息，请参阅Adobe Experience Platform Segmentation Service文档中关于[遵守选择退出请求](../../segmentation/consents.md)的文档。

## 支持IAB TCF 2.0

[!DNL Real-time CDP] 构建于Adobe Experience Platform上，是注册的供 [应](https://iabeurope.eu/vendor-list-tcf-v2-0/) 商列表 [!DNL Transparency & Consent Framework (TCF)]的一部分，如 [!DNL Interactive Advertising Bureau (IAB)]所述根据TCF 2.0要求，Platform允许您收集详细的客户同意数据并将其集成到存储的客户配置文件中。 然后，可以根据特定用户档案的用例，在导出的受众区段中是否包含特定用户档案时，可以将此同意数据考虑在内。

有关更多信息，请参阅Experience Platform](../../landing/governance-privacy-security/consent/iab/overview.md)中的[IAB TCF 2.0支持概述。

## 后续步骤

本文档简要介绍[!DNL Real-time CDP]的隐私功能。 有关每项功能的更多信息，请参阅本指南中链接的文档。
