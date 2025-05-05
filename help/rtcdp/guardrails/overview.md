---
title: Real-Time CDP护栏
description: 了解Real-Time CDP各种服务和领域的数据保障。
feature: Guardrails, Data Management, Data Ingestion, Data Export
exl-id: 377499b4-5707-4d50-94e3-02f88ad5bf2c
source-git-commit: 7f3459f678c74ead1d733304702309522dd0018b
workflow-type: tm+mt
source-wordcount: '393'
ht-degree: 1%

---

# Real-Time CDP护栏

护栏是阈值，可为数据和系统使用、性能优化以及避免Real-Time CDP中的错误或意外结果提供指导。 护栏可指您对与许可权利相关的数据和处理的使用或使用。

>[!IMPORTANT]
>
>除了此护栏页面外，还检查销售订单中的许可证授权和相应的[产品描述](https://helpx.adobe.com/cn/legal/product-descriptions.html)中的实际使用限制。

从此处开始，访问下面的链接，了解Real-Time CDP各种服务和区域的所有防护：

* [数据摄取的护栏](/help/ingestion/guardrails.md)
* [!DNL Edge Network API][&#128279;](https://developer.adobe.com/data-collection-apis/docs/getting-started/guardrails/)的护栏
* [ [!DNL Real-Time Customer Profile] 数据和分段的护栏](/help/profile/guardrails.md)
* [ [!DNL Identity Service] 数据的护栏](/help/identity-service/guardrails.md)
* [ [!DNL Query Service]的护栏](/help/query-service/guardrails.md)
* [通过目标激活数据的护栏](/help/destinations/guardrails.md)
* [Real-Time CDP B2B的护栏](/help/rtcdp/b2b-guardrails.md)

>[!TIP]
>
>此外，请访问[数字体验Blueprint](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/deployment/guardrails.html?lang=zh-Hans)以了解详细信息，如各种Experience Platform服务的[端到端延迟图](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/deployment/guardrails.html?lang=zh-Hans#end-to-end-latency-diagrams)。

## 护栏类型 {#guardrail-types}

请注意，跨越所有Real-Time CDP区域和服务的两种护栏类型是：

| 护栏类型 | 描述 |
|----------|---------|
| **性能护栏（软限制）** | 性能护栏是与用例范围相关的使用限制。 当超出性能护栏时，您可能会遇到性能下降和延迟问题。 Adobe不对此类性能下降负责。 始终超过性能护栏的客户可以选择许可额外的容量，以避免性能下降。 |
| **系统强制的护栏（硬限制）** | Real-Time CDP UI或API强制实施系统强制的护栏。 这些限制不得超过，因为UI和API将阻止您这样做或您会返回错误。 |

{style="table-layout:auto"}

## Real-Time CDP许可和授权信息 {#product-descriptions}

此外，请参阅下面的产品描述链接，以了解基于您购买的Real-Time CDP版本和层的许可和授权信息：

* [所有Adobe产品描述](https://helpx.adobe.com/cn/legal/product-descriptions.html)
* [Real-Time Customer Data Platform (B2C版本 — Prime和Ultimate包)](https://helpx.adobe.com/cn/legal/product-descriptions/real-time-customer-data-platform-b2c-edition-prime-and-ultimate-packages.html)
* [Real-Time Customer Data Platform (B2P版本 — Prime和Ultimate包)](https://helpx.adobe.com/cn/legal/product-descriptions/real-time-customer-data-platform-b2p-edition-prime-and-ultimate-packages.html)
* [Real-Time Customer Data Platform (B2B edition - Prime和Ultimate包)](https://helpx.adobe.com/cn/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html)

## 其他Experience Platform应用程序的护栏  {#guardrails-other-aep-apps}

其他Experience Platform应用程序也存在类似的护栏。 有关详细信息，请访问下面的链接：

* [Adobe Journey Optimizer护栏](https://experienceleague.adobe.com/docs/journey-optimizer/using/get-started/guardrails.html?lang=zh-Hans)
* [Customer Journey Analytics护栏](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-admin/guardrails.html?lang=zh-Hans)

## 后续步骤

在了解了适用于Real-Time CDP各个区域和服务的护栏后，您可以遵循该护栏并查看一个[Real-Time CDP实施示例用例](/help/rtcdp/get-started.md)。
