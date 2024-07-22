---
title: Adobe Experience Platform Web SDK 发行说明
description: Adobe Experience Platform Web SDK 最新发行说明。
keywords: Adobe Experience Platform Web SDK；平台Web SDK；Web SDK；发行说明；
exl-id: efd4e866-6a27-4bd5-af83-4a97ca8adebd
source-git-commit: 47cf9cdb7c59ce8459ecb8823787b5145d5f5621
workflow-type: tm+mt
source-wordcount: '1857'
ht-degree: 1%

---


# 发行说明

本文档介绍Adobe Experience Platform Web SDK的发行说明。
有关Web SDK标记扩展的最新发行说明，请参阅[Web SDK标记扩展发行说明](../tags/extensions/client/web-sdk/web-sdk-ext-release-notes.md)。

>[!IMPORTANT]
>
>Google [已宣布](https://developers.google.com/privacy-sandbox/3pcd/prepare/prepare-for-phaseout)计划在2024年下半年停止Chrome对第三方Cookie的支持。 因此，任何主要浏览器将不再支持第三方Cookie。
>
>实施此更改后，Adobe将停止对Web SDK中当前支持的`demdex` Cookie的支持。

## 2.21.1版 — 2024年7月18日

**修复和改进**

* 修复了使用NPM库时的生成错误。

## 2.21.0版 — 2024年7月16日

**新增功能**

* 添加了对自动建议交互跟踪的支持。
* 添加了提供alloy.js文件的自定义构建脚本。
* 通过ActivityMap和事件分组支持改进了点击收集。

## 2.20.0版 — 2024年5月21日

**新增功能**

* 添加了对[流媒体收藏集](../web-sdk/commands/configure/streamingmedia.md)的支持。

**修复和改进**

* 修复了在选择禁用同意时，导致默认内容被预隐藏代码片段隐藏的错误。

## 版本2.19.2 - 2024年1月10日

**修复和改进**

* 修复了标识错误正在掩蔽其他错误，并将标识错误更改为警告的问题。
* 修复了当`renderDecisions`设置为`false`的页面顶部调用时，页面底部调用绝不会发送的问题。
* 修复了在存在多个`adobe_mc`查询字符串参数时Web SDK无法读取跨域标识的问题。

## 版本2.19.1 - 2023年11月10日

**修复和改进**

* 修复了从`sendEvent`调用返回的建议数组始终为空的问题。

## 版本2.19.0 - 2023年11月1日

**新增功能**

* 添加了对从Adobe Journey Optimizer呈现应用程序内消息的支持。
* 添加了对[页面顶部和底部事件](use-cases/top-bottom-page-events.md)的支持。
* 向`sendEvent`命令添加了[`defaultPersonalizationEnabled`](commands/sendevent/personalization.md)选项以控制请求页面范围的范围和默认表面。

**修复和改进**

* 在呈现多种类型的个性化时，组合的个性化会显示多个事件。
* 修复了单页面应用程序视图名称区分大小写的问题。
* 修复了影子DOM个性化优惠选择器的问题。

## 2.18.0版 — 2023年7月31日

**新增功能**

* 添加了对数据流ID](../datastreams/overrides.md)的每命令[覆盖的支持。

**修复和改进**

* 修复了由于域是查询的一部分而导致退出链接不符合条件的问题。
* 已弃用`edgeConfigId`，在Web SDK配置中支持`datastreamId`。

## 2.17.0版 — 2023年5月17日

**修复和改进**

* Web SDK现在对Audience ManagerCookie目标值进行编码，类似于[Data Integration Library(DIL)](https://experienceleague.adobe.com/docs/audience-manager/user-guide/dil-api/dil-overview.html?lang=zh-Hans)。

## 版本2.16.0 - 2023年4月25日

**新增功能**

* 添加了对[数据流配置覆盖](../datastreams/overrides.md)的支持。

## 版本2.15.0 - 2023年3月30日

**新增功能**

* 添加了对[`onBeforeLinkClickSend`](/help/web-sdk/commands/configure/onbeforelinkclicksend.md)链接点击回调的支持。
* 添加了对Adobe Journey Optimizer点击跟踪的支持。

**修复和改进**

* 现在，链接收藏集包含链接名称和访客区域。
* 移除了失败URL目标的控制台错误。

## 版本2.14.0 - 2023年1月25日

* (Beta)添加了对Adobe Journey Optimizer表面和建议的支持。

**修复和改进**

* 修复了Adobe Target VEC自定义代码操作的一个问题，该问题导致代码被插入到[!DNL at.js]以外的其他位置。
* 修复了在某些边缘情况下，对Edge Network的请求未正确设置“referer”标头的问题。
* 修复了[用户代理客户端提示](/help/web-sdk/use-cases/client-hints.md)属性可能设置为不正确类型的问题。
* 修复了`placeContext.localTime`与架构不匹配的问题。

## 版本2.13.1 - 2022年10月13日

* 修复了在配置后定义window.Visitor时访客迁移不起作用的问题。 当使用Adobe标签运行时，这个问题尤为突出。
* 修复了在某些环境中将`device.screenWidth`和`device.screenHeight`填充为字符串的问题。

## 版本2.13.0 - 2022年9月28日

**新增功能**

* 添加了对[Page by Page Full Migration](home.md#migrating-to-web-sdk)的支持。 现在，当访客在at.js和Web SDK页面之间移动时，将保留Adobe Target配置文件。
* 添加了对[高熵用户代理客户端提示](/help/web-sdk/use-cases/client-hints.md)的可配置支持。
* 添加了对[`applyResponse`](/help/web-sdk/commands/applyresponse.md)命令的支持。 这样可通过[Edge Network服务器API](../server-api/overview.md)实现混合个性化。
* QA模式链接现在可以在多个页面中使用。

**修复和改进**

* 修复了在禁用链接跟踪时个性化点击跟踪量度未更新的问题。
* 更新了在指定未知选项时引发验证错误的命令。
* 自动发送显示和交互个性化事件时现在会填充`_experience.decisioning.propositionEventType`属性。
* 为`getIdentity`命令添加了重复的命名空间验证。
* 为`sendEvent`命令添加了重复的决定范围验证。

## 版本2.12.0 - 2022年6月29日

* 将请求更改为Edge Network以使用`cluster` Cookie位置提示作为URL的一部分。 这可确保会话期间更改其位置（例如，通过VPN或带着移动设备开车等）的用户点击同一边缘并具有相同的个性化配置文件。
* 在getLibraryInfo命令响应中字符串化已配置的函数。

## 版本2.11.0 - 2022年6月13日

**新增功能**

* 现在，通过在移动应用程序和移动Web内容之间以及跨域共享访客ID，您可以更准确地提供个性化体验。 有关详细信息，请参阅[专用文档](identity/id-sharing.md)。
* 您现在可以将[!DNL Adobe Target]中的一系列建议渲染或执行到单页应用程序中，而无需增加Analytics量度。 这减少了报告错误，并提高了分析准确性。 有关详细信息，请参阅[专用文档](personalization/rendering-personalization-content.md#applypropositions)。
* 向`getLibraryInfo`命令添加了其他信息，包括可用命令和实例的最终配置。

**修复和改进**

* 更新了Cookie设置以在[!DNL HTTPS]页面上使用`sameSite="none"`和`secure`标记。
* 修复了在使用`eq`伪选择器时个性化内容未正确应用的问题。
* 修复了`localTimezoneOffset`无法通过Experience Platform验证的问题。

## 版本2.10.1 - 2022年5月3日

* 修复了为ID同步和区段目标创建多个永久iframe的问题。

## 版本2.10.0 - 2022年4月22日

* 对所有ID同步和区段目标使用永久性iframe。
* 修复了合并的量度建议在`sendEvent`结果中重复的问题。

## 版本2.9.0 - 2022年3月10日

* 添加了对跟踪[!DNL control (default)]Adobe Target体验的支持。
* 优化了单页应用程序的查看 — 更改事件。 现在，在呈现个性化体验时，显示通知包含在查看 — 更改事件中。
* 已移除不存在`eventType`时的控制台警告。
* 修复了在缓存中请求或检索体验时仅从`sendEvent`命令返回`propositions`属性的问题。 `propositions`属性现在将始终定义为数组。
* 修复了从Edge Network返回错误时未显示隐藏容器的问题。
* 修复了Adobe Target中未计算interact事件的问题。 通过将视图名称添加到XDM的web.webPageDetails.viewName中修复了此问题。
* 修复控制台消息中损坏的文档链接。

## 版本2.8.0 - 2022年1月19日

* 支持个性化的影子DOM选择器。
* 重命名了个性化事件类型。 （`display`和`click`成为`decisioning.propositionDisplay`和`decisioning.propositionInteract`）
* 修复了具有内联脚本标记的HTML选件将脚本标记两次添加到页面的问题，即使脚本仅运行一次。

## 版本2.7.0 - 2021年10月26日

* 在来自`sendEvent`的返回值中公开来自Edge Network的其他信息，包括`inferences`和`destinations`。 由于这些功能当前正在作为Beta的一部分推出，因此这些属性的格式可能会发生更改。

## 版本2.6.4 - 2021年9月7日

* 修复了应用于`head`元素的设置HTMLAdobe Target操作将替换整个`head`内容的问题。 现在，将应用于`head`元素的HTML操作更改为附加HTML。

## 版本2.6.3 - 2021年8月16日

* 修复了通过`configure`命令的已解析承诺公开非公共用途对象的问题。

## 版本2.6.2 - 2021年8月4日

* 修复了以下问题：即使未访问`result.decisions`属性，`result.decisions`的弃用（由`sendEvent`命令提供）警告也会记录到控制台。 访问`result.decisions`属性时不会记录任何警告，但该属性仍被弃用。

## 版本2.6.1 - 2021年7月29日

* 修复了呈现没有个性化内容的单页应用程序视图的个性化设置会引发错误并导致`sendEvent`命令返回的承诺被拒绝的问题。

## 2.6.0版 — 2021年7月27日

* 在`sendEvent`已解决的承诺中提供更多的个性化内容，包括Adobe Target响应令牌。 执行`sendEvent`命令时，将返回一个promise，该承诺最终将由包含从服务器接收的信息的`result`对象解析。 以前，此结果对象包含一个名为`decisions`的属性。 该`decisions`属性已被弃用。 已添加新属性`propositions`。 此新属性使客户能够访问更多个性化内容，包括[响应令牌](/help/web-sdk/personalization/adobe-target/accessing-response-tokens.md)。

## 版本2.5.0 - 2021年6月

* 添加了对重定向个性化选件的支持。
* 自动收集的负值视区宽度和高度将不再发送到服务器。
* 现在，当通过从`onBeforeEventSend`回调返回`false`而取消事件时，将记录一条消息。
* 修复了用于单个事件的特定XDM数据片段包含在多个事件中的问题。

## 版本2.4.0 - 2021年3月

* SDK现在可以作为[NPM包](/help/web-sdk/install/npm.md)安装。
* 在[配置默认同意](/help/web-sdk/commands/configure/defaultconsent.md)时添加了对`out`选项的支持，默认同意会丢弃所有事件，直到收到同意为止（现有`pending`选项将事件排入队列，并在收到同意后发送它们）。
* [`onBeforeEventSend`](/help/web-sdk/commands/configure/onbeforeeventsend.md)回调现在可用于阻止发送事件。
* 在发送有关正在呈现或单击的个性化内容的事件时，现在使用XDM架构字段组而不是`meta.personalization`。
* [`getIdentity`](/help/web-sdk/commands/getidentity.md)命令现在会随身份一起返回边缘区域ID。
* 从服务器收到的警告和错误已得到改进，并以更合适的方式进行处理。
* 为[`setConsent`](/help/web-sdk/commands/setconsent.md)命令添加了对AdobeConsent 2.0标准的支持。
* 同意首选项在收到后将进行哈希处理并存储在本地存储中，以实现CMP、Platform Web SDK和PlatformEdge Network之间的优化集成。 如果您正在收集同意首选项，我们现在鼓励您在每次加载页面时调用`setConsent`。
* 已添加两个[监视挂接](https://github.com/adobe/alloy/wiki/Monitoring-Hooks)、`onCommandResolved`和`onCommandRejected`。
* 错误修复：当用户导航到新的单页应用程序视图、返回原始视图并单击符合转化条件的元素时，Personalization交互通知事件将包含有关相同活动的重复信息。
* 错误修复：如果SDK发送的第一个事件将`documentUnloading`设置为`true`，则将使用[`sendBeacon`](https://developer.mozilla.org/en-US/docs/Web/API/Navigator/sendBeacon)发送该事件，从而导致有关未建立标识的错误。

## 版本2.3.0 - 2020年11月

* 添加了nonce支持，以允许实施更严格的内容安全策略。
* 添加了对单页应用程序的个性化支持。
* 改进了与其他可能覆盖`window.console` API的页面上JavaScript代码的兼容性。
* 错误修复： `documentUnloading`设置为`true`或自动跟踪链接点击时，未使用`sendBeacon`。
* 错误修复：如果锚点元素包含HTML内容，则不会自动跟踪链接。
* 错误修复：某些包含只读`message`属性的浏览器错误未得到适当处理，从而导致向客户公开其他错误。
* 错误修复：如果iframe的HTML页面来自与父窗口的HTML页面不同的子域，则在iframe中运行SDK会导致错误。

## 版本2.2.0 - 2020年10月

* 错误修复：当`idMigrationEnabled`为`true`时，选择加入对象阻止Web SDK进行调用。
* 错误修复：使Web SDK知道应返回个性化选件的请求，以防止出现闪烁问题。

## 版本2.1.0 - 2020年8月

* 删除`syncIdentity`命令并支持在`sendEvent`命令中传递这些ID。
* 支持IAB 2.0 Consent Standard。
* 支持在`setConsent`命令中传递其他ID。
* 支持覆盖`sendEvent`命令中的`datasetId`。
* 支持监视挂接（[了解更多](https://github.com/adobe/alloy/wiki/Monitoring-Hooks)）
* 在实施详细信息上下文数据中传递`environment: browser`。
