---
title: 在Reactor API中共享专用扩展包
description: 了解如何授权其他企业在Reactor API中共享私有扩展包。
exl-id: 3300a630-6d22-46e1-8b1b-b5d12a3ea44c
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '503'
ht-degree: 2%

---

# 共享专用扩展包

>[!NOTE]
>
>在扩展包所有者组织中具有`develop_extensions`权限的用户能够创建、列出和删除该扩展包的扩展包使用授权。 授权组织中具有`manage_properties`权限的用户只能列出其组织的扩展包使用授权，并且如果想要使用该扩展包，则将其状态更新为`accepted`；如果不想使用，则更新为`rejected`。

扩展包的所有者可以授予其他公司通过Reactor API使用其私有版本的权限。 一个扩展包的使用许可证被授予每个已批准的业务，此授权适用于该包的所有当前和未来专用版本。

本指南提供了有关如何配置扩展包使用授权的高级概述。 有关如何管理Reactor API中的授权的更多详细指导，包括授权结构的示例JSON，请参阅[扩展包使用授权端点指南](../endpoints/extension-package-usage-authorizations.md)。

## 创建授权 {#create-authorization}

要创建新授权，您必须具有`develop_extensions`权限。 以下示例演示了如何使用要授权的公司的`authorized_org_id`为扩展包创建扩展包使用授权。

**API格式**

```http
POST /extension_packages/{EXTENSION_PACKAGE_ID}/extension_package_usage_authorizations
```

| 参数 | 描述 |
| --- | --- |
| `EXTENSION_PACKAGE_ID` | 要为其创建授权的扩展包的`ID`。 |

{style="table-layout:auto"}

**请求**

以下请求为指定的公司创建新的扩展包授权。

```shell
curl -X POST \
  https://reactor.adobe.io/extension_packages/{EXTENSION_PACKAGE_ID}/extension_package_usage_authorizations \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -d '{
        "data": {
          "attributes": {
            "authorized_org_id": "{ORG_ID}"
          },
          "type": "extension_package_usage_authorizations"
        }
      } 
```

| 属性 | 描述 |
| --- | --- |
| `attributes.authorized_org_id` | 要授权的组织的`ID`。 |

{style="table-layout:auto"}

授权的初始状态处于`pending_approval`阶段。 在使用扩展包之前，公司必须批准授权。 公司用户可以在授权未决批准时浏览私有扩展包，但他们无法安装该包，并且无法在扩展目录中找到它。

## 批准授权 {#approve-authorization}

要批准授权，您必须具有`manage_properties`权限。 作为授权公司，您需要向扩展包使用授权发送PATCH请求，包括授权的`ID`，并将状态设置为`approved`。

**API格式**

```http
PATCH //extension_package_usage_authorizations/{EXTENSION_PACKAGE_USAGE_AUTHORIZATION_ID}
```

| 参数 | 描述 |
| --- | --- |
| `EXTENSION_PACKAGE_USAGE_AUTHORIZATION_ID` | 要批准的授权的`ID`。 |

{style="table-layout:auto"}

**请求**

以下PATCH请求将授权的`state`设置为`approved`。

```shell
curl -X PATCH \
  https://reactor.adobe.io/extension_package_usage_authorizations/{EXTENSION_PACKAGE_USAGE_AUTHORIZATION_ID} \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-Api-Key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -d '{
        "data": {
          "attributes": {
            "state": "approved"
            },
            "id": ":extension_package_usage_authorization_id",
            "type": "extension_package_usage_authorizations"
        }
      }
```

授权获得批准后，作为授权的公司，您现在可以在资产上安装扩展包。

>[!NOTE]
>
>如果授权被拒绝，则被授权的公司将无法使用扩展包。

## 删除授权 {#delete-authorization}

作为扩展包的所有者，您可以随时通过删除扩展包使用授权来撤销授权。 这将阻止授权的公司查看目录中的扩展包的私有版本并在其属性上安装该扩展包。 但是，在删除后，已安装的专用版本将继续按预期工作。

**API格式**

```http
DELETE //extension_package_usage_authorizations/{EXTENSION_PACKAGE_USAGE_AUTHORIZATION_ID}
```

| 参数 | 描述 |
| --- | --- |
| `EXTENSION_PACKAGE_USAGE_AUTHORIZATION_ID` | 要删除的授权的`ID`。 |

{style="table-layout:auto"}

**请求**

以下DELETE请求删除公司的授权特权。

```shell
curl -X DELETE \
  https://reactor.adobe.io/extension_package_usage_authorizations/{EXTENSION_PACKAGE_USAGE_AUTHORIZATION_ID} \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-Api-Key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
```
