---
title: Adobe Experience Platform Web SDK 发行说明
description: Adobe Experience Platform Web SDK 最新发行说明。
keywords: Adobe Experience Platform Web SDK;Platform Web SDK;Web SDK；发行说明；
exl-id: efd4e866-6a27-4bd5-af83-4a97ca8adebd
translation-type: tm+mt
source-git-commit: ab0798851e5f2b174d9f4241ad64ac8afa20a938
workflow-type: tm+mt
source-wordcount: '502'
ht-degree: 5%

---

# 发行说明

## 版本2.4.0,2021年3月

* SDK现在可以[作为npm包](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/installing-the-sdk.html)安装。
* 增加了对[配置默认同意](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#default-consent)时`out`选项的支持，该选项将删除所有事件，直到收到同意(现有`pending`选项将事件排队，并在收到同意后发送它们)。
* [onBeforeEventSend回调](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#onbeforeeventsend)现在可用于阻止发送事件。
* 现在，在发送有关呈现或单击的个性化内容的事件时，使用XDM模式字段组而不是`meta.personalization`。
* 现在，[getIdentity命令](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html#retrieving-the-visitor-id)将返回边缘区域ID和标识。
* 从服务器收到的警告和错误已得到改进，并以更适当的方式处理。
* 增加了对[Adobe的“同意2.0”标准](https://experienceleague.adobe.com/docs/experience-platform/edge/consent/supporting-consent.html?communicating-consent-preferences-via-the-adobe-standard)的支持。
* 同意首选项在收到后会经过散列处理并存储在本地存储中，以便在CMP、Platform Web SDK和Platform Edge Network之间实现优化集成。 如果您正在收集同意首选项，我们现在建议您在每次页面加载时调用`setConsent`。
* 添加了两个[监视挂接](https://github.com/adobe/alloy/wiki/Monitoring-Hooks)、`onCommandResolved`和`onCommandRejected`。
* 错误修复：个性化交互通知事件将包含有关同一活动的重复信息，当用户导航到新的单页应用程序视图，返回到原始视图，并单击某个符合转换条件的元素时。
* 错误修复：如果SDK发送的第一个事件的`documentUnloading`设置为`true`，则将使用[`sendBeacon`](https://developer.mozilla.org/zh-CN/docs/Web/API/Navigator/sendBeacon)发送事件，从而导致有关未建立身份的错误。

## 版本2.3.0,2020年11月

* 增加了一次性支持，以允许更严格的内容安全策略。
* 增加了对单页应用程序的个性化支持。
* 改进了与可能覆盖`window.console` API的其他页面JavaScript代码的兼容性。
* 错误修复：将`documentUnloading`设置为`true`或自动跟踪链接点击时，未使用`sendBeacon`。
* 错误修复：如果锚点元素包含HTML内容，则不会自动跟踪链接。
* 错误修复：某些包含只读`message`属性的浏览器错误未得到适当处理，导致向客户公开了其他错误。
* 错误修复：如果iframe的HTML页来自父窗口的HTML页以外的子域，则在iframe中运行SDK将导致错误。

## 版本2.2.0,2020年10月

* 错误修复：当`idMigrationEnabled`为`true`时，Opt-in对象阻止Alloy发出调用。
* 错误修复：让Alloy了解应返回个性化优惠以防止出现闪烁问题的请求。

## 版本2.1.0,2020年8月

* 删除`syncIdentity`命令并支持在`sendEvent`命令中传递这些ID。
* 支持IAB 2.0同意标准。
* 支持在`setConsent`命令中传递其他ID。
* 支持覆盖`sendEvent`命令中的`datasetId`。
* 支持合金监视器（[阅读更多](https://github.com/adobe/alloy/wiki/Monitoring-Hooks)）
* 在实现详细信息上下文数据中传递`environment: browser`。
