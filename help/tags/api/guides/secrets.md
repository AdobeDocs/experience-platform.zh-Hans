---
title: Reactor API中的密钥
description: 了解如何在Reactor API中配置用于事件转发的密钥的基础知识。
exl-id: 0298c0cd-9fba-4b54-86db-5d2d8f9ade54
source-git-commit: 88939d674c0002590939004e0235d3da8b072118
workflow-type: tm+mt
source-wordcount: '1241'
ht-degree: 2%

---

# Reactor API中的密钥

在Reactor API中，密钥是表示身份验证凭据的资源。 在事件转发中使用密钥来向另一个系统进行身份验证以进行安全数据交换。 因此，只能在事件转发属性(其 `platform` 属性设置为 `edge`)。

当前，在 `type_of` 属性：

| 密钥类型 | 描述 |
| --- | --- |
| `token` | 一个字符串，表示两个系统已知和理解的身份验证令牌值。 |
| `simple-http` | 包含用户名和密码的两个字符串属性。 |
| `oauth2-client_credentials` | 包含多个属性以支持 [OAuth](https://datatracker.ietf.org/doc/html/rfc6749) 验证规范。 事件转发会要求您获取所需信息，然后在指定的时间间隔内为您处理这些令牌的续订。 |

{style=&quot;table-layout:auto&quot;}

本指南提供了有关如何配置用于事件转发的密钥的高级概述。 有关如何在Reactor API中管理密钥（包括密钥结构的示例JSON）的详细指南，请参阅 [secrets endpoint指南](../endpoints/secrets.md).

## 凭据

每个密钥都包含 `credentials` 属性。 When [在API中创建密钥](../endpoints/secrets.md#create)，则每种类型的密钥具有不同的必需属性，如以下部分所示：

* [`令牌`](#token)
* [&#39;simple-http&#39;](#simple-http)
* [&#39;oauth2-client_credentials&#39;](#oauth2-client_credentials)
* [&#39;oauth2-google&#39;](#oauth2-google)

### `token` {#token}

含有 `type_of` 值 `token` 只需在 `credentials`:

| 凭据属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `token` | 字符串 | 目标系统可理解的密钥令牌。 |

{style=&quot;table-layout:auto&quot;}

令牌将存储为静态值，因此密钥的 `expires_at` 和 `refresh_at` 属性设置为 `null` 创建密钥时。

### `simple-http` {#simple-http}

含有 `type_of` 值 `simple-http` 需要在 `credentials`:

| 凭据属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `username` | 字符串 | 用户名。 |
| `password` | 字符串 | 密码。 API响应中未包含此值。 |

{style=&quot;table-layout:auto&quot;}

创建密钥后，这两个属性会与的BASE64编码交换 `username:password`. 交换后，秘密 `expires_at` 和 `refresh_at` 属性设置为 `null`.

### `oauth2-client_credentials` {#oauth2-client_credentials}

含有 `type_of` 值 `oauth2-client_credentials` 需要在 `credentials`:

| 凭据属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `client_id` | 字符串 | OAuth集成的客户端ID。 |
| `client_secret` | 字符串 | OAuth集成的客户端密钥。 API响应中未包含此值。 |
| `token_url` | 字符串 | OAuth集成的授权URL。 |
| `refresh_offset` | 整数 | *（可选）* 用于将刷新操作偏移的值（以秒为单位）。 如果在创建密钥时忽略此属性，则会将值设置为 `14400` （4小时）。 |
| `options` | 对象 | *（可选）* 为OAuth集成指定其他选项：<ul><li>`scope`:表示 [OAuth 2.0范围](https://oauth.net/2/scope/) ，以获取凭据。</li><li>`audience`:表示 [Auth0访问令牌](https://auth0.com/docs/protocols/protocol-oauth2).</li></ul> |

当 `oauth2-client_credentials` 密钥创建或更新， `client_id` 和 `client_secret` (可能 `options`)会在向 `token_url`，根据OAuth协议的客户端凭据流。

>[!NOTE]
>
>授权服务响应主体应与OAuth协议兼容。

如果授权服务响应 `200 OK` 和JSON响应主体之后，将解析主体并 `access_token` 被推送到边缘环境，并且 `expires_in` 用于计算 `expires_at` 和 `refresh_at` 属性。 如果秘密上没有环境关联， `access_token` 将被丢弃。

在以下条件下，凭据交换被视为成功：

* `expires_in` 大于 `28800` （八小时）。
* `refresh_offset` 小于的值 `expires_in` 减号 `14400` （四小时）。 例如，如果 `expires_in` is `36000` （10小时）， `refresh_offset` is `28800` （8小时），则交换被视为失败，因为 `28800` 大于 `36000` - `14400` (`21600`)。

如果交换成功，则密钥的状态属性将设置为 `succeeded` 和值 `expires_at` 和 `refresh_at` 已设置：

* `expires_at` 是当前UTC时间加值 `expires_in`.
* `refresh_at` 是当前UTC时间加值 `expires_in`，减去的值 `refresh_offset`. 例如，如果 `expires_in` is `43200` （十二小时） `refresh_offset` is `14400` （四小时） `refresh_at` 属性将设置为 `28800` （8小时）当前UTC时间之后。

如果交易因任何原因失败， `status_details` 属性 `meta` 对象会更新相关信息。

#### 刷新 `oauth2-client_credentials` 秘密

如果 `oauth2-client_credentials` 已将密钥分配给环境，其状态为 `succeeded` （凭据交换成功），则会在 `refresh_at`.

如果交换成功，则 `refresh_status` 属性 `meta` 对象设置为 `succeeded` while `expires_at`, `refresh_at`和 `activated_at` 会相应地更新。

如果交换失败，操作将再次尝试三次，上次尝试的时间不超过访问令牌过期前的两小时。 如果所有尝试都失败， `refresh_status_details` 属性 `meta` 对象会更新相关详细信息。

### `oauth2-google` {#oauth2-google}

含有 `type_of` 值 `oauth2-google` 需要在 `credentials`:

| 凭据属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `scopes` | 数组 | 列出Google产品验证范围。 支持以下范围：<ul><li>[Google Ads](https://developers.google.com/google-ads/api/docs/oauth/overview): `https://www.googleapis.com/auth/adwords`</li><li>[Google Pub/Sub](https://cloud.google.com/pubsub/docs/reference/service_apis_overview): `https://www.googleapis.com/auth/pubsub`</li></ul> |

创建 `oauth2-google` 密钥，响应包括 `meta.authorization_url` 属性。 您必须将此URL复制并粘贴到浏览器中，才能完成Google身份验证流程。

#### 重新授权 `oauth2-google` 秘密

的授权URL `oauth2-google` 密钥在创建密钥一小时后过期(如 `meta.authorization_url_expires_at`)。 此后，必须重新授权密钥，才能续订身份验证过程。

请参阅 [secrets endpoint指南](../endpoints/secrets.md#reauthorize) 有关如何重新授权的详细信息 `oauth2-google` 向Reactor API发出PATCH请求以进行密钥。

## 环境关系

创建密钥时，必须指定 [环境](../endpoints/environments.md) 它将存在。 密钥会立即部署到其创建环境。

密钥只能与一个环境关联。 一旦建立了密钥与环境之间的关系，便无法从环境中清除该密钥，并且该密钥无法与其他环境关联。

>[!NOTE]
>
>此规则的唯一例外是相关环境被删除。 在这种情况下，将清除关系并将密钥分配给其他环境。

成功交换密钥的凭据后，为了与环境关联的密钥，交换对象(用于 `token`，的Base64编码字符串 `simple-http`，或的访问令牌 `oauth2-client_credentials`)安全地保存在环境中。

在环境中成功保存Exchange对象后，密钥的 `activated_at` 属性设置为当前UTC时间，现在可以使用数据元素引用。 请参阅 [下一部分](#referencing-secrets) 以了解有关引用密钥的更多信息。

## 引用密钥 {#referencing-secrets}

要引用密钥，必须创建类型为“[!UICONTROL 密码]”(由 [[!UICONTROL 核心] 扩展](../../extensions/client/core/overview.md))。 配置此数据元素时，系统会提示您指明要为每个环境使用的密钥。 然后，您可以创建引用机密数据元素的规则，例如在HTTP调用的标头中。

![密钥数据元素](../../images/api/guides/secrets/data-element.png)

>[!NOTE]
>
>要向库中添加密钥数据元素，您必须至少具有一个 `succeeded` 与正在构建库的环境关联的密钥。 例如，如果库的机密数据元素没有 `succeeded` 为配置的密钥 [!UICONTROL 暂存密钥] 部分，尝试在暂存环境中构建该库将导致错误。

在运行时，将秘密数据元素替换为保存在环境中的相应秘密交换对象。

## 后续步骤

本指南介绍了在Reactor API中处理密钥的基础知识。 有关如何使用API调用管理密钥的详细信息，请参阅 [secrets endpoint指南](../endpoints/secrets.md).
