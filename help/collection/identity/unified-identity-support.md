---
title: 数据收集中的统一身份支持
description: 了解统一身份支持如何在Web数据收集中将第一方持久性和受支持的第三方激活结合在一起。
hide: true
hidefromtoc: true
badge: Beta 版
source-git-commit: 32c2565d31eed4eda28195afaf82aac6f04a6f8a
workflow-type: tm+mt
source-wordcount: '1029'
ht-degree: 3%

---

# 数据收集中的统一身份支持

>[!AVAILABILITY]
>
>此功能当前处于测试阶段。 可用性、行为和文档可能会发生变化。

统一身份支持使Edge Network可以同时在第一方和第三方身份上下文中工作。 它可以在支持第三方Cookie的浏览器中，将您拥有的属性的持久第一方标识与第三方激活工作流整合在一起。 有关Web SDK如何处理ECID、FPID和其他身份信号的背景，请参阅数据收集中的[身份](./overview.md)。

通过统一身份支持，您可以：

* **最大化受众覆盖范围**：在第三方目标（DSP、SSP和广告网络）上激活Experience Platform受众，以获得更大份额的流量。
* **保持测量准确性**：在拥有的属性和广告平台之间保持一致的访客识别。
* **您的实施经得起未来考验**：使用第一方设备ID作为您的基础，同时保持与第三方激活工作流的兼容性。

当访客访问您的网站时，Edge Network会评估可用的身份信号，即在条件允许时自动关联第一方和第三方上下文。 阻止第三方Cookie的浏览器将继续在第一方模式下运行，而不会中断您的实施。

## 工作原理

Edge Network通过按照以下优先级顺序评估可用身份信号来生成ECID：

| 优先级 | 来源 | 上下文 | 行为 |
| --- | --- | --- | --- |
| 1 | **Demdex ID** | 第三方 | 如果存在Demdex ID，则会从中植入ECID。 此种子会在共享相同第三方Cookie的域之间生成一致的ECID。 |
| 2 | **FPID** | 第一方 | 如果不存在任何Demdex ID，但存在FPID，则ECID是从FPID中植入的，并且会从中派生一个Demdex ID。 |
| 3 | **Random** | 第一方 | 如果Demdex ID和FPID都不可用，则会生成一个新的随机ECID并从中派生一个Demdex ID。 |

ECID和Demdex ID通过确定性算法以密码方式连接，这意味着可以从另一个衍生。 这种关系允许Edge Network在第一方和第三方身份上下文之间转换，而无需在实施中单独的访客处理逻辑。

由于这种关系是确定性的，因此当相应的Demdex ID可用时，基于第一方ECID构建的受众可以通过第三方基础架构激活。

对于已具有FPID派生的ECID的访客，Edge Network可以自动将其第一方身份链接到第三方身份上下文。 当浏览器支持第三方Cookie并且不需要对实施进行更改时，此操作会透明地发生。 发生自动链接时：

1. Edge Network检测到访客的ECID并非派生自Demdex ID。
1. 如果访客的浏览器支持第三方Cookie，则会触发轻量级身份同步。
1. 系统会在访客的第一方ECID与其第三方身份之间创建一个链接。
1. 该链接存储在身份存储中，从而支持在第三方目标上进行受众激活。

自动链接可保留现有ECID并防止访客悬崖。 随着时间的推移，随着访客的返回并发生关联，您的更多受众将逐渐符合使用第三方激活的资格。

第三方受众激活依赖于ID同步（ID同步）。 当Edge Network建立或刷新第三方身份时，它会在响应中返回ID同步指令。 这些说明会指示浏览器将访客身份与合作伙伴域（DSP、广告网络和其他激活平台）同步，以便在这些平台上匹配和交付您的Experience Platform受众。

## 先决条件

统一身份支持需要以下所有项：

* 您的网站在您控制的域上使用第一方数据收集。
* 您的实施使用FPID或其他第一方持久性策略作为基础。
* 您的Web SDK配置中已启用第三方Cookie。
* 已为数据流启用第三方ID同步。
* 访客使用的浏览器允许第三方Cookie（请参阅下面的[浏览器兼容性](#browser-compatibility)）。

## 配置

1. **在Web SDK中启用第三方Cookie**：在Web SDK实现中启用&#x200B;**使用第三方Cookie**&#x200B;设置。 如果使用标记扩展，请在&#x200B;**[!UICONTROL Use third-party cookies]**&#x200B;身份配置设置[中启用](/help/tags/extensions/client/web-sdk/configure/identity.md#use-third-party-cookies)。 如果使用JavaScript库，请将[`thirdPartyCookiesEnabled`](/help/collection/js/commands/configure/thirdpartycookiesenabled.md)设置为`true`。

1. **在数据流中启用第三方ID同步**：在数据流的高级设置中启用&#x200B;**[!UICONTROL Third-Party ID Sync]**&#x200B;选项。 请参阅[创建和配置数据流](/help/datastreams/configure.md#advanced-options)。

1. **确保第一方持久性已就绪**：确认您的第一方持久性策略（如FPID）已部署到您拥有的域上。 查看数据收集[中的](fpid.md)第一方设备ID。

## 验证

验证统一身份支持是否正常工作：

1. 打开浏览器的开发人员工具并导航到&#x200B;**网络**&#x200B;选项卡。
1. 清除现有请求并在新的或无痕会话中触发Web SDK事件（页面加载或自定义事件）。
1. 查找Edge Network响应（查找对`adobedc.demdex.net`和您的第一方收集端点的调用）。
1. 检查ID同步指令的响应有效负载。

当出现ID同步指令时，响应包含类似于以下内容的`identity:exchange`句柄：

```json
{
  "handle": [
    {
      "type": "identity:exchange",
      "payload": [
        {
          "type": "url",
          "id": 411,
          "spec": {
            "url": "https://example.com/...",
            "hideReferrer": false,
            "ttlMinutes": 10080
          }
        },
        {
          "type": "url",
          "id": 89,
          "spec": {
            "url": "https://example.org/...",
            "hideReferrer": true,
            "ttlMinutes": 10080
          }
        }
      ]
    }
  ]
}
```

| 元素 | 描述 |
| --- | --- |
| `type: "identity:exchange"` | 表示存在ID同步指令。 |
| `payload`数组 | 合作伙伴ID同步URL的列表。 |
| `url`值 | 将URL重定向到合作伙伴域以进行ID同步。 |
| `id`值 | 合作伙伴标识符。 |

>[!TIP]
>
>如果您在响应中未看到`identity:exchange`句柄：
>
>* 确保使用新的或无痕浏览器会话进行测试。 现有身份不会触发新同步。
>* 验证数据流和Web SDK设置是否已正确配置。
>* 确认您使用的浏览器支持第三方Cookie（请参阅下表）。

确认ID同步活动后，请验证：

* 在您拥有的域上进行的页面加载中，第一方身份会按预期持续存在。
* 激活和报告流程在您支持的环境中按预期运行。

## 浏览器兼容性 {#browser-compatibility}

第三方身份功能取决于浏览器对第三方Cookie的支持。 下表总结了预期行为：

| 浏览器 | 第三方Cookie支持 | Demdex可用 | 身份行为 |
| --- | --- | --- | --- |
| Google Chrome | 受支持 | 是 | Demdex→ECID（跨域一致） |
| Microsoft Edge | 默认支持 | 是 | Demdex→ECID（跨域一致） |
| Mozilla Firefox | 默认阻止(ETP) | 否（默认） | FPID→ECID（每个域） |
| Apple Safari | 已阻止(ITP) | 否 | FPID→ECID（每个域） |

对于阻止第三方Cookie的浏览器，第一方标识将继续正常工作。 第三方激活功能仅在浏览器允许使用第三方Cookie时可用。

## 限制

* 第三方身份行为完全取决于访客允许第三方Cookie的浏览器。 在阻止第三方激活的浏览器中，不存在第三方激活的回退。
* 自动链接要求访客返回网站。 有资格进行第三方激活的受众比例会随着时间的推移逐渐增加。
