---
title: Adobe Experience Platform Web SDK 发行说明
description: Adobe Experience Platform Web SDK 最新发行说明。
keywords: Adobe Experience Platform Web SDK；Experience Platform Web SDK；Web SDK；发行说明；
exl-id: efd4e866-6a27-4bd5-af83-4a97ca8adebd
source-git-commit: 21140a6ff4f34db213032dd600d4099a5459e31d
workflow-type: tm+mt
source-wordcount: '2502'
ht-degree: 2%

---


# Web SDK发行说明

本文档介绍Adobe Experience Platform Web SDK的发行说明。
有关Web SDK标记扩展的最新发行说明，请参阅[Web SDK标记扩展发行说明](../tags/extensions/client/web-sdk/web-sdk-ext-release-notes.md)。

## 2.28.1版 — 2025年7月31日

**修复和改进**

- 修复了阻止自定义内部版本运行的问题。

## 2.28.0版 — 2025年7月24日

**新增功能**

- 添加了对Adobe Journey Optimizer取消资格规则的支持。

**修复和改进**

- 修复了[Media Analytics跟踪器](commands/getmediaanalyticstracker.md)中的一个错误，该错误导致媒体对象的`length`属性错误地接受无效数据类型。
- 改进了[身份管理](identity/overview.md)错误处理，以便在身份查找失败时正确处理promise拒绝。
- 解决了包含HTML内容项的[个性化内容](personalization/rendering-personalization-content.md)无法呈现的问题，该问题导致与缺少`renderStatusHandler`相关的错误。
- 修复了Activity Map [URL集合](commands/configure/clickcollectionenabled.md)以正确处理非HTTP URL。

**已知问题**

- 使用[的](/help/web-sdk/install/create-custom-build.md)自定义内部版本`npx @adobe/alloy`进程当前在版本2.28.0中无法按预期运行。所有组件都包含在生成的内部版本中，与选定的模块无关。 此问题不会影响CDN上可用的标准JavaScript文件。 正在进行修复。

## 2.27.0版 — 2025年5月20日

**修复和改进**

- 修复了应用程序内消息中自定义样式应用不正确的问题。
- 更改了事件历史记录的格式。 这将导致在删除旧历史记录数据时重新显示应用程序内消息和内容卡。
- 修复了在SPA用例中重新应用建议的问题。
- 修复了对影子DOM元素进行点击跟踪的问题。

## 版本2.26.0 - 2025年3月5日

**新增功能**

- 您现在可以使用Web SDK NPM包创建自定义Web SDK内部版本，并仅选择所需的库组件。 这可以减小库大小并优化加载时间。 请参阅有关如何使用NPM包[创建自定义Web SDK内部版本的文档](install/create-custom-build.md)。
- [`getIdentity`](commands/getidentity.md)命令现在会自动直接从`kndctr`身份Cookie中读取ECID。 如果您使用`getIdentity`命名空间调用`ECID`，并且已存在身份Cookie，则Web SDK不再向Edge Network发出获取身份的请求。 现在，它会从Cookie中读取身份。

**修复和改进**

- 修复了在发送`getIdentity`调用后`collect`命令未返回标识的问题。
- 修复了个性化重定向导致内容在重定向发生之前闪烁的问题。

## 版本2.25.0 - 2025年1月23日

**已修复和改进**

- 向`setDebug`命令添加了选项验证。
- 添加了一个警告，在禁用单击收集时配置`onBeforeLinkClickSend`函数或下载链接限定符。
- 修复了呈现的建议未包含在显示通知中的问题。

**新增功能**

- 在启用了第三方Cookie并阻止对adobedc.demdex.net的请求时，对配置的Edge域实施了回退。

## 版本2.24.1 - 2024年12月6日

**已修复和改进**

- 解决了与[Adobe Experience Platform规则引擎](https://github.com/adobe/aepsdk-rulesengine-typescript/)相关的依赖项问题，该问题会导致某些客户集成中出现错误。 Web SDK现在需要[Adobe Experience Platform Rules Engine](https://github.com/adobe/aepsdk-rulesengine-typescript/) 2.0.3或更高版本。

## 版本2.24.0 - 2024年10月31日

**新增功能**

- 现在启动媒体会话时支持[数据流覆盖](../datastreams/overrides.md)。

- 在[`onContentRendering`](monitoring-hooks.md#onContentRendering)监控挂接中添加了对Adobe Target响应令牌的支持。

**修复和改进**

- 当返回多个应用程序内消息时，只会显示具有最高优先级的消息。 其它则被记录为隐含。
- 空数据流覆盖不再发送到Edge Network，从而减少与服务器端路由配置的潜在冲突。
- 重命名了以下日志消息组件名称，以与其他Adobe SDK保持一致：
   - `DecisioningEngine`已重命名为`RulesEngine`
   - `LegacyMediaAnalytics`已重命名为`MediaAnalyticsBridge`
   - `Privacy`已重命名为`Consent`
- 修复了通过[`applyPropositions`](../web-sdk/commands/applypropositions.md)呈现默认内容项时发生的错误。
- 修复了Adobe Target移动和调整操作大小时的CSS错误。
- 已从`machineLearning`响应中删除[`sendEvent`](../web-sdk/commands/sendevent/overview.md)键。

## 版本2.23.0 - 2024年9月19日

**新增功能**

- 在[getIdentity](identity/overview.md#tracking-coreid-web-sdk)命令中添加了对请求[核心ID](commands/getidentity.md#get-identity-using-the-web-sdk-javascript-library)的支持。

**修复和改进**

- 修复了在本地运行Web SDK时无法正确写入Cookie的问题。

## 版本2.22.0 - 2024年8月22日

**新增功能**

- 添加了对个性化监控挂接的支持。

**修复和改进**

- 删除了对Internet Explorer的支持，将库gzip大小减少了9%。
- 修复了在调用`onInstanceConfigured`监视器挂接时未初始化Activity Map链接详细信息的问题。
- 修复了Cookie目标未设置为正确路径的问题。
- 修复了调用具有的客户问题。
- 修复了`adobe_mc`参数中的无效URL编码导致[sendEvent](commands/sendevent/overview.md)调用失败的问题。

## 2.21.1版 — 2024年7月18日

**修复和改进**

- 修复了使用NPM库时的生成错误。

## 2.21.0版 — 2024年7月16日

**新增功能**

- 添加了对自动建议交互跟踪的支持。
- 添加了提供alloy.js文件的自定义构建脚本。
- 通过ActivityMap和事件分组支持改进了点击收集。

## 2.20.0版 — 2024年5月21日

**新增功能**

- 添加了对[流媒体收藏集](../web-sdk/commands/configure/streamingmedia.md)的支持。

**修复和改进**

- 修复了在选择禁用同意时，导致默认内容被预隐藏代码片段隐藏的错误。

## 版本2.19.2 - 2024年1月10日

**修复和改进**

- 修复了标识错误正在掩蔽其他错误，并将标识错误更改为警告的问题。
- 修复了当`renderDecisions`设置为`false`的页面顶部调用时，页面底部调用绝不会发送的问题。
- 修复了在存在多个`adobe_mc`查询字符串参数时，Web SDK无法读取跨域标识的问题。

## 版本 2.19.1 - 2023 年 11 月 10 日

**修复和改进**

- 修复了从`sendEvent`调用返回的建议数组始终为空的问题。

## 版本2.19.0 - 2023年11月1日

**新增功能**

- 添加了对从Adobe Journey Optimizer呈现应用程序内消息的支持。
- 添加了对[页面顶部和底部事件](use-cases/top-bottom-page-events.md)的支持。
- 向[`defaultPersonalizationEnabled`](commands/sendevent/personalization.md)命令添加了`sendEvent`选项以控制请求页面范围的范围和默认表面。

**修复和改进**

- 在呈现多种类型的个性化时，组合的个性化会显示多个事件。
- 修复了单页面应用程序视图名称区分大小写的问题。
- 修复了影子DOM个性化优惠选择器的问题。

## 2.18.0版 — 2023年7月31日

**新增功能**

- 添加了对数据流ID[的每命令](../datastreams/overrides.md)覆盖的支持。

**修复和改进**

- 修复了由于域是查询的一部分而导致退出链接不符合条件的问题。
- 在Web SDK配置中弃用`edgeConfigId`而支持`datastreamId`。

## 2.17.0版 — 2023年5月17日

**修复和改进**

- Web SDK现在对Audience Manager Cookie目标值进行编码，类似于[Data Integration Library (DIL)](https://experienceleague.adobe.com/docs/audience-manager/user-guide/dil-api/dil-overview.html?lang=zh-Hans)。

## 版本2.16.0 - 2023年4月25日

**新增功能**

- 添加了对[数据流配置覆盖](../datastreams/overrides.md)的支持。

## 版本2.15.0 - 2023年3月30日

**新增功能**

- 添加了对[`onBeforeLinkClickSend`](/help/web-sdk/commands/configure/onbeforelinkclicksend.md)链接点击回调的支持。
- 添加了对Adobe Journey Optimizer点击跟踪的支持。

**修复和改进**

- 现在，链接收藏集包含链接名称和访客区域。
- 移除了失败URL目标的控制台错误。

## 版本2.14.0 - 2023年1月25日

- (Beta)添加了对Adobe Journey Optimizer表面和建议的支持。

**修复和改进**

- 修复了Adobe Target VEC自定义代码操作的一个问题，该问题导致代码被插入到[!DNL at.js]以外的其他位置。
- 修复了在某些边缘情况下，对Edge Network的请求未正确设置“referer”标头的问题。
- 修复了[用户代理客户端提示](/help/web-sdk/use-cases/client-hints.md)属性可能设置为不正确类型的问题。
- 修复了`placeContext.localTime`与架构不匹配的问题。

## 版本2.13.1 - 2022年10月13日

- 修复了在配置后定义window.Visitor时访客迁移不起作用的问题。 当使用Adobe标记运行时，这个问题尤为突出。
- 修复了在某些环境中将`device.screenWidth`和`device.screenHeight`填充为字符串的问题。

## 版本2.13.0 - 2022年9月28日

**新增功能**

- 添加了对[Page by Page Full Migration](home.md#migrating-to-web-sdk)的支持。 现在，当访客在at.js和Web SDK页面之间移动时，将保留Adobe Target配置文件。
- 添加了对[高熵用户代理客户端提示](/help/web-sdk/use-cases/client-hints.md)的可配置支持。
- 添加了对[`applyResponse`](/help/web-sdk/commands/applyresponse.md)命令的支持。 这样可通过[Edge Network API](https://developer.adobe.com/data-collection-apis/docs/api/)实现混合个性化。
- QA模式链接现在可以在多个页面中使用。

**修复和改进**

- 修复了在禁用链接跟踪时个性化点击跟踪量度未更新的问题。
- 更新了在指定未知选项时引发验证错误的命令。
- 自动发送显示和交互个性化事件时现在会填充`_experience.decisioning.propositionEventType`属性。
- 为`getIdentity`命令添加了重复的命名空间验证。
- 为`sendEvent`命令添加了重复的决定范围验证。

## 版本2.12.0 - 2022年6月29日

- 将对Edge Network的请求更改为使用`cluster` Cookie位置提示作为URL的一部分。 这可确保会话期间更改其位置（例如，通过VPN或带着移动设备开车等）的用户点击同一边缘并具有相同的个性化配置文件。
- 在getLibraryInfo命令响应中字符串化已配置的函数。

## 版本2.11.0 - 2022年6月13日

**新增功能**

- 现在，通过在移动应用程序和移动Web内容之间以及跨域共享访客ID，您可以更准确地提供个性化体验。 有关详细信息，请参阅[专用文档](identity/id-sharing.md)。
- 您现在可以将[!DNL Adobe Target]中的一系列建议渲染或执行到单页应用程序中，而无需增加Analytics量度。 这减少了报告错误，并提高了分析准确性。 有关详细信息，请参阅[专用文档](personalization/rendering-personalization-content.md#applypropositions)。
- 向`getLibraryInfo`命令添加了其他信息，包括可用命令和实例的最终配置。

**修复和改进**

- 更新了Cookie设置以在`sameSite="none"`页面上使用`secure`和[!DNL HTTPS]标记。
- 修复了在使用`eq`伪选择器时个性化内容未正确应用的问题。
- 修复了`localTimezoneOffset`可能无法通过Experience Platform验证的问题。

## 版本2.10.1 - 2022年5月3日

- 修复了为ID同步和区段目标创建多个永久iframe的问题。

## 版本2.10.0 - 2022年4月22日

- 对所有ID同步和区段目标使用永久性iframe。
- 修复了合并的量度建议在`sendEvent`结果中重复的问题。

## 版本2.9.0 - 2022年3月10日

- 添加了对跟踪[!DNL control (default)]Adobe Target体验的支持。
- 优化了单页应用程序的查看 — 更改事件。 现在，在呈现个性化体验时，显示通知包含在查看 — 更改事件中。
- 已移除不存在`eventType`时的控制台警告。
- 修复了在缓存中请求或检索体验时仅从`propositions`命令返回`sendEvent`属性的问题。 `propositions`属性现在将始终定义为数组。
- 修复了从Edge Network返回错误时，未显示隐藏容器的问题。
- 修复了Adobe Target中未计算interact事件的问题。 通过将视图名称添加到XDM的web.webPageDetails.viewName中修复了此问题。
- 修复控制台消息中损坏的文档链接。

## 版本2.8.0 - 2022年1月19日

- 支持个性化的影子DOM选择器。
- 重命名了个性化事件类型。 （`display`和`click`成为`decisioning.propositionDisplay`和`decisioning.propositionInteract`）
- 修复了以下问题：带有内联脚本标记的HTML选件将脚本标记两次添加到页面中，即使脚本只运行一次。

## 版本 2.7.0 - 2021 年 10 月 26 日

- 在`sendEvent`的返回值中公开来自Edge Network的其他信息，包括`inferences`和`destinations`。 由于这些功能当前正在作为Beta的一部分推出，因此这些属性的格式可能会发生更改。

## 版本2.6.4 - 2021年9月7日

- 修复了应用于`head`元素的设置HTML Adobe Target操作将替换整个`head`内容的问题。 现在，将应用于`head`元素的HTML操作更改为附加HTML。

## 版本2.6.3 - 2021年8月16日

- 修复了通过`configure`命令的已解析承诺公开非公共用途对象的问题。

## 版本2.6.2 - 2021年8月4日

- 修复了以下问题：即使未访问`result.decisions`属性，`sendEvent`的弃用（由`result.decisions`命令提供）警告也会记录到控制台。 访问`result.decisions`属性时不会记录任何警告，但该属性仍被弃用。

## 版本2.6.1 - 2021年7月29日

- 修复了呈现没有个性化内容的单页应用程序视图的个性化设置会引发错误并导致`sendEvent`命令返回的承诺被拒绝的问题。

## 2.6.0版 — 2021年7月27日

- 在`sendEvent`已解决的承诺中提供更多的个性化内容，包括Adobe Target响应令牌。 执行`sendEvent`命令时，将返回一个promise，该承诺最终将由包含从服务器接收的信息的`result`对象解析。 以前，此结果对象包含一个名为`decisions`的属性。 该`decisions`属性已被弃用。 已添加新属性`propositions`。 此新属性使客户能够访问更多个性化内容，包括[响应令牌](/help/web-sdk/personalization/adobe-target/accessing-response-tokens.md)。

## 版本2.5.0 - 2021年6月

- 添加了对重定向个性化选件的支持。
- 自动收集的负值视区宽度和高度将不再发送到服务器。
- 现在，当通过从`false`回调返回`onBeforeEventSend`而取消事件时，将记录一条消息。
- 修复了用于单个事件的特定XDM数据片段包含在多个事件中的问题。

## 版本2.4.0 - 2021年3月

- SDK现在可以作为[NPM包](/help/web-sdk/install/npm.md)安装。
- 在`out`配置默认同意[时添加了对](/help/web-sdk/commands/configure/defaultconsent.md)选项的支持，默认同意会丢弃所有事件，直到收到同意为止（现有`pending`选项将事件排入队列，并在收到同意后发送它们）。
- [`onBeforeEventSend`](/help/web-sdk/commands/configure/onbeforeeventsend.md)回调现在可用于阻止发送事件。
- 在发送有关正在呈现或单击的个性化内容的事件时，现在使用XDM架构字段组而不是`meta.personalization`。
- [`getIdentity`](/help/web-sdk/commands/getidentity.md)命令现在会随身份一起返回边缘区域ID。
- 从服务器收到的警告和错误已得到改进，并以更合适的方式进行处理。
- 为[`setConsent`](/help/web-sdk/commands/setconsent.md)命令添加了对Adobe Consent 2.0标准的支持。
- 收到同意首选项后，将对首选项进行哈希处理并将其存储在本地存储中，以优化CMP、Experience Platform Web SDK和Experience Platform Edge Network之间的集成。 如果您正在收集同意首选项，我们现在鼓励您在每次加载页面时调用`setConsent`。
- 已添加两个[监视挂接](https://github.com/adobe/alloy/wiki/Monitoring-Hooks)、`onCommandResolved`和`onCommandRejected`。
- 错误修复：当用户导航到新的单页应用程序视图、返回原始视图并单击符合转化条件的元素时，Personalization交互通知事件将包含有关相同活动的重复信息。
- 错误修复：如果SDK发送的第一个事件将`documentUnloading`设置为`true`，则将使用[`sendBeacon`](https://developer.mozilla.org/en-US/docs/Web/API/Navigator/sendBeacon)发送该事件，从而导致有关未建立标识的错误。

## 版本2.3.0 - 2020年11月

- 添加了nonce支持，以允许实施更严格的内容安全策略。
- 添加了对单页应用程序的个性化支持。
- 改进了与其他可能覆盖`window.console` API的页面上JavaScript代码的兼容性。
- 错误修复： `sendBeacon`设置为`documentUnloading`或自动跟踪链接点击时，未使用`true`。
- 错误修复：如果锚点元素包含HTML内容，则不会自动跟踪链接。
- 错误修复：某些包含只读`message`属性的浏览器错误未得到适当处理，从而导致向客户公开其他错误。
- 错误修复：如果iframe的SDK页面来自与父窗口的HTML页面不同的子域，则在iframe中运行HTML会导致错误。

## 版本2.2.0 - 2020年10月

- 错误修复：当`idMigrationEnabled`为`true`时，选择加入对象阻止Web SDK进行调用。
- 错误修复：使Web SDK知道应返回个性化选件的请求，以防止出现闪烁问题。

## 版本2.1.0 - 2020年8月

- 删除`syncIdentity`命令并支持在`sendEvent`命令中传递这些ID。
- 支持IAB 2.0 Consent Standard。
- 支持在`setConsent`命令中传递其他ID。
- 支持覆盖`datasetId`命令中的`sendEvent`。
- 支持监视挂接（[了解更多](https://github.com/adobe/alloy/wiki/Monitoring-Hooks)）
- 在实施详细信息上下文数据中传递`environment: browser`。
