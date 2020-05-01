---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 实时客户用户档案中的隐私请求处理
topic: overview
translation-type: tm+mt
source-git-commit: cc296670db91640e75fd7a47b874a46eaf57ecde

---


# 实时客户用户档案中的隐私请求处理

Adobe Experience Platform Privacy Service处理客户访问、选择退出出售或删除其个人数据的请求，这些请求由隐私法规(如一般数据保护规定(GDPR)和加利福尼亚消费者隐私法(CCPA))规定。

此文档涵盖与处理实时客户用户档案的隐私请求相关的基本概念。

## 入门指南

在阅读本指南之前，建议您对以下Experience Platform服务有一定的了解：

* [隐私服务](home.md): 管理客户在Adobe Experience Cloud应用程序中访问、选择退出销售或删除其个人数据的请求。
* [身份服务](../identity-service/home.md): 通过跨设备和系统桥接身份，解决客户体验数据碎片化带来的根本挑战。
* [实时客户用户档案](../profile/home.md): 基于来自多个来源的聚集数据提供统一、实时的消费者用户档案。

## 了解身份命名空间 {#namespaces}

Adobe Experience Platform Identity Service跨系统和设备连接客户身份数据。 身份服务 **使用身份命名空间** ，通过将身份值与其来源系统相关联来提供与身份值相关的上下文。 命名空间可以表示一个通用概念，如电子邮件地址（“电子邮件”），或将标识与特定应用程序(如Adobe Advertising Cloud ID(“AdCloud”)或Adobe目标ID(“TNTID”))关联。

Identity Service维护全局定义（标准）和用户定义（自定义）标识命名空间的存储。 标准命名空间适用于所有组织（例如，“电子邮件”和“ECID”），而您的组织也可以创建自定义命名空间以满足其特定需求。

有关Experience Platform中身份命名空间的更多信息，请参阅 [身份命名空间概述](../identity-service/namespaces.md)。

## 提交请求 {#submit}

>[!NOTE] 本节介绍如何为用户档案数据存储创建隐私请求。 强烈建议您查看Privacy Service API [或Privacy](../privacy-service/api/getting-started.md) Service UI [](../privacy-service/ui/overview.md) 文档，了解如何提交隐私作业的完整步骤，包括如何在请求负载中正确设置提交的用户身份数据的格式。

以下部分概述了如何使用隐私服务API或UI对实时客户用户档案和数据湖提出隐私请求。

### 使用API

在API中创建作业请求时，提 `userIDs` 供的任何作业请求都必须使用特 `namespace` 定 `type` 的，具体取决于它们所应用的数据存储。 用户档案商店的ID必须使用“标准”或“自定义”作为 `type` 其值，而Identity Service必须 [为其值](#namespaces) 识别有 `namespace` 效的标识命名空间。


此外，请求 `include` 有效负荷的数组必须包含请求所针对的不同数据存储的产品值。 向数据湖发出请求时，阵列必须包含值“ProfileService”。

以下请求使用标准“电子邮件”身份用户档案为实时客户命名空间创建新的隐私工作。 它还包括阵列中用户档案的产品 `include` 价值：

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

在UI中创建作业请求时，请务必在 **产品下选择** AEP Data Lake和／或 **用户档案**__ ，以便分别处理存储在“数据湖”或“实时客户”用户档案中的数据的作业。

<img src="images/privacy/product-value.png" width="450"><br>

## 删除请求处理

当Experience Platform从隐私服务收到删除请求时，平台会向隐私服务发送确认消息，确认该请求已收到且受影响的数据已标记为删除。 然后在七天内从数据湖或用户档案库中删除记录。 在这七天的时间内，数据会被软删除，因此任何平台服务都无法访问。

在将来的版本中，平台将在数据被物理删除后向隐私服务发送确认信息。

## 后续步骤

阅读此文档，您便了解了在Experience Platform中处理隐私请求的重要概念。 建议您继续阅读本指南中提供的文档，以加深您对如何管理身份数据和创建隐私工作的理解。

有关处理用户档案未使用的平台资源的隐私请求的信息，请参阅数据 [湖中的隐私请求处理文档](../catalog/privacy.md)。