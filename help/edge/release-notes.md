---
title: Adobe Experience Platform Web SDK 发行说明
description: Adobe Experience Platform Web SDK 最新发行说明。
keywords: Adobe Experience Platform Web SDK；平台Web SDK;Web SDK；发行说明；
exl-id: efd4e866-6a27-4bd5-af83-4a97ca8adebd
source-git-commit: f5d3c5911357d4b76e4d38564bf637e2549469d6
workflow-type: tm+mt
source-wordcount: '771'
ht-degree: 4%

---

# 发行说明

## 2.6.4版 — 2021年9月7日

* 修复了应用于`head`元素的设置HTML Adobe Target操作替换整个`head`内容的问题。 现在，对`head`元素应用的HTML操作进行了更改，以附加HTML。

## 2.6.3版 — 2021年8月16日

* 修复了非公共用途对象通过`configure`命令中已解析的promise公开的问题。

## 2.6.2版 — 2021年8月4日

* 修复了即使未访问`result.decisions`属性，`result.decisions`（由`sendEvent`命令提供）的弃用警告也会记录到控制台的问题。 访问`result.decisions`属性时不会记录任何警告，但该属性仍被弃用。

## 2.6.1版 — 2021年7月29日

* 修复了在对没有个性化内容的单页应用程序视图进行个性化渲染时会引发错误，并导致从`sendEvent`命令返回的promise被拒绝的问题。

## 2.6.0版 — 2021年7月27日

* 在`sendEvent`已解析的承诺中提供更多个性化内容，包括Adobe Target响应令牌。 执行`sendEvent`命令时，将返回一个promise，该promise最终通过包含从服务器接收的信息的`result`对象进行解析。 以前，此结果对象包含名为`decisions`的属性。 此`decisions`属性已弃用。 添加了新属性`propositions`。 此新属性为客户提供了对更多个性化内容的访问权限，这些内容包括[响应令牌](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/accessing-response-tokens.html)。

## 2.5.0版 — 2021年6月

* 添加了对重定向个性化选件的支持。
* 自动收集的作为负值的视区宽度和高度将不再发送到服务器。
* 当通过从`onBeforeEventSend`回调返回`false`来取消事件时，将记录一条消息。
* 修复了多个事件中包含针对单个事件的特定XDM数据段的问题。

## 2.4.0版 — 2021年3月

* SDK现在可以[作为npm包](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/installing-the-sdk.html?lang=zh-Hans)安装。
* 在[配置默认同意](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#default-consent)时添加了对`out`选项的支持，该选项会丢弃所有事件直到收到同意（现有的`pending`选项会将事件排入队列，并在收到同意后发送它们）。
* [onBeforeEventSend回调](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#onbeforeeventsend)现在可用于阻止发送事件。
* 现在，在发送有关呈现或单击的个性化内容的事件时，会使用XDM架构字段组，而不是`meta.personalization`。
* 现在， [getIdentity命令](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html#retrieving-the-visitor-id)会在标识旁边返回边缘区域ID。
* 从服务器收到的警告和错误已得到改进，并以更适当的方式处理。
* 添加了对[Adobe的“同意2.0”标准](https://experienceleague.adobe.com/docs/experience-platform/edge/consent/supporting-consent.html?communicating-consent-preferences-via-the-adobe-standard)的支持。
* 同意首选项在收到后将经过哈希处理并存储在本地存储中，以便CMP、Platform Web SDK和Platform Edge Network之间实现优化集成。 如果您收集同意首选项，我们现在建议您在每次加载页面时调用`setConsent`。
* 添加了两个[监视挂接](https://github.com/adobe/alloy/wiki/Monitoring-Hooks)、`onCommandResolved`和`onCommandRejected`。
* 错误修复：当用户导航到新的单页应用程序视图、返回到原始视图并单击符合转化条件的元素时，个性化交互通知事件将包含有关同一活动的重复信息。
* 错误修复：如果SDK发送的第一个事件将`documentUnloading`设置为`true`，则将使用[`sendBeacon`](https://developer.mozilla.org/zh-CN/docs/Web/API/Navigator/sendBeacon)来发送该事件，从而导致有关未建立身份的错误。

## 2.3.0版 — 2020年11月

* 添加了nonce支持，以允许更严格的内容安全策略。
* 为单页应用程序添加了个性化支持。
* 改进了与可能覆盖`window.console` API的其他页面上JavaScript代码的兼容性。
* 错误修复：将`documentUnloading`设置为`true`或自动跟踪链接点击时，未使用`sendBeacon`。
* 错误修复：如果锚点元素包含HTML内容，则不会自动跟踪链接。
* 错误修复：某些包含只读`message`属性的浏览器错误处理不当，导致向客户显示其他错误。
* 错误修复：如果iframe的HTML页面来自与父窗口的HTML页面不同的子域，则在iframe中运行SDK会导致错误。

## 2.2.0版 — 2020年10月

* 错误修复：当`idMigrationEnabled`为`true`时，选择加入对象阻止Alloy进行调用。
* 错误修复：使Alloy了解应返回个性化选件以防止出现闪烁问题的请求。

## 2.1.0版 — 2020年8月

* 删除`syncIdentity`命令，并支持在`sendEvent`命令中传递这些ID。
* 支持IAB 2.0 Consent Standard。
* 支持在`setConsent`命令中传递其他ID。
* 支持在`sendEvent`命令中覆盖`datasetId`。
* 支持合金显示器（[阅读更多](https://github.com/adobe/alloy/wiki/Monitoring-Hooks)）
* 在实施详细信息上下文数据中传递`environment: browser`。
