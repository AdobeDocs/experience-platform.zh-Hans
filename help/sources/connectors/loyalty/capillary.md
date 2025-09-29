---
title: 毛细管流事件概述
description: 了解如何将数据从Capillary流式传输到Experience Platform。
badge: Beta 版
exl-id: 3b8eb2f6-3b4a-4b91-89d4-b6d9027c6ab4
source-git-commit: bd5611b23740f16e41048f3bc65f62312593a075
workflow-type: tm+mt
source-wordcount: '295'
ht-degree: 4%

---

# [!DNL Capillary Streaming Events]

>[!AVAILABILITY]
>
>[!DNL Capillary Streaming Events]源为测试版。 有关使用测试版标记源的更多信息，请阅读源概述中的[条款和条件](../../home.md#terms-and-conditions)。

[!DNL Capillary Technologies]是一个领先的忠诚度和参与平台，受到全球300多个品牌的信任。 使用[!DNL Capillary Streaming Events]源使您的企业能够无缝地将[!DNL Capillary]中的客户个人资料、忠诚度数据和事务性事件流式传输到Adobe Experience Platform中。 连接您的[!DNL Capillary]源以启用实时个性化、高级受众分段和全渠道营销活动编排。

通过将[!DNL Capillary]与Experience Platform集成，您可以：

* 实时同步&#x200B;**会员积分、层级和奖励**。
* 将&#x200B;**事务性数据**&#x200B;发送到Experience Platform以进行分析和激活。
* 利用Real-Time CDP、Experience Platform和Adobe Journey Optimizer进行分段、历程编排和个性化。

## 先决条件

在将[!DNL Capillary]连接到Adobe Experience Platform之前，请确保您已：

* 有效的&#x200B;**Adobe组织ID**&#x200B;以及对已启用的Experience Platform沙盒的访问权限。
* **[!DNL Capillary]源凭据**（客户端ID和客户端密码）。
* 在Adobe Admin Console中创建源和数据流所需的权限。

### 收集所需的凭据

必须提供以下凭据的值，才能将您的[!DNL Capillary]帐户连接到Experience Platform：

| 凭据 | 描述 | 示例 |
| --- | --- | --- |
| 客户端 ID | [!DNL Capillary]源的客户端标识符。 | `321c8a8fee0d4a06838d46f9d3109e8a` |
| 客户端密码 | 与客户端ID一起颁发的客户端密钥 | `xxxxxxxxxxxxxxxxxx` |
| 组织 ID | 您的Adobe组织ID | `0A7D42FC5DB9D3360A495FD3@AdobeOrg` |

有关生成访问令牌的更多信息，请阅读[Adobe身份验证指南](https://developer.adobe.com/developer-console/docs/guides/authentication/)。

### 生成访问令牌

接下来，使用您的客户端ID和客户端密钥从Adobe生成访问令牌。

**请求**

```shell
curl -X POST 'https://ims-na1.adobelogin.com/ims/token' \
  -d 'client_id={CLIENT_ID}' \
  -d 'client_secret={CLIENT_SECRET}' \
  -d 'grant_type=client_credentials' \
  -d 'scope=openid AdobeID read_organizations additional_info.projectedProductContext session'
```

**响应**

```json
{
  "access_token": "eyJhbGciOi...",
  "token_type": "bearer",
  "expires_in": 86399994
}
```

## 后续步骤

完成[!DNL Capillary]的先决条件设置后，请阅读以下文档以了解如何连接帐户并开始将数据从[!DNL Capillary]流式传输到Experience Platform。

* [使用API连接 [!DNL Capillary Streaming Events] 到Experience Platform](../../tutorials/api/create/loyalty/capillary.md)
* [使用UI连接 [!DNL Capillary Streaming Events] 到Experience Platform](../../tutorials/ui/create/loyalty/capillary.md)
