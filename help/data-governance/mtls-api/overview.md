---
title: MTLS API指南
description: 了解如何使用mTLS服务API安全地检索和验证Adobe颁发的公共证书。
role: Developer
source-git-commit: f805d03ff2cd3a4f84ca8068023d83986f8bdfbb
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 1%

---

# MTLS服务API概述

使用MTLS服务API安全地检索Adobe为您的组织的应用程序颁发的公共证书。 此API可确保对客户与Adobe Experience Platform之间的数据交换进行身份验证和加密，从而提供额外的安全层。 通过从外部验证证书的真实性，您可以增强信任并保护敏感信息。

## 公共证书

公共证书是在安全通信中用于验证服务器或客户端身份的数字文档。 在mTLS服务API的上下文中，这些证书确保与Adobe Experience Platform的数据交换经过身份验证和加密。 通过API检索和验证这些证书可以确认它们的真实性，增强数据交易的安全性和可信度，并保护敏感信息。 要了解如何检索您的公共证书，请参阅[端点指南](./public-certificate-endpoint.md)以了解如何进行调用。

## 后续步骤

要开始使用MTLS服务API进行调用，请阅读[快速入门指南](./getting-started.md)以了解有关所需标头的重要信息，以及读取示例API调用等。
