---
title: XDM中的敏感和个人信息
description: 了解有关Experience Data Model(XDM)中敏感个人信息(SPI)和个人身份信息(PII)的关键注意事项。
source-git-commit: 76815389a1c87fbf908e499c50594a4b356a11a9
workflow-type: tm+mt
source-wordcount: '526'
ht-degree: 0%

---

# XDM中的敏感和个人信息

体验数据模型(XDM)提供了可在Adobe Experience Platform中使用的标准数据结构，允许您收集有关客户体验的数据。 此数据可以包括敏感个人信息(SPI)和个人身份信息(PII)，如客户的电子邮件地址、名称、帐户ID和其他数据字段。

组织规则和法律隐私法规(如《通用数据保护条例》(GDPR))对如何收集、存储、使用和共享SPI和PII实施了限制。 因此，务必要考虑哪些字段表示数据模型中的敏感或个人信息，并确保您的操作符合组织和法律准则。

本文档介绍了有关XDM中敏感和个人数据的主要注意事项。

## 确定哪些字段包含敏感或个人数据

构成SPI和PII的内容非常特定于上下文，因此，您需要了解数据模型、业务运营和适用的法规，以确定哪些架构字段表示敏感或个人数据。

例如，客户的法律管辖范围会直接影响哪些信息被视为敏感信息。 GDPR为SPI和PII提供了强大的定义，但欧洲经济区(EEA)以外的客户可能会受到不同的定义和限制。

## 处理敏感和个人数据

与敏感和个人数据本身的定义类似，处理此数据的限制也特定于上下文。

客户同意通常是收集和处理哪些数据以及用于什么目的的关键因素。 根据您的客户所在的法律管辖区，可能需要明确同意才能收集其敏感和个人数据。 即使不需要明确同意，数据处理限制仍会适用，具体取决于隐私声明对客户说的内容。

请咨询您的法律团队，以确定应针对您的业务用例处理多敏感和个人数据。

## 限制使用敏感和个人数据

XDM提供了各种标准字段组和数据类型，用于描述相关的常用数据结构，以提升客户体验。 但是，如果推荐的标准资源包含您不希望包含在架构中的受限字段，则不必使用该资源。

平台允许您定义自己的自定义字段组和数据类型，如果任何可用的标准资源无法满足您的需求，则可让您完全控制数据的结构方式。 有关如何定义这些自定义资源的更多信息，请参阅以下文档：

* [创建自定义字段组](../ui/resources/field-groups.md#create)
* [创建自定义数据类型](../ui/resources/data-types.md#create)

<!-- (To include once features are available)
* Marking fields as sensitive
* Remove fields from standard field groups pre-ingestion
* Deprecate fields post-ingestion
-->

## 后续步骤

本文档介绍了有关XDM中敏感和个人数据的主要注意事项。 有关如何为模式建模以最好地满足业务用例的更多信息，请参阅 [数据建模最佳实践](./best-practices.md).

有关Experience Platform中的数据管理和隐私功能的更多信息，请参阅 [管理、隐私和安全](../../landing/governance-privacy-security/overview.md).
