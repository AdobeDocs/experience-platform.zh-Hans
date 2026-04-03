---
title: 在数据收集中使用identityMap
description: 了解如何构造和发送identityMap负载，以识别Web SDK实施中的跨命名空间已知访客。
source-git-commit: 696e5098ebf556bfc0fa4fc22ff637cb0835eee0
workflow-type: tm+mt
source-wordcount: '1671'
ht-degree: 0%

---

# 在数据收集中使用identityMap

`identityMap`有效负载对象是您告知Edge Network哪些访客超出其设备级[ECID](./overview.md)的方法。 当访客登录、完成购买或以其他方式得知时，您可以随ECID发送人员级别标识符（CRM ID、哈希电子邮件、忠诚度ID等）。 这些人员级别的标识符为下游服务提供了有价值的信息，以便它们可以：

* **跨设备和渠道将活动拼合到人员。** [身份服务](/help/identity-service/home.md)将您发送的身份链接到[身份图](/help/identity-service/features/identity-graph-viewer.md)，从而将匿名设备级行为连接到已知人员。
* **构建统一客户配置文件。** [实时客户个人资料](/help/profile/home.md)使用您设置为将事件和属性锚定到单个个人资料的主要标识，从而启用人员级别分段和受众构建。
* **激活下游目标上的受众。**&#x200B;许多[目标](/help/destinations/home.md)需要解析的人员级别身份（散列电子邮件、电话号码等）以将受众与其用户基础相匹配。
* **编排跨渠道历程。** [Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html?lang=zh-Hans)使用已解析的身份，根据访客的已验证行为，跨电子邮件、推送和应用程序内渠道触发历程并对历程进行个性化。

本页介绍如何构建`identityMap`负载、为每个标识选择正确的设置以及处理常见的实施方案。

## 有效负荷结构 {#structure}

`identityMap`是一个JSON对象，其中的每个顶级键都是一个命名空间，该值是一个身份描述符数组。 您可以在单个有效负载中包含一个或多个命名空间，并且每个描述符包含三个字段：`id`、`authenticatedState`和`primary`。

```json
{
  "identityMap": {
    "CRMID": [
      {
        "id": "abc-123-xyz",
        "authenticatedState": "authenticated",
        "primary": true
      }
    ]
  }
}
```

| 字段 | 类型 | 必需 | 描述 |
| --- | --- | --- | --- |
| `id` | 字符串 | 是 | 标识符值（例如，`user@example.com`或`ABC123`）。 |
| `authenticatedState` | 字符串 | 是 | 您非常自信地知道此身份属于访客。 有效值包括`ambiguous`、`authenticated`和`loggedOut`。 |
| `primary` | 布尔值 | 是 | 此身份是否应是事件的主要标识符。 必须将所有命名空间中的唯一标识标记为`primary: true`。 |

以下各部分详细介绍了有效负载的各个部分。

### 命名空间键 {#namespace-keys}

`identityMap`中的每个顶级键都是[标识命名空间](/help/identity-service/features/namespaces.md) — 一个对标识符类型进行分类的字符串（例如，`CRMID`、`Email`、`Phone`或`LoyaltyId`）。 命名空间必须存在于Identity Service中，然后才能在有效负载中引用它们。 当访客具有多个标识符时，可以在同一事件中包含多个命名空间键。

您无需包含ECID作为命名空间密钥。 Edge Network会自动将ECID添加到身份有效负载中。 如果您明确地包含ECID，则当也存在人员级别标识时，请勿将其标记为`primary`。

### `id` {#id}

`id`字段是标识符字符串本身，该值用于告知Experience Platform此身份表示的特定人员或设备。 每个[标识命名空间](/help/identity-service/features/namespaces.md)都需要特定的值格式，而以错误的格式发送值会创建一个无法与正确格式化的版本合并的不同标识，从而导致配置文件碎片。

在`identityMap`中包含值之前，请根据目标命名空间期望的格式准备该值：

| 常见命名空间类型 | 如何准备值 | 示例 |
| --- | --- | --- |
| **CRM/内部ID** | 使用记录系统分配的确切标识符。 保持所有事件（大小写、前导零、前缀）的格式一致。 | `ABC-12345`、`00098765` |
| **电子邮件（原始）** | 小写完整电子邮件地址，并修剪前导和尾随空格。 | `user@example.com` |
| **电子邮件（散列）** | 小写并首先修剪电子邮件地址，然后使用SHA-256进行散列。 发送生成的64字符十六进制字符串。 除非您的命名空间定义需要使用Salt，否则请勿添加Salt。 | `a1b2c3d4e5f6a7b8c9...` |
| **电话(E.164)** | 以[E.164](https://en.wikipedia.org/wiki/E.164)格式设置数字：前导`+`、国家/地区代码以及没有空格或标点的订阅者号码。 | `+15551234567` |
| **FPID** | 生成[UUIDv4](https://datatracker.ietf.org/doc/html/rfc4122)字符串。 有关生成要求，请参阅[第一方设备ID](./fpid.md)。 | `123e4567-e89b-42d3-9456-426614174000` |

有关标准命名空间及其定义的完整列表，请参阅[身份命名空间概述](/help/identity-service/features/namespaces.md#standard)。

>[!TIP]
>
>`id`值区分大小写。 `User@Example.com`和`user@example.com`被视为两个单独的标识。 在发送值之前标准化大小写（通常通过将电子邮件转换为小写并修剪空格）以避免在图形中创建重复的标识。

#### 正在运行时收集`id` {#collect-id}

您需要的标识符很少直接在页面上可用。 常见的收集策略包括：

* **数据层**：在访客登录后，从网站的数据层读取标识符。 此位置是最可靠的方法，因为数据层由应用程序后端填充，并反映经过身份验证的会话状态。
* **身份验证令牌或会话Cookie**：从身份验证系统设置的JWT或会话Cookie解码或查找标识符。 在使用值之前，请验证令牌是否仍处于活动状态。
* **服务器端扩充**：使用[数据收集](/help/datastreams/data-prep.md)的数据准备或[事件转发规则](/help/tags/ui/event-forwarding/overview.md)在Edge上映射或转换标识符，然后该标识符到达下游服务。 当客户端只有映射到服务器端内部ID的不透明会话令牌时，此位置非常有用。

>[!TIP]
>
>如果给定的`id`值解析为空字符串`null`或`undefined`，则不要在`identityMap`中包含命名空间。 发送空的`id`会创建损坏的身份记录。 在构建有效负载之前，使用检查功能保护实施。

### `authenticatedState` {#authenticated-state}

`authenticatedState`字段告知下游服务在给定标识中要放置多少信任。 以下值对此字段有效：

| 值 | 使用时间 |
| --- | --- |
| **`authenticated`** | 访客已在当前会话期间主动验证其身份（例如，使用凭据登录、完成MFA或类似验证）。 |
| **`loggedOut`** | 访客之前已经过身份验证，但随后已注销。 该身份仍与设备关联，但会话不再处于活动状态。 |
| **`ambiguous`** | 无法确认该身份属于当前访客。 将此值用于设备级标识符（如FPID）或尚未进行身份验证的任何标识符。 |

>[!TIP]
>
>`authenticatedState`值影响Adobe Experience Platform Identity Service如何构建和合并身份图。 为尚未验证的标识发送`authenticated`可能会创建不正确的跨设备链接，而这些链接很难撤消。

### `primary` {#primary-identity}

每个`identityMap`有效负载必须正好有一个标记为`primary: true`的标识。 主标识可确定在Experience Platform中将哪个标识用作事件的锚点。

设置主标识时，请遵循以下准则：

* **当人员级别标识可用时**（访客已登录），请将人员级别命名空间标记为主命名空间，并将ECID标记为非主命名空间。 这会告知Experience Platform将事件锚定到人员而非设备。
* **当只有设备级标识可用时** （访客是匿名的），ECID将自动用作主标识。 您无需在`identityMap`中包含ECID — Edge Network会自动添加它。

```json
{
  "identityMap": {
    "CRMID": [
      {
        "id": "abc-123-xyz",
        "authenticatedState": "authenticated",
        "primary": true
      }
    ],
    "Email": [
      {
        "id": "user@example.com",
        "authenticatedState": "authenticated",
        "primary": false
      }
    ]
  }
}
```

## 在您的实施中发送identityMap {#send-identity}

>[!BEGINTABS]

>[!TAB JavaScript库]

在`identityMap`调用的`xdm`对象中传递[`sendEvent`](/help/collection/js/commands/sendevent/overview.md)：

```js
alloy("sendEvent", {
  xdm: {
    identityMap: {
      CRMID: [
        {
          id: "abc-123-xyz",
          authenticatedState: "authenticated",
          primary: true
        }
      ]
    },
    eventType: "web.webpagedetails.pageViews"
  }
});
```

>[!TAB Web SDK标记扩展]

使用[标识映射](/help/tags/extensions/client/web-sdk/data-element-types.md#identity-map)数据元素类型在标记UI中构建您的标识有效负载：

1. 创建具有&#x200B;**[!UICONTROL Adobe Experience Platform Web SDK]**&#x200B;扩展和&#x200B;**[!UICONTROL Identity map]**&#x200B;数据元素类型的数据元素。
2. 通过指定命名空间、解析为标识符的数据元素或值以及身份验证状态来添加身份。
3. 将一个标识标记为主标识。
4. 在&#x200B;**[!UICONTROL Send event]**&#x200B;下的&#x200B;**[!UICONTROL Identity map]**&#x200B;操作中引用此数据元素。

>[!ENDTABS]

## 常见应用场景 {#common-scenarios}

+++**登录**

当访客登录时，使用`authenticatedState: "authenticated"`和`primary: true`发送其人员级别标识符。 将此身份包含在身份验证后的第一个事件上以及会话中的所有后续事件上。

```json
{
  "identityMap": {
    "CRMID": [
      {
        "id": "abc-123-xyz",
        "authenticatedState": "authenticated",
        "primary": true
      }
    ]
  }
}
```

+++

+++**注销**

访客注销时，在保留相同标识符的同时将`authenticatedState`更新为`loggedOut`。 这保留了设备和人员之间的关联，同时发出会话不再活动的信号。

```json
{
  "identityMap": {
    "CRMID": [
      {
        "id": "abc-123-xyz",
        "authenticatedState": "loggedOut",
        "primary": false
      }
    ]
  }
}
```

注销后，ECID将返回到有效的主要身份（Edge Network会自动应用它）。 请勿将其他人员级别的身份标记为主要身份，除非访客使用其他帐户登录。

>[!IMPORTANT]
>
>注销后不要完全停止发送标识符。 从`authenticated`切换到`loggedOut`会告知下游服务会话已结束。 省略标识符会在身份图中留下空白，可能会导致配置文件碎片。

+++

+++**多个命名空间**

您可以在同一事件中发送多个身份命名空间。 当访客登录并且您有多个可用标识符（例如，CRM ID、经过哈希处理的电子邮件和忠诚度ID）时，这种情况很常见。 包括所有已知标识符，仅将一个标记为主标识符，并将其他标识符设置为`primary: false`。

```json
{
  "identityMap": {
    "CRMID": [
      {
        "id": "abc-123-xyz",
        "authenticatedState": "authenticated",
        "primary": true
      }
    ],
    "Email_LC_SHA256": [
      {
        "id": "a1b2c3d4e5f6...",
        "authenticatedState": "authenticated",
        "primary": false
      }
    ],
    "LoyaltyId": [
      {
        "id": "LOY-98765",
        "authenticatedState": "authenticated",
        "primary": false
      }
    ]
  }
}
```

>[!TIP]
>
>在同一事件上发送多个具有相同`authenticatedState`的命名空间会为Identity Service提供用于链接这些身份的最强信号。 在身份验证时包括所有可用的标识符，而不是将它们分散到不同的事件中。

+++

+++**匿名访客**

对于匿名访客，您通常根本不需要发送任何`identityMap`。 Edge Network会自动分配ECID并将其用作主标识。 如果您使用[第一方设备ID](./fpid.md)，则FPID是您需要包含给匿名访客的唯一标识。

+++

## identityMap如何影响身份图 {#identity-graph}

每个到达Experience Platform的`identityMap`有效负载都由[标识服务](/help/identity-service/home.md)处理，该服务将您发送的标识链接到[标识图](/help/identity-service/features/identity-graph-viewer.md)。 您包括的命名空间、设置`authenticatedState`的方式以及标记为`primary`的身份直接影响Identity Service如何构建和合并这些图形。

要注意的关键行为：

* 在同一事件中发送的&#x200B;**标识链接在一起。**&#x200B;如果您在同一`sendEvent`调用中包含CRMID和电子邮件命名空间，Identity Service将在这两个身份之间创建链接。 将标识符分散到不同的事件中会产生较弱的链接，并可能导致图形碎片。
* **身份`primary`锚定实时客户配置文件中的事件。**&#x200B;配置文件使用主标识来确定该事件所属的配置文件。 将错误标识标记为主要标识（例如，在人员级别ID可用时，将ECID设置为主要）可能会导致根据设备级别配置文件（而非人员级别配置文件）存储事件。
* **`authenticatedState`影响图形置信度。**&#x200B;为尚未实际验证的标识发送`authenticated`可能会创建不正确的跨设备链接，而这些链接很难撤消。 仅当访客在当前会话期间主动证明其身份时才使用`authenticated`。

如果您的实施使用[身份图链接规则](/help/identity-service/identity-graph-linking-rules/overview.md)（如命名空间优先级或身份优化算法），请查看[实施指南](/help/identity-service/identity-graph-linking-rules/implementation-guide.md)，以了解这些规则如何与您通过`identityMap`发送的身份进行交互。

>[!NOTE]
>
>`identityMap`仅在Web SDK向Edge Network发出请求时发送，该请求受访客同意状态的限制。 如果您的实施使用`defaultConsent: "pending"`，则在获得同意之前不会发送身份。 有关详细信息，请参阅[同意和标识](./consent.md)。
