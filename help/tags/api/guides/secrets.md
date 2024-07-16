---
title: Reactor API中的密钥
description: 了解有关如何在Reactor API中配置用于事件转发的密钥的基础知识。
exl-id: 0298c0cd-9fba-4b54-86db-5d2d8f9ade54
source-git-commit: 88939d674c0002590939004e0235d3da8b072118
workflow-type: tm+mt
source-wordcount: '1206'
ht-degree: 2%

---

# Reactor API中的密钥

在Reactor API中，密码是表示身份验证凭据的资源。 在事件转发中使用密码来向另一个系统验证以进行安全的数据交换。 因此，只能在事件转发属性（`platform`属性设置为`edge`的属性）中创建密钥。

`type_of`属性中当前表示三种受支持的密钥类型：

| 密码类型 | 描述 |
| --- | --- |
| `token` | 表示两个系统都已知和理解的身份验证令牌值的单个字符串。 |
| `simple-http` | 包含用户名和密码的两个字符串属性。 |
| `oauth2-client_credentials` | 包含多个支持[OAuth](https://datatracker.ietf.org/doc/html/rfc6749)身份验证规范的属性。 事件转发会要求您提供所需信息，然后在指定的时间间隔内为您处理这些令牌的续订。 |

{style="table-layout:auto"}

本指南简要介绍如何配置用于事件转发的密钥。 有关如何在Reactor API中管理密码的详细指导，包括密码结构的JSON示例，请参阅[密码端点指南](../endpoints/secrets.md)。

## 凭据

每个密钥都包含一个`credentials`属性，该属性保存其各自的凭据值。 在[在API](../endpoints/secrets.md#create)中创建密钥时，每种类型的密钥都有不同的必需属性，如以下部分所示：

* [&#39;令牌&#39;](#token)
* [&#39;simple-http&#39;](#simple-http)
* [&#39;oauth2-client_credentials&#39;](#oauth2-client_credentials)
* [&#39;oauth2-google&#39;](#oauth2-google)

### `token` {#token}

`type_of`值为`token`的密钥只需要`credentials`下的单个特性：

| 凭据属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `token` | 字符串 | 目标系统可识别的机密令牌。 |

{style="table-layout:auto"}

令牌存储为静态值，因此在创建密钥时，密钥的`expires_at`和`refresh_at`属性将设置为`null`。

### `simple-http` {#simple-http}

`type_of`值为`simple-http`的密钥需要`credentials`下的以下属性：

| 凭据属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `username` | 字符串 | 用户名。 |
| `password` | 字符串 | 密码。 API响应中不包含此值。 |

{style="table-layout:auto"}

创建密钥后，将使用`username:password`的BASE64编码交换这两个属性。 交换后，密码的`expires_at`和`refresh_at`属性设置为`null`。

### `oauth2-client_credentials` {#oauth2-client_credentials}

`type_of`值为`oauth2-client_credentials`的密钥需要`credentials`下的以下属性：

| 凭据属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `client_id` | 字符串 | Oauth集成的客户端ID。 |
| `client_secret` | 字符串 | OAuth集成的客户端密码。 API响应中不包含此值。 |
| `token_url` | 字符串 | Oauth集成的授权URL。 |
| `refresh_offset` | 整数 | *（可选）*&#x200B;刷新操作偏移的值（以秒为单位）。 如果在创建密钥时省略此属性，则默认情况下将该值设置为`14400`（四个小时）。 |
| `options` | 对象 | *（可选）*&#x200B;为OAuth集成指定其他选项：<ul><li>`scope`：表示凭据的[OAuth 2.0作用域](https://oauth.net/2/scope/)的字符串。</li><li>`audience`：表示[Auth0访问令牌](https://auth0.com/docs/protocols/protocol-oauth2)的字符串。</li></ul> |

创建或更新`oauth2-client_credentials`密钥后，根据OAuth协议的客户端凭据流程，在POST请求中将`client_id`和`client_secret`（可能还有`options`）交换给`token_url`。

>[!NOTE]
>
>预期授权服务响应正文与OAuth协议兼容。

如果授权服务使用`200 OK`和JSON响应正文进行响应，则解析正文并将`access_token`推送到Edge环境，并使用`expires_in`计算密码的`expires_at`和`refresh_at`属性。 如果密码上不存在环境关联，则会丢弃`access_token`。

在以下条件下，凭据交换被视为成功：

* `expires_in`大于`28800`（8小时）。
* `refresh_offset`小于`expires_in`减去`14400`的值（四个小时）。 例如，如果`expires_in`是`36000` （10个小时），而`refresh_offset`是`28800` （8个小时），则交换被视为失败，因为`28800`大于`36000` - `14400` (`21600`)。

如果交换成功，密码的状态属性将设置为`succeeded`，并设置`expires_at`和`refresh_at`的值：

* `expires_at`是当前UTC时间加上`expires_in`的值。
* `refresh_at`是当前UTC时间加上`expires_in`的值减去`refresh_offset`的值。 例如，如果`expires_in`是`43200` （十二小时），`refresh_offset`是`14400` （四个小时），则`refresh_at`属性将在当前UTC时间之后设置为`28800` （八个小时）。

如果交换由于任何原因失败，`meta`对象中的`status_details`属性将使用相关信息更新。

#### 正在刷新`oauth2-client_credentials`密码

如果已将`oauth2-client_credentials`密钥分配给环境并且其状态为`succeeded`（已成功交换凭据），则将在`refresh_at`上自动执行新的交换。

如果交换成功，`meta`对象中的`refresh_status`属性将设置为`succeeded`，同时相应地更新`expires_at`、`refresh_at`和`activated_at`。

如果交换失败，则再次尝试该操作3次，最后一次尝试的时间不超过访问令牌过期前的2小时。 如果所有尝试都失败，`meta`对象中的`refresh_status_details`属性将更新为相关详细信息。

### `oauth2-google` {#oauth2-google}

`type_of`值为`oauth2-google`的密钥需要`credentials`下的以下属性：

| 凭据属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `scopes` | 数组 | 列出用于身份验证的Google产品范围。 支持以下范围：<ul><li>[Google广告](https://developers.google.com/google-ads/api/docs/oauth/overview)： `https://www.googleapis.com/auth/adwords`</li><li>[Google Pub/Sub](https://cloud.google.com/pubsub/docs/reference/service_apis_overview)： `https://www.googleapis.com/auth/pubsub`</li></ul> |

创建`oauth2-google`密钥后，响应包含`meta.authorization_url`属性。 您必须将此URL复制并粘贴到浏览器中才能完成Google身份验证流程。

#### 重新授权`oauth2-google`密码

`oauth2-google`密码的授权URL将在创建密码后一小时过期（如`meta.authorization_url_expires_at`所指示）。 在此时间之后，必须重新授权密钥才能更新身份验证过程。

有关如何通过向Reactor API发出PATCH请求来重新授权`oauth2-google`密钥的详细信息，请参阅[密钥端点指南](../endpoints/secrets.md#reauthorize)。

## 环境关系

创建密码时，必须指定密码将存在的[环境](../endpoints/environments.md)。 密钥会立即部署到在其中创建它们的环境。

密钥只能与一个环境关联。 一旦秘密与环境之间的关系建立，就不能从环境中清除该秘密，也不能将该秘密与不同的环境相关联。

>[!NOTE]
>
>此规则的唯一例外是删除相关环境时。 在这种情况下，关系会被清除，并且密码可以分配给不同的环境。

成功交换密钥的凭据后，为将密钥与环境相关联，将在环境中安全地保存Exchange项目（`token`的令牌字符串、`simple-http`的Base64编码字符串或`oauth2-client_credentials`的访问令牌）。

在环境中成功保存Exchange工件后，密码的`activated_at`属性将设置为当前的UTC时间，现在可以使用数据元素引用该属性。 有关引用密码的更多信息，请参阅[下一节](#referencing-secrets)。

## 引用密钥 {#referencing-secrets}

为了引用密码，您必须在事件转发属性上创建类型为“[!UICONTROL 密码]”（由[[!UICONTROL Core]扩展](../../extensions/client/core/overview.md)提供）的数据元素。 配置此数据元素时，系统会提示您指明每个环境要使用的密码。 然后，您可以创建引用机密数据元素的规则，例如HTTP调用的标头中的规则。

![机密数据元素](../../images/api/guides/secrets/data-element.png)

>[!NOTE]
>
>若要向库中添加机密数据元素，您必须至少有一个`succeeded`机密与正在生成库的环境关联。 例如，如果某个库的机密数据元素没有为[!UICONTROL 暂存密码]部分配置`succeeded`密码，则尝试在暂存环境中构建该库会导致错误。

在运行时，将机密数据元素替换为保存在环境中的相应机密交换构件。

## 后续步骤

本指南介绍了在Reactor API中使用机密的基础知识。 有关如何使用API调用管理密钥的详细信息，请参阅[密钥端点指南](../endpoints/secrets.md)。
