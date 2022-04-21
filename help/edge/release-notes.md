---
title: Adobe Experience Platform Web SDK 发行说明
description: Adobe Experience Platform Web SDK 最新发行说明。
keywords: Adobe Experience Platform Web SDK；平台Web SDK;Web SDK；发行说明；
exl-id: efd4e866-6a27-4bd5-af83-4a97ca8adebd
source-git-commit: 22ae7d206d4393719352232dc254d7669ca667bd
workflow-type: tm+mt
source-wordcount: '1001'
ht-degree: 3%

---

# 发行说明

## 版本2.10.0 - 2022年4月22日

* 对所有ID同步和区段目标使用永久性iframe。
* 修复了合并的量度主张在 `sendEvent` 结果。

## 2.9.0版 — 2022年3月10日

* 添加了对跟踪的支持 [!DNL control (default)] Adobe Target体验。
* 优化了单页应用程序的视图更改事件。 现在，在呈现个性化体验时，显示通知会包含在视图更改事件中。
* 删除了控制台警告，当没有 `eventType` 存在。
* 修复了 `propositions` 仅从 `sendEvent` 命令。 的 `propositions` 属性现在将始终定义为数组。
* 修复了从Adobe Experience Edge返回错误时未显示隐藏容器的问题。
* 修复了交互事件未计入Adobe Target的问题。 通过在XDM的web.webPageDetails.viewName中添加视图名称，修复了此问题。
* 修复了控制台消息中文档链接损坏的问题。

## 2.8.0版 — 2022年1月19日

* 支持用于个性化的卷影DOM选择器。
* 重命名了个性化事件类型。 (`display` 和 `click` 变成 `decisioning.propositionDisplay` 和 `decisioning.propositionInteract`)
* 修复了即使脚本只运行一次，带有内联脚本标记的HTML选件仍会将脚本标记添加两次到页面的问题。

## 2.7.0版 — 2021年10月26日

* 在的返回值中显示Experience Edge的其他信息 `sendEvent`，包括 `inferences` 和 `destinations`. 由于这些功能当前作为测试版的一部分推出，因此这些属性的格式可能会发生更改。 有关更多信息，请参阅 [跟踪事件。](fundamentals/tracking-events.md)

## 2.6.4版 — 2021年9月7日

* 修复了设置HTMLAdobe Target操作时应用于 `head` 元素正在替换 `head` 内容。 现在，设置应用于的HTML操作 `head` 元素已更改，可附加HTML。

## 2.6.3版 — 2021年8月16日

* 修复了非公共用途的对象通过 `configure` 命令。

## 2.6.2版 — 2021年8月4日

* 修复了 `result.decisions` (由 `sendEvent` 命令)将记录到控制台，即使 `result.decisions` 未访问资产。 访问 `result.decisions` 属性，但该属性仍被弃用。

## 2.6.1版 — 2021年7月29日

* 修复了在对没有个性化内容的单页应用程序视图进行个性化渲染时，会引发错误并导致从 `sendEvent` 命令。

## 2.6.0版 — 2021年7月27日

* 在 `sendEvent` 已解决的promise，包括Adobe Target响应令牌。 当 `sendEvent` 命令执行时，会返回一个promise，该promise最终通过 `result` 包含从服务器接收的信息的对象。 以前，此结果对象包含名为的属性 `decisions`. 此 `decisions` 属性已弃用。 新财产， `propositions`，已添加。 此新资产为客户提供了对更多个性化内容的访问权限，包括 [响应令牌](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/accessing-response-tokens.html).

## 2.5.0版 — 2021年6月

* 添加了对重定向个性化选件的支持。
* 自动收集的作为负值的视区宽度和高度将不再发送到服务器。
* 通过返回取消事件时 `false` 从 `onBeforeEventSend` 回调，则现在会记录一条消息。
* 修复了多个事件中包含针对单个事件的特定XDM数据段的问题。

## 2.4.0版 — 2021年3月

* SDK现在可以 [作为npm包安装](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/installing-the-sdk.html?lang=zh-Hans).
* 添加了对 `out` 选项时 [配置默认同意](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#default-consent)，在收到同意之前会丢弃所有事件(现有 `pending` 选项会将事件排入队列，并在收到同意后发送它们)。
* 的 [onBeforeEventSend回调](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#onbeforeeventsend) 现在可用于阻止发送事件。
* 现在使用XDM架构字段组，而不是 `meta.personalization` 发送有关呈现或单击的个性化内容的事件时，会向用户发送相关消息。
* 的 [getIdentity命令](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html#retrieving-the-visitor-id) 现在，将边缘区域ID与标识一起返回。
* 从服务器收到的警告和错误已得到改进，并以更适当的方式处理。
* 添加了 [Adobe的同意2.0标准](https://experienceleague.adobe.com/docs/experience-platform/edge/consent/supporting-consent.html?communicating-consent-preferences-via-the-adobe-standard).
* 同意首选项在收到后将经过哈希处理并存储在本地存储中，以便CMP、Platform Web SDK和Platform Edge Network之间实现优化集成。 如果您收集同意首选项，我们现在鼓励您调用 `setConsent` 每次加载页面时。
* 两个 [监控挂钩](https://github.com/adobe/alloy/wiki/Monitoring-Hooks), `onCommandResolved` 和 `onCommandRejected`，已添加。
* 错误修复：当用户导航到新的单页应用程序视图、返回到原始视图并单击符合转化条件的元素时，个性化交互通知事件将包含有关同一活动的重复信息。
* 错误修复：如果SDK发送的第一个事件 `documentUnloading` 设置为 `true`, [`sendBeacon`](https://developer.mozilla.org/zh-CN/docs/Web/API/Navigator/sendBeacon) 将用于发送事件，从而导致有关未建立身份的错误。

## 2.3.0版 — 2020年11月

* 添加了nonce支持，以允许更严格的内容安全策略。
* 为单页应用程序添加了个性化支持。
* 改进了与可能会覆盖的其他页面JavaScript代码的兼容性 `window.console` API。
* 错误修复： `sendBeacon` 在 `documentUnloading` 设置为 `true` 或自动跟踪链接点击时。
* 错误修复：如果锚点元素包含HTML内容，则不会自动跟踪链接。
* 错误修复：包含只读的某些浏览器错误 `message` 未正确处理属性，从而导致向客户显示其他错误。
* 错误修复：如果iFrame的HTML页面来自与父窗口的HTML页面不同的子域，则在iFrame中运行SDK会导致错误。

## 2.2.0版 — 2020年10月

* 错误修复：选择加入对象阻止Alloy在 `idMigrationEnabled` is `true`.
* 错误修复：使Alloy了解应返回个性化选件以防止出现闪烁问题的请求。

## 2.1.0版 — 2020年8月

* 删除 `syncIdentity` 命令和支持在 `sendEvent` 命令。
* 支持IAB 2.0 Consent Standard。
* 支持在 `setConsent` 命令。
* 支持覆盖 `datasetId` 在 `sendEvent` 命令。
* 支持合金显示器([了解更多](https://github.com/adobe/alloy/wiki/Monitoring-Hooks))
* 通过 `environment: browser` 在实施详细信息中，上下文数据。
