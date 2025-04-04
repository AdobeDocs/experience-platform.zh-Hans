---
title: 数据Distiller授权API指南
description: 了解如何使用Data Distiller Authorization API对通过SQL的安全连接实施基于网络的IP限制。 使用此API可增强对Adobe Experience Platform数据的数据访问控制。
role: Developer
exl-id: bcc5ea0e-cb6d-4c7b-bf9f-a0336f76c4c8
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '425'
ht-degree: 2%

---

# 数据Distiller授权API指南

>[!AVAILABILITY]
>
>此功能适用于购买了Data Distiller附加产品的客户。 有关更多信息，请与您的 Adobe 代表联系。

使用数据Distiller授权API强制执行基于IP的限制。 应用这些措施可以确保只有获得批准的网络和客户端计算机才能通过Adobe Experience Platform中的SQL访问数据。 这些控制可帮助您满足严格的安全标准，同时提供实时访问监控和警报。

利用此API，您可以配置、强制执行并监视通过SQL接口访问数据的IP限制。 本文档全面概述了API的核心功能、端点功能和未来功能。

## 主要功能

通过下列功能，您可以定义基于IP的访问限制、监视访问尝试以及自定义查询服务的网络安全设置：

- **定义基于网络的数据访问控制**：为查询服务访问指定允许的IP范围。 此限制特别适用于SQL数据库连接，包括通过Business Intelligence (BI)工具、数据库客户端或编程接口（如JDBC）建立的连接。
- **启用全面监视和警报**：所有访问尝试（包括被拒绝的连接）都将被记录并发送到[Adobe Experience Platform审核日志](../../landing/governance-privacy-security/audit-logs/overview.md)以进行实时跟踪。 使用此功能可监控访问模式并检测潜在的安全漏洞。
- **配置灵活的IP限制**：以单个IP和CIDR块格式指定允许的IP。 这些设置适用于每个沙盒，允许您根据特定安全需求定制网络限制。

## 审计和监测能力

为了支持安全的数据访问实践，查询服务会记录所有访问或尝试访问Experience Platform的客户端IP。 审核事件（包括被拒绝的连接）将发送到Experience Platform审核日志。 这可以启用：

- **实时监控**：跟踪基于IP的访问模式以确保法规遵从性。
- **未授权访问警报**：识别来自未授权IP的访问尝试并做出响应。

有关详细信息，请参阅[审核日志概述](../../landing/governance-privacy-security/audit-logs/overview.md)。

## 后续步骤

通过查看[入门指南](./getting-started.md)开始使用数据Distiller授权API，以了解必要的设置步骤，包括所需的标头和API调用约定。 然后，探索特定于端点的[IP访问](./ip-access.md)和[IP验证](./validate.md)指南，以配置和管理安全数据访问。

请参阅[Data Distiller Authorization OpenAPI参考文档](https://developer.adobe.com/experience-platform-apis/references/data-distiller-auth/)，查看易于集成、测试和探索的机器可读的标准化格式。

有关每个返回的数据集的各种响应参数的信息，请参阅[数据集API开发人员文档](https://developer.adobe.com/experience-platform-apis/references/catalog/#tag/Datasets/operation/listDatasets)。
