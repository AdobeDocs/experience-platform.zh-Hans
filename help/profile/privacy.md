---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 实时客户用户档案中的隐私请求处理
topic: overview
translation-type: tm+mt
source-git-commit: 5f0e0deb4a2fae636ac4d2313a6541c25309c294

---


# 实时客户用户档案中的隐私请求处理

Adobe Experience Platform Privacy Service处理客户访问、销售或删除其个人数据的请求，这些请求由隐私法规(如《一般数据保护条例》(GDPR)和《加利福尼亚消费者隐私法》(CCPA))规定。

本文档涵盖与处理实时客户用户档案的隐私请求相关的基本概念。

## 入门指南

在阅读本指南之前，建议您对以下Experience Platform服务有充分的了解：

* [隐私服务](home.md):管理客户跨Adobe Experience Cloud应用程序访问、选择退出销售或删除其个人数据的请求。
* [标识服务](../identity-service/home.md):通过跨设备和系统桥接身份，解决客户体验数据碎片化带来的根本挑战。
* [实时客户用户档案](../profile/home.md):根据来自多个来源的汇总数据提供统一、实时的消费者用户档案。

## 了解身份命名空间 {#namespaces}

Adobe Experience Platform Identity Service跨系统和设备连接客户标识数据。 身份服务使 **用身份命名空间** ，通过将身份值与其来源系统相关联来提供与身份值相关的上下文。 命名空间可以表示通用概念，如电子邮件地址（“电子邮件”），或将标识与特定应用程序(如Adobe Advertising Cloud ID(“AdCloud”)或Adobe目标ID(“TNTID”))关联。

Identity Service维护全局定义（标准）和用户定义（自定义）标识命名空间的存储。 标准命名空间适用于所有组织（例如，“电子邮件”和“ECID”），而您的组织也可以创建自定义命名空间以满足其特定需求。

有关Experience Platform中标识命名空间的更多信息，请参阅标识 [命名空间概述](../identity-service/namespaces.md)。

## 提交请求 {#submit}

>[!NOTE] 本节介绍如何设置数据湖的隐私请求的格式。 强烈建议您查看 [Privacy Service API](../privacy-service/api/getting-started.md) 或 [Privacy Service UI](../privacy-service/ui/overview.md) 文档，了解有关如何提交隐私作业的完整步骤，包括如何在请求负载中正确设置提交的用户标识数据的格式。

以下部分概述了如何使用隐私服务API或UI向实时客户用户档案和数据湖提出隐私请求。

### 使用API

在API中创建作业请求时，提供的任 `userIDs` 何作业请求都必须使用特定的，并 `namespace` 且 `type` 取决于它们所应用的数据存储。 用户档案商店的ID必须使用“标准”或“自定义”作为其值， `type` 而标识服务必须为 [其值识别有效的标识](#namespaces)`namespace` 命名空间。


此外，请求 `include` 有效负荷的数组必须包括请求所针对的不同数据存储的产品值。 向数据湖发出请求时，阵列必须包含值“ProfileService”。

以下请求使用标准的“电子邮件”标识用户档案为实时客户命名空间创建新的隐私工作。 它还包括阵列中用户档案的产品 `include` 值：

```shell
curl -X POST \
  https://platform.adobe.io/data/core/privacy/jobs \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -d '{
    "companyContexts": [
      {
        "namespace": "imsOrgID",
        "value": "{IMS_ORG}"
      }
    ],
    "users": [
      {
        "key": "user12345",
        "action": ["access","delete"],
        "userIDs": [
          {
            "namespace": "Email",
            "value": "ajones@acme.com",
            "type": "standard"
          },
          {
            "namespace": "email_label",
            "value": "ajones@acme.com",
            "type": "unregistered"
          }
        ]
      }
    ],
    "include": ["ProfileService", "aepDataLake"],
    "expandIds": false,
    "priority": "normal",
    "analyticsDeleteMethod": "anonymize",
    "regulation": "ccpa"
}'
```

### 使用UI

在UI中创建作业请求时，请务必在 **Products下选择** AEP Data Lake **and/or**__ 用户档案，以便分别处理数据湖或实时客户用户档案中存储的数据的作业。

<img src="images/privacy/product-value.png" width="450"><br>

## 删除请求处理

当Experience Platform从隐私服务收到删除请求时，平台会向隐私服务发送确认消息，确认该请求已收到且受影响的数据已被标记为删除。 然后，在七天内从数据湖或用户档案商店中删除记录。 在该七天的窗口期内，数据会被软删除，因此任何平台服务都无法访问。

在将来的版本中，平台将在数据实际删除后向隐私服务发送确认。

## 后续步骤

阅读本文档，您便了解了在Experience Platform中处理隐私请求时涉及的重要概念。 建议您继续阅读本指南中提供的文档，以加深您对如何管理身份数据和创建隐私工作的理解。

有关处理非用户档案使用的平台资源的隐私请求的信息，请参阅数据湖 [中的隐私请求处理文档](../catalog/privacy.md)。