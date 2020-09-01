---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 实时客户用户档案中的隐私请求处理
topic: overview
translation-type: tm+mt
source-git-commit: 397f08efa276f7885e099a0a8d9dc6d23fe0e8cc
workflow-type: tm+mt
source-wordcount: '603'
ht-degree: 0%

---


# 隐私请求处理 [!DNL Real-time Customer Profile]

Adobe Experience Platform [!DNL Privacy Service] 处理客户访问、选择退出出售或删除其个人数据的请求，这些请求由隐私法规(如一般数据保护规定(GDPR)和(CCPA)) [!DNL California Consumer Privacy Act] 规定。

本文档涵盖与处理隐私请求相关的基本概念 [!DNL Real-time Customer Profile]。

## 入门指南

在阅读本指南之前，建议您对以下服 [!DNL Experience Platform] 务有一定的了解：

* [[!DNLPrivacy Service]](home.md):管理跨Adobe Experience Cloud应用程序访问、选择退出销售或删除其个人数据的客户请求。
* [[!DNL标识服务]](../identity-service/home.md):通过跨设备和系统桥接身份，解决客户体验数据碎片化带来的根本挑战。
* [[!DNL实时客户用户档案]](../profile/home.md):基于来自多个来源的聚集数据提供统一、实时的消费者用户档案。

## 了解身份命名空间 {#namespaces}

Adobe Experience Platform [!DNL Identity Service] 将跨系统和设备的客户身份数据建立桥梁。 [!DNL Identity Service] 使用 **身份命名空间** ，通过将身份值与其来源系统相关联来提供与身份值相关的上下文。 命名空间可以表示一个通用概念，如电子邮件地址（“电子邮件”），或将标识与特定应用程序(如Adobe Advertising CloudID(“AdCloud”)或Adobe TargetID(“TNTID”))关联。

Identity Service维护全局定义（标准）和用户定义（自定义）标识命名空间的存储。 标准命名空间适用于所有组织（例如，“电子邮件”和“ECID”），而您的组织也可以创建自定义命名空间以满足其特定需求。

有关中的标识命名空间的详 [!DNL Experience Platform]细信息，请参 [阅标识命名空间概述](../identity-service/namespaces.md)。

## 提交请求 {#submit}

>[!NOTE]
>
>本节介绍如何为数据存储创建隐私 [!DNL Profile] 请求。 强烈建议您查看Privacy Service [API](../privacy-service/api/getting-started.md) 或 [](../privacy-service/ui/overview.md) Privacy ServiceUI文档，了解如何提交隐私作业的完整步骤，包括如何在请求负载中正确设置提交的用户标识数据的格式。

以下部分概述了如何提出隐私 [!DNL Real-time Customer Profile] 请求以 [!DNL Data Lake] 及如何 [!DNL Privacy Service] 使用API或UI。

### 使用API

在API中创建作业请求时，提 `userIDs` 供的任何作业请求都必须使用特 `namespace` 定 `type` 的，具体取决于它们所应用的数据存储。 商店的ID [!DNL Profile] 必须使用“标准”或“自定义”作 `type` 为其值，并使用有效的 [标识命名空间](#namespaces) (由 [!DNL Identity Service] 其值识别 `namespace` )。


此外，请求 `include` 有效负荷的数组必须包含请求所针对的不同数据存储的产品值。 向阵列发出请 [!DNL Data Lake]求时，阵列必须包含值“ProfileService”。

以下请求使用标准的“电子邮件”标 [!DNL Real-time Customer Profile]识命名空间为两者创建新的隐私工作。 它还包括阵列中 [!DNL Profile] 的产品 `include` 值：

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

在UI中创建作业请求时，请务必在“产 **[!UICONTROL 品”下选]** 择AEP **[!UICONTROL Data Lake和／或]** 用户档案 **[!UICONTROL ，以便分别]** 处理存储在或中的 [!DNL Data Lake][!DNL Real-time Customer Profile]数据的作业。

<img src="images/privacy/product-value.png" width="450"><br>

## 删除请求处理

当 [!DNL Experience Platform] 收到来自的删除请 [!DNL Privacy Service]求 [!DNL Platform] 时，会发送确认， [!DNL Privacy Service] 确认该请求已接收且受影响的数据已标记为删除。 然后在七天内从或 [!DNL Data Lake] 存储 [!DNL Profile] 中删除记录。 在这七天的窗口期内，数据会被软删除，因此任何服务都无法访问 [!DNL Platform] 它。

在以后的版本中， [!DNL Platform] 将在实际删除 [!DNL Privacy Service] 数据后向其发送确认信息。

## 后续步骤

通过阅读此文档，您了解了处理中的隐私请求所涉及的重要概念 [!DNL Experience Platform]。 建议您继续阅读本指南中提供的文档，以加深您对如何管理身份数据和创建隐私工作的理解。

有关处理未使用的资源的隐 [!DNL Platform] 私请求的信 [!DNL Profile]息，请参阅数据 [湖中的隐私请求处理文档](../catalog/privacy.md)。