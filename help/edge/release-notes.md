---
title: Adobe Experience Platform Web SDK 发行说明
description: Adobe Experience Platform Web SDK 最新发行说明。
keywords: Adobe Experience Platform Web SDK；平台Web SDK；Web SDK；发行说明；
exl-id: efd4e866-6a27-4bd5-af83-4a97ca8adebd
source-git-commit: 5f2358c2e102c66a13746004ad73e2766e933705
workflow-type: tm+mt
source-wordcount: '1549'
ht-degree: 3%

---


# 发行说明

本文档介绍了Adobe Experience Platform Web SDK的发行说明。
有关Web SDK标记扩展的最新发行说明，请参阅 [Web SDK标记扩展发行说明](../tags/extensions/client/web-sdk/web-sdk-ext-release-notes.md).

## 版本2.16.0 - 2023年5月17日

**修复和改进功能**

* Web SDK现在对Audience ManagerCookie目标值进行编码，类似于 [Data Integration Library(DIL)](https://experienceleague.adobe.com/docs/audience-manager/user-guide/dil-api/dil-overview.html?lang=en).

## 版本2.16.0 - 2023年4月25日

**新增功能**

* 添加了对的支持 [数据流配置覆盖](../datastreams/overrides.md).

## 版本2.15.0 - 2023年3月30日

**新增功能**

* 添加了对的支持 [`onBeforeLinkClickSend`](fundamentals/configuring-the-sdk.md#onBeforeLinkClickSend) 链接单击回调。
* 添加了对Adobe Journey Optimizer点击跟踪的支持。

**修复和改进功能**

* 链接收藏集现在包括链接名称和访客区域。
* 已删除失败URL目标的控制台错误。

## 版本2.14.0 - 2023年1月25日

* (Beta)添加了对Adobe Journey Optimizer表面和建议的支持。

**修复和改进功能**

* 修复了Adobe Target VEC自定义代码操作的一个问题，该问题导致代码被插入到替代位置，而不是使用 [!DNL at.js].
* 修复了在某些边缘情况下，对边缘网络的请求未正确设置“referer”标头的问题。
* 修复了以下问题： [用户代理客户端提示](fundamentals/user-agent-client-hints.md) 属性可能设置为不正确的类型。
* 修复了以下问题： `placeContext.localTime` 不匹配架构。

## 版本2.13.1 - 2022年10月13日

* 修复了在配置后定义window.Visitor的情况下，访客迁移不起作用的问题。 当使用Adobe标记运行时，这个问题尤为突出。
* 修复了以下问题： `device.screenWidth` 和 `device.screenHeight` 在某些环境中以字符串形式填充。

## 版本2.13.0 - 2022年9月28日

**新增功能**

* 添加了对的支持 [分页完整迁移](home.md#migrating-to-web-sdk). 现在，当访客在at.js和Web SDK页面之间移动时，将保留Adobe Target配置文件。
* 添加了对的可配置支持 [高熵用户代理客户端提示](fundamentals/user-agent-client-hints.md#high-entropy).
* 添加了对新版本的支持 `applyResponse` 命令。 这可通过以下方式启用混合个性化 [边缘网络服务器API](../server-api/overview.md).
* QA模式链接现在可以在多个页面中使用。

**修复和改进功能**

* 修复了在禁用链接跟踪时个性化点击跟踪量度未更新的问题。
* 更新了在指定未知选项时引发验证错误的命令。
* 此 `_experience.decisioning.propositionEventType` 属性现在在自动发送显示和交互个性化事件时填充。
* 为添加了重复的命名空间验证 `getIdentity` 命令。
* 为添加了重复的决策范围验证 `sendEvent` 命令。

## 版本2.12.0 - 2022年6月29日

* 将请求更改为Edge Network以使用 `cluster` URL中包含的Cookie位置提示。 这可确保会话期间更改其位置（例如，通过VPN或使用移动设备驾驶等）的用户点击同一边缘并具有相同的个性化配置文件。
* 在getLibraryInfo命令响应中字符串化配置的函数。

## 版本2.11.0 - 2022年6月13日

**新增功能**

* 现在，通过在移动应用程序和移动Web内容之间以及跨域共享访客ID，您可以更准确地提供个性化体验。 请参阅 [专用文档](identity/id-sharing.md) 了解更多信息。
* 您现在可以从以下位置渲染或执行建议数组 [!DNL Adobe Target] 添加到单页应用程序中，而不增加Analytics量度。 这减少了报告错误并提高了分析准确性。 请参阅 [专用文档](personalization/rendering-personalization-content.md#applypropositions) 了解更多信息。
* 已将其他信息添加到 `getLibraryInfo` 命令，其中包括可用命令和实例的最终配置。

**修复和改进功能**

* 更新了要使用的Cookie设置 `sameSite="none"` 和 `secure` 标记于 [!DNL HTTPS] 页数。
* 修复了在使用时个性化内容未正确应用的问题 `eq` 伪选择器。
* 修复了以下问题： `localTimezoneOffset` 可能无法通过Experience Platform验证。

## 版本2.10.1 - 2022年5月3日

* 修复了为ID同步和区段目标创建多个永久iframe的问题。

## 版本2.10.0 - 2022年4月22日

* 对所有ID同步和区段目标使用永久性iframe。
* 修复了合并指标建议在中复制的问题 `sendEvent` 结果。

## 版本2.9.0 - 2022年3月10日

* 添加了对跟踪的支持 [!DNL control (default)] Adobe Target体验。
* 优化了单页应用程序的查看 — 更改事件。 现在，呈现个性化体验时，显示通知包含在查看更改事件中。
* 删除控制台警告（若否） `eventType` 存在。
* 修复了以下问题 `propositions` 资产仅从 `sendEvent` 命令来指示何时请求体验或从缓存中检索体验。 此 `propositions` 属性现在将始终定义为数组。
* 修复了从Adobe Experience Edge返回错误时未显示隐藏容器的问题。
* 修复了Interact事件未计入Adobe Target中的问题。 通过将视图名称添加到XDM （网址为web.webPageDetails.viewName）解决了此问题。
* 修复控制台消息中损坏的文档链接。

## 版本2.8.0 - 2022年1月19日

* 支持用于个性化的影子DOM选择器。
* 重命名了个性化事件类型。 (`display` 和 `click` 成为 `decisioning.propositionDisplay` 和 `decisioning.propositionInteract`)
* 修复了以下问题：具有内联脚本标记的HTML选件将脚本标记两次添加到页面中，即使脚本仅运行一次。

## 版本2.7.0 - 2021年10月26日

* 在来自的返回值中公开来自Experience Edge的其他信息 `sendEvent`，包括 `inferences` 和 `destinations`. 这些属性的格式可能会随着这些功能当前作为Beta版的一部分推出而更改。 有关更多信息，请参阅 [跟踪事件。](fundamentals/tracking-events.md)

## 版本2.6.4 - 2021年9月7日

* 修复了设置HTMLAdobe Target操作应用于的问题 `head` 元素替换了整个 `head` 内容。 现在，设置应用于的HTML操作 `head` 元素更改为附加HTML。

## 版本2.6.3 - 2021年8月16日

* 修复了以下问题：非公共用途的对象通过已解析的承诺公开 `configure` 命令。

## 版本2.6.2 - 2021年8月4日

* 修复了以下问题：关于弃用的警告 `result.decisions` (由 `sendEvent` 命令)将被记录到控制台，即使 `result.decisions` 未访问属性。 访问时不会记录任何警告 `result.decisions` 资产，但该资产仍被弃用。

## 版本2.6.1 - 2021年7月29日

* 修复了以下问题：对于没有个性化内容的单页面应用程序视图，呈现个性化操作会引发错误，并导致从 `sendEvent` 命令被拒绝。

## 版本2.6.0 - 2021年7月27日

* 在中提供更多的个性化内容 `sendEvent` 已解决承诺，包括Adobe Target响应令牌。 当 `sendEvent` 执行命令，返回promise，最终使用 `result` 包含从服务器收到的信息的对象。 以前，此结果对象包含一个名为的属性 `decisions`. 此 `decisions` 属性已弃用。 新资产， `propositions`，已添加。 这个新资产使客户能够访问更多个性化内容，包括 [响应令牌](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/accessing-response-tokens.html).

## 版本2.5.0 - 2021年6月

* 添加了对重定向个性化选件的支持。
* 自动收集的负值视区宽度和高度将不再发送到服务器。
* 当通过返回取消事件时 `false` 从 `onBeforeEventSend` callback，现在会记录一条消息。
* 修复了用于单个事件的特定XDM数据片段包含在多个事件中的问题。

## 版本2.4.0 - 2021年3月

* 现在，SDK可以是 [安装为npm包](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/installing-the-sdk.html).
* 添加了对的支持 `out` 选项条件 [配置默认同意](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#default-consent)，丢弃所有事件，直到获得用户同意(现有 `pending` 选项将事件排入队列，并在收到同意后发送它们)。
* 此 [onBeforeEventSend回调](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#onbeforeeventsend) 现在可用于阻止发送事件。
* 现在使用XDM架构字段组，而不是 `meta.personalization` 发送有关正在呈现或单击的个性化内容的事件时。
* 此 [getIdentity命令](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html#retrieving-the-visitor-id) 现在，将随身份返回边缘区域ID。
* 从服务器收到的警告和错误已得到改进，并以更合适的方式进行处理。
* 添加了对的支持 [Adobe的Consent 2.0标准](https://experienceleague.adobe.com/docs/experience-platform/edge/consent/supporting-consent.html?communicating-consent-preferences-via-the-adobe-standard).
* 收到同意首选项后，将对首选项进行哈希处理并将其存储在本地存储中，以优化CMP、Platform Web SDK和Platform Edge Network之间的集成。 如果您正在收集同意首选项，我们现在鼓励您致电 `setConsent` 每次页面加载时。
* 二 [监测挂钩](https://github.com/adobe/alloy/wiki/Monitoring-Hooks)， `onCommandResolved` 和 `onCommandRejected`，已添加。
* 错误修复：当用户导航到新的单页应用程序视图、返回原始视图，并单击符合转化条件的元素时，个性化交互通知事件将包含有关相同活动的重复信息。
* 错误修复：如果SDK发送的第一个事件具有 `documentUnloading` 设置为 `true`， [`sendBeacon`](https://developer.mozilla.org/zh-CN/docs/Web/API/Navigator/sendBeacon) 将用于发送事件，从而导致有关未建立标识的错误。

## 版本2.3.0 - 2020年11月

* 添加了nonce支持，以允许实施更严格的内容安全策略。
* 添加了对单页应用程序的个性化支持。
* 改进了与其他可能正在覆盖的页面上JavaScript代码的兼容性 `window.console` API。
* 错误修复： `sendBeacon` 未使用，当时 `documentUnloading` 已设置为 `true` 或在自动跟踪链接点击量时。
* 错误修复：如果锚点元素包含HTML内容，则不会自动跟踪链接。
* 错误修复：某些包含只读的浏览器错误 `message` 未正确处理资产，导致向客户公开其他错误。
* 错误修复：如果iframe的HTML页面来自与父窗口的HTML页面不同的子域，则在iframe中运行SDK会导致错误。

## 版本2.2.0 - 2020年10月

* 错误修复：选择加入对象在以下情况下阻止Alloy进行调用： `idMigrationEnabled` 是 `true`.
* 错误修复：使Alloy知道应返回个性化选件的请求，以防止出现闪烁问题。

## 版本2.1.0 - 2020年8月

* 删除 `syncIdentity` 命令并支持将这些ID传递到 `sendEvent` 命令。
* 支持IAB 2.0 Consent Standard。
* 支持在中传递其他ID `setConsent` 命令。
* 支持覆盖 `datasetId` 在 `sendEvent` 命令。
* 支持Alloy显示器([了解更多](https://github.com/adobe/alloy/wiki/Monitoring-Hooks))
* 通过 `environment: browser` 在实施详细信息上下文数据中。
