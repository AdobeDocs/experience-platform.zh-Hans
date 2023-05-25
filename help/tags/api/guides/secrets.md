---
title: Reactor API中的密钥
description: 了解如何在Reactor API中配置用于事件转发的密码的基础知识。
exl-id: 0298c0cd-9fba-4b54-86db-5d2d8f9ade54
source-git-commit: 88939d674c0002590939004e0235d3da8b072118
workflow-type: tm+mt
source-wordcount: '1232'
ht-degree: 1%

---

# Reactor API中的密钥

在Reactor API中，密码是表示身份验证凭据的资源。 在事件转发中使用密钥，以向另一个系统验证以进行安全数据交换。 因此，只能在事件转发属性（具有以下属性的属性）中创建密钥 `platform` 属性设置为 `edge`)。

目前有三种受支持的密钥类型表示在 `type_of` 属性：

| 密码类型 | 描述 |
| --- | --- |
| `token` | 表示两个系统都已知和理解的身份验证令牌值的单个字符串。 |
| `simple-http` | 包含用户名和密码的两个字符串属性。 |
| `oauth2-client_credentials` | 包含多个属性以支持 [OAuth](https://datatracker.ietf.org/doc/html/rfc6749) 身份验证规范。 事件转发会要求您提供所需信息，然后在指定的时间间隔内为您处理这些令牌的续订。 |

{style="table-layout:auto"}

本指南提供了有关如何配置用于事件转发的密码的高级概述。 有关如何在Reactor API中管理机密的详细指导，包括机密结构的JSON示例，请参阅 [密钥端点指南](../endpoints/secrets.md).

## 凭据

每个密码都包含 `credentials` 保存其相应凭据值的属性。 时间 [在API中创建密钥](../endpoints/secrets.md#create)，每种类型的密码具有不同的必需属性，如以下部分所示：

* [`令牌`](#token)
* [&#39;simple-http&#39;](#simple-http)
* [&#39;oauth2-client_credentials&#39;](#oauth2-client_credentials)
* [&#39;oauth2-google&#39;](#oauth2-google)

### `token` {#token}

带有的密钥 `type_of` 值 `token` 仅要求下的单个属性 `credentials`：

| 凭据属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `token` | 字符串 | 目标系统可识别的机密令牌。 |

{style="table-layout:auto"}

令牌存储为静态值，因此密码的 `expires_at` 和 `refresh_at` 属性设置为 `null` 创建密码时。

### `simple-http` {#simple-http}

带有的密钥 `type_of` 值 `simple-http` 需要以下属性 `credentials`：

| 凭据属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `username` | 字符串 | 用户名。 |
| `password` | 字符串 | 密码。 API响应中不包含此值。 |

{style="table-layout:auto"}

当创建密钥时，两个属性会使用BASE64编码进行交换 `username:password`. 交易结束后，秘密是 `expires_at` 和 `refresh_at` 属性设置为 `null`.

### `oauth2-client_credentials` {#oauth2-client_credentials}

带有的密钥 `type_of` 值 `oauth2-client_credentials` 需要以下属性 `credentials`：

| 凭据属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `client_id` | 字符串 | Oauth集成的客户端ID。 |
| `client_secret` | 字符串 | OAuth集成的客户端密钥。 API响应中不包含此值。 |
| `token_url` | 字符串 | Oauth集成的授权URL。 |
| `refresh_offset` | 整数 | *（可选）* 刷新操作偏移的值（以秒为单位）。 如果在创建密钥时省略此属性，则值将设置为 `14400` （4小时）默认情况。 |
| `options` | 对象 | *（可选）* 指定OAuth集成的其他选项：<ul><li>`scope`：表示 [OAuth 2.0范围](https://oauth.net/2/scope/) 用于凭据。</li><li>`audience`：一个字符串，表示 [Auth0访问令牌](https://auth0.com/docs/protocols/protocol-oauth2).</li></ul> |

当 `oauth2-client_credentials` 密码已创建或更新， `client_id` 和 `client_secret` (可能会 `options`)在POST请求中交换给 `token_url`，根据OAuth协议的客户端凭据流程。

>[!NOTE]
>
>授权服务响应正文应与OAuth协议兼容。

如果授权服务响应 `200 OK` 和JSON响应主体，解析主体和 `access_token` 推送到边缘环境，并且 `expires_in` 用于计算 `expires_at` 和 `refresh_at` 密码的属性。 如果密码上没有环境关联， `access_token` 将被丢弃。

在以下条件下，凭据交换被视为成功：

* `expires_in` 大于 `28800` （8小时）。
* `refresh_offset` 小于的值 `expires_in` 减号 `14400` （四个小时）。 例如，如果 `expires_in` 是 `36000` （十小时），以及 `refresh_offset` 是 `28800` （8小时），交换被视为失败，因为 `28800` 大于 `36000` - `14400` (`21600`)。

如果交换成功，密码的状态属性将设置为 `succeeded` 和值 `expires_at` 和 `refresh_at` 已设置：

* `expires_at` 是当前的UTC时间加上 `expires_in`.
* `refresh_at` 是当前的UTC时间加上 `expires_in`，减去 `refresh_offset`. 例如，如果 `expires_in` 是 `43200` （十二小时）及 `refresh_offset` 是 `14400` （四个小时）， `refresh_at` 属性将设置为 `28800` （8小时）之前的UTC时间。

如果交换由于任何原因而失败， `status_details` 中的属性 `meta` 对象会更新相关信息。

#### 刷新 `oauth2-client_credentials` 密码

如果 `oauth2-client_credentials` 密码已分配给环境，其状态为 `succeeded` （已成功交换凭据），新交换将在以下日期自动执行： `refresh_at`.

如果交换成功， `refresh_status` 中的属性 `meta` 对象设置为 `succeeded` while `expires_at`， `refresh_at`、和 `activated_at` 将进行相应更新。

如果交换失败，则再次尝试该操作，上次尝试的时间不超过访问令牌过期两小时。 如果所有尝试都失败， `refresh_status_details` 属性来自 `meta` 对象更新及相关详细信息。

### `oauth2-google` {#oauth2-google}

带有的密钥 `type_of` 值 `oauth2-google` 需要以下属性 `credentials`：

| 凭据属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `scopes` | 数组 | 列出用于身份验证的Google产品范围。 支持以下范围：<ul><li>[Google Ads](https://developers.google.com/google-ads/api/docs/oauth/overview)： `https://www.googleapis.com/auth/adwords`</li><li>[Google Pub/Sub](https://cloud.google.com/pubsub/docs/reference/service_apis_overview)： `https://www.googleapis.com/auth/pubsub`</li></ul> |

创建之后 `oauth2-google` 密码，响应包含 `meta.authorization_url` 属性。 您必须将此URL复制并粘贴到浏览器中才能完成Google身份验证流程。

#### 重新授权 `oauth2-google` 密码

的授权URL `oauth2-google` 密钥在创建后一小时过期（如所示） `meta.authorization_url_expires_at`)。 在此时间之后，必须重新授权密钥才能续订身份验证过程。

请参阅 [密钥端点指南](../endpoints/secrets.md#reauthorize) 以详细了解如何重新授权 `oauth2-google` 向Reactor API发出PATCH请求以作为密钥。

## 环境关系

创建密码时，必须指定 [环境](../endpoints/environments.md) 在那里它将会存在。 密钥会立即部署到在其中创建它们的环境。

密码只能与一个环境相关联。 一旦秘密与环境之间的关系建立，就不能从环境中清除该秘密，并且该秘密不能与不同的环境相关联。

>[!NOTE]
>
>此规则的唯一例外是删除相关环境时。 在这种情况下，关系会被清除，并且密钥可以分配给不同的环境。

成功交换密码的凭据后，为了与环境关联的密码，交换构件(的令牌字符串 `token`，的Base64编码字符串 `simple-http`，或的访问令牌 `oauth2-client_credentials`)将安全地保存在环境中。

在环境中成功保存Exchange工件后， `activated_at` 属性设置为当前UTC时间，现在可以使用数据元素引用。 请参阅 [下一节](#referencing-secrets) 以了解有关引用密码的更多信息。

## 引用密钥 {#referencing-secrets}

要引用密码，您必须创建一个类型为“”的数据元素[!UICONTROL 密码]“(由 [[!UICONTROL 核心] 扩展](../../extensions/client/core/overview.md))。 配置此数据元素时，系统会提示您指明每个环境要使用的密码。 然后，您可以创建引用机密数据元素的规则，例如HTTP调用的标头中的规则。

![机密数据元素](../../images/api/guides/secrets/data-element.png)

>[!NOTE]
>
>要将机密数据元素添加到库，您必须至少有一个 `succeeded` 与库构建环境关联的密码。 例如，如果库中包含的机密数据元素不包含 `succeeded` 为配置的密码 [!UICONTROL 暂存密码] 部分，尝试在暂存环境中构建该库将导致错误。

在运行时，将机密数据元素替换为保存在环境中的相应机密交换构件。

## 后续步骤

本指南介绍了在Reactor API中使用机密的基础知识。 有关如何使用API调用管理密钥的详细信息，请参阅 [密钥端点指南](../endpoints/secrets.md).
