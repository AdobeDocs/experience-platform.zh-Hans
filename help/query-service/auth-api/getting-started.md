---
keywords: Experience Platform；查询服务；IP访问控制；授权；API；入门
title: 数据Distiller授权API指南
description: 了解如何开始使用Adobe Experience Platform查询服务中的授权和IP范围限制来确保数据访问安全。
role: Developer
exl-id: d93ce774-c8b2-4f15-a4d9-117d9aa5d9e7
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '510'
ht-degree: 5%

---

# 数据Distiller授权API入门

>[!AVAILABILITY]
>
>此功能适用于购买了Data Distiller附加产品的客户。 有关更多信息，请与您的 Adobe 代表联系。

Data Distiller Authorization API通过Adobe Experience Platform中的SQL接口，使组织能够更严格地控制数据访问。 您可以使用此API定义IP限制、限制对指定网络的数据访问以及增强安全监控。

本指南概述如何设置调用数据Distiller授权API所需的授权凭据和权限。

## 快速入门 {#getting-started}

以下部分提供了有关准备所需的授权值和首次请求数据Distiller授权API的信息。

### 所需的权限 {#required-permissions}

要在查询服务中启用安全数据访问限制，您需要&#x200B;**[!UICONTROL 管理允许列表]**&#x200B;权限。 此权限允许组织定义有权通过SQL界面访问Experience Platform中数据的特定IP范围（IPv4或IPv6格式）。 访问在沙盒级别进行管理，用户可以配置一个已批准IP地址或CIDR块的列表，将访问限制为仅访问允许的网络。

>[!NOTE]
>
>系统管理员可以从Adobe [Admin Console](https://adminconsole.adobe.com/)设置用户权限。 有关详细信息，请参阅 [Admin Console 用户指南](https://helpx.adobe.com/enterprise/using/admin-console.html)。

以下功能具有&#x200B;**[!UICONTROL 管理允许列表]**&#x200B;权限：

- **定义允许的IP范围**：只有这些定义范围中的IP地址或CIDR块才能使用SQL通过查询服务访问Experience Platform中的数据。
- **强制IP范围检查**：来自允许范围以外的IP的连接被拒绝。
- **审核和警报功能**：所有访问尝试（包括被拒绝的连接）都记录为审核事件。 这些事件在[Adobe Experience Platform审核日志](../../landing/governance-privacy-security/audit-logs/overview.md)中提供，用于监视潜在的安全漏洞。

### 收集所需标头的值 {#gather-values-for-required-headers}

要调用Data Distiller Authorization API，您必须完成[Experience Platform API身份验证教程](../../landing/api-authentication.md)，该教程提供了API调用中所需标头的值。 在每个请求中包含以下标头：

- **授权**： `Bearer {ACCESS_TOKEN}`
- **x-api-key**： `{API_KEY}`
- **x-gw-ims-org-id**： `{ORG_ID}`
- **x-sandbox-name**： `{SANDBOX_NAME}`

>[!NOTE]
>
> 有关沙盒的详细信息，请参阅[沙盒概述文档](../../sandboxes/home.md)。

包含有效负载(POST、PUT、PATCH)的所有请求也需要此标头：

- **内容类型**： `application/json`

### 后续步骤

收集了所需的权限和标头值后，您就可以开始为查询服务配置IP限制了。 请继续查看端点文档，以获取CRUD操作的详细示例，包括：

- API格式和示例请求/响应对。
- 每个工序的题头、有效负荷和响应代码。

每个API调用示例都演示了如何设置请求格式和解读响应，从而帮助您在查询服务中强制实施对数据的安全访问。

有关配置和验证IP限制的特定说明，请参阅[IP访问端点文档](./ip-access.md)和[IP验证端点文档](./validate.md)。

请参阅[Data Distiller Authorization OpenAPI参考文档](https://developer.adobe.com/experience-platform-apis/references/data-distiller-auth/)，查看易于集成、测试和探索的机器可读的标准化格式。
