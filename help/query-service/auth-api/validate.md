---
keywords: Experience Platform；安全；ip访问；验证；API指南；查询服务；IP验证
title: IP验证端点
description: 了解如何使用IP验证API端点验证查询服务中沙盒的IP访问权限。
role: Developer
source-git-commit: ad1b6d8449a2a3ca9c8422e70769d12e33d8e255
workflow-type: tm+mt
source-wordcount: '208'
ht-degree: 0%

---

# IP验证端点

使用IP验证API端点验证是否允许指定的IP地址访问查询服务中的指定沙盒。 此检查可确认访问限制是否适用，或是否允许IP地址访问沙盒中的数据。

## 验证IP以访问沙盒 {#validate-ip-for-sandbox-access}

使用IP验证端点检查是否允许给定IP地址访问指定沙盒的数据。 如果没有为沙盒配置IP限制，则默认情况下允许所有IP地址。 如果存在IP或CIDR限制，则此API验证指定的IP地址是否与任何配置的范围匹配。

>[!NOTE]
>
>您可以使用&#x200B;**用户令牌**&#x200B;或&#x200B;**服务令牌**&#x200B;访问此端点。 无需特定的角色要求。

**API格式**

```http
POST /security/validate/ip-access
```

**请求**

```shell
curl -X POST https://platform.adobe.io/data/foundation/query/security/validate/ip-access \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
       "ipAddress": "197.2.0.2"
     }'
```

**响应**

成功的响应会返回HTTP状态200，并显示一个布尔值，指示是否允许该IP。

>[!NOTE]
>
>如果允许提供的IP访问沙盒，响应中的`isAllowed`字段将返回`true`，否则返回`false`。 此API支持动态验证访问并确保沙盒环境的安全合规性。

```json
{
"isAllowed": true
}
```
