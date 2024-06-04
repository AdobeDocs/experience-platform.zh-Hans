---
title: Real-Time CDP护栏
description: 了解Real-Time CDP各种服务和领域的数据保障。
feature: Guardrails, Data Management, Data Ingestion, Data Export
exl-id: 377499b4-5707-4d50-94e3-02f88ad5bf2c
source-git-commit: 5d6b70e397a252e037589c3200053ebcb7eb8291
workflow-type: tm+mt
source-wordcount: '392'
ht-degree: 1%

---

# Real-Time CDP护栏

护栏是阈值，可为数据和系统使用、性能优化以及避免Real-Time CDP中的错误或意外结果提供指导。 护栏可指您对与许可权利相关的数据和处理的使用或使用。

>[!IMPORTANT]
>
>检查您的销售订单中的许可证权利以及相应的 [产品描述](https://helpx.adobe.com/legal/product-descriptions.html) 实际使用限制以及此护栏页面。

从此处开始，访问下面的链接，了解Real-Time CDP各种服务和区域的所有防护：

* [数据摄取的护栏](/help/ingestion/guardrails.md)
* [的护栏 [!DNL Edge Network Server API]](/help/server-api/guardrails.md)
* [护栏 [!DNL Real-Time Customer Profile] 数据和分段](/help/profile/guardrails.md)
* [护栏 [!DNL Identity Service] 数据](/help/identity-service/guardrails.md)
* [护栏 [!DNL Query Service]](/help/query-service/guardrails.md)
* [通过目标激活数据的护栏](/help/destinations/guardrails.md)
* [Real-Time CDP B2B的护栏](/help/rtcdp/b2b-guardrails.md)

>[!TIP]
>
>此外，访问 [数字体验Blueprint](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/deployment/guardrails.html) 以了解更多信息，例如 [端到端延迟图](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/deployment/guardrails.html?lang=en#end-to-end-latency-diagrams) 用于各种Experience Platform服务。

## 护栏类型 {#guardrail-types}

请注意，跨越所有Real-Time CDP区域和服务的两种护栏类型是：

| 护栏类型 | 描述 |
|----------|---------|
| **性能护栏（软限制）** | 性能护栏是与用例范围相关的使用限制。 当超出性能护栏时，您可能会遇到性能下降和延迟问题。 Adobe不对此类性能下降负责。 始终超过性能护栏的客户可以选择许可额外的容量，以避免性能下降。 |
| **系统强制的护栏（硬限制）** | Real-Time CDP UI或API强制实施系统强制的护栏。 这些限制不得超过，因为UI和API将阻止您这样做或您会返回错误。 |

{style="table-layout:auto"}

## Real-Time CDP许可和授权信息 {#product-descriptions}

此外，请参阅下面的产品描述链接，以了解基于您购买的Real-Time CDP版本和层的许可和授权信息：

* [所有Adobe产品描述](https://helpx.adobe.com/legal/product-descriptions.html)
* [Real-time Customer Data Platform （B2C版本 — Prime和Ultimate包）](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2c-edition-prime-and-ultimate-packages.html)
* [Real-time Customer Data Platform （B2P版本 — Prime和Ultimate包）](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2p-edition-prime-and-ultimate-packages.html)
* [Real-time Customer Data Platform （B2B版本 — Prime和Ultimate包）](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html)

## 用于其他Experience Platform应用的护栏  {#guardrails-other-aep-apps}

对于其他Experience Platform应用也存在类似的护栏。 有关详细信息，请访问下面的链接：

* [Adobe Journey Optimizer护栏](https://experienceleague.adobe.com/docs/journey-optimizer/using/get-started/guardrails.html?lang=en)
* [Customer Journey Analytics护栏](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-admin/guardrails.html)

## 后续步骤

了解了适用于Real-Time CDP各个区域和服务的护栏后，您可以遵循这些护栏 [Real-Time CDP实施的示例用例](/help/rtcdp/get-started.md).
