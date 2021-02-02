---
keywords: 数据管理rtcdp;rtcdp数据治理；实时客户数据用户档案数据治理；隐私rtcdp;rtcdp隐私
title: 实时客户数据用户档案中的隐私
seo-title: 实时客户数据用户档案中的隐私
description: 实时客户用户档案使您能够简化数据操作遵守隐私法规的流程。
seo-description: 实时客户用户档案使您能够简化数据操作遵守隐私法规的流程。
translation-type: tm+mt
source-git-commit: 49c984a60fd699706eec508ec1d786340df40b57
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 0%

---


# [!DNL Real-time CDP]中的隐私

[!DNL Real-time Customer Data Platform] ([!DNL Real-time CDP])帮助营销人员将多个企业系统中的数据整合在一起，使他们能够更好地识别、理解和吸引客户。Adobe将消费者数据隐私视为一项基本的设计原则，并提供各种控件来帮助营销人员管理其客户的数据隐私。

大多数[!DNL Real-time CDP]功能由Adobe Experience Platform提供。 本文档提供有关[!DNL Real-time CDP]支持的各种隐私增强技术的信息，并提供指向[!DNL Experience Platform]文档的链接以了解更多信息。

## 支持客户访问和删除请求

法律隐私法规(如[!DNL General Data Protection Regulation](GDPR)和[!DNL California Consumer Privacy Act](CCPA))赋予客户权利请求访问或删除您从他们那里收集的个人数据。 由于[!DNL Real-time CDP]利用[!DNL Experience Platform]功能进行数据收集和存储，因此应在[!DNL Platform]内管理客户访问和删除其个人数据的请求。 有关详细信息，请参见[Adobe Experience Platform Privacy Service](../../privacy-service/home.md)的概述。

## 退出功能

[!DNL Real-time CDP] 允许客户将选择退出其个人数据包含在细分用例中。客户的退出首选项由[!DNL Real-time Customer Profile]捕获并存储，可以通过在区段谓词中使用布尔逻辑(“AND NOT”)排除已退出区段的用户来实施。

有关详细信息，请参阅Adobe Experience Platform分段服务文档中的[支持退出请求](../../segmentation/honoring-opt-outs.md)的文档。

## IAB TCF 2.0支持

[!DNL Real-time CDP] 构建在Adobe Experience Platform上，是注册的供 [应](https://iabeurope.eu/vendor-list-tcf-v2-0/) 商列表 [!DNL Transparency & Consent Framework (TCF)]的一部分，如中所述 [!DNL Interactive Advertising Bureau (IAB)]。根据TCF 2.0要求，平台允许您收集详细的客户同意数据并将其集成到存储的客户用户档案中。 此同意数据随后可以纳入导出的用户档案段中是否包括某些受众，具体取决于其用例。

有关详细信息，请参见Experience Platform](../../landing/governance-privacy-security/consent/iab/overview.md)中有关[IAB TCF 2.0支持的概述。

## 后续步骤

本文档简要介绍了[!DNL Real-time CDP]的隐私功能。 请查看本指南中链接的文档，了解有关各项功能的更多信息。