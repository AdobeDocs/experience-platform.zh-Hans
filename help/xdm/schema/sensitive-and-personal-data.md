---
title: XDM中的敏感信息和个人信息
description: 了解与Experience Data Model (XDM)中的敏感个人信息(SPI)和个人身份信息(PII)相关的关键注意事项。
exl-id: 92a8b6ad-3c45-4772-8178-60f857ab13e2
source-git-commit: 9785b252b7c9cb3513858476753b6b4f71277ed7
workflow-type: tm+mt
source-wordcount: '526'
ht-degree: 0%

---

# XDM中的敏感信息和个人信息

Experience Data Model (XDM)提供在Adobe Experience Platform中使用的标准数据结构，允许您收集有关客户体验的数据。 此数据可以包括敏感的个人信息(SPI)和个人身份信息(PII)，例如客户的电子邮件地址、姓名、帐户ID和其他数据字段。

《通用数据保护条例》(GDPR)等组织规则和法律隐私法规对SPI和PII的收集、存储、使用和共享方式施加了限制。 因此，请务必考虑哪些字段代表数据模型中的敏感信息或个人信息，并确保您的操作符合组织和法律准则。

本文档介绍了XDM中有关敏感数据和个人数据的重要注意事项。

## 确定哪些字段包含敏感数据或个人数据

构成SPI和PII的内容与上下文密切相关，因此，您可以自行了解数据模型、业务运营和适用的法规，以确定哪些架构字段表示敏感数据或个人数据。

例如，客户的法律管辖范围直接影响到哪些信息被视为敏感信息。 GDPR为SPI和PII提供了可靠的定义，但欧洲经济区(EEA)以外的客户可能会受到不同的定义和限制。

## 处理敏感数据和个人数据

与敏感数据和个人数据本身的定义类似，处理此数据的限制也是特定于上下文的。

就能够收集和处理哪些数据以及出于什么目的而言，客户同意通常是关键因素。 根据客户所处的法律管辖范围，可能需要获得明确同意才能收集其敏感数据和个人数据。 即使不需要明确同意，数据处理限制仍然适用，具体取决于隐私通知向客户声明的内容。

请咨询您的法律团队，以确定为您的业务用例处理敏感数据和个人数据的方式。

## 限制使用敏感数据和个人数据

XDM提供了各种标准字段组和数据类型，用于描述提供客户体验的相关常用数据结构。 但是，如果推荐的标准资源包含您不希望包含在架构中的受限字段，则无需使用该资源。

Platform允许您定义自己的自定义字段组和数据类型，从而让您能够在任何可用的标准资源无法满足您的需求时，完全控制数据的结构方式。 有关如何定义这些自定义资源的更多信息，请参阅以下文档：

* [创建自定义字段组](../ui/resources/field-groups.md#create)
* [创建自定义数据类型](../ui/resources/data-types.md#create)

<!-- (To include once features are available)
* Marking fields as sensitive
* Remove fields from standard field groups pre-ingestion
* Deprecate fields post-ingestion
-->

## 后续步骤

本文档介绍了有关XDM中的敏感数据和个人数据的主要注意事项。 有关如何对架构进行建模以最佳地满足您的业务用例的更多信息，请参阅以下指南： [数据建模的最佳实践](./best-practices.md).

有关Experience Platform中的数据治理和隐私功能的更多信息，请参阅以下内容的概述： [治理、隐私和安全](../../landing/governance-privacy-security/overview.md).
