---
title: 上下文
description: 自动收集设备、环境或位置数据。
exl-id: 911cabec-2afb-4216-b413-80533f826b0e
source-git-commit: c2564f1b9ff036a49c9fa4b9e9ffbdbc598a07a8
workflow-type: tm+mt
source-wordcount: '821'
ht-degree: 5%

---

# `context`

`context`属性是一个字符串数组，用于确定Web SDK可自动收集的内容。 虽然此数据可以带来巨大价值，但忽略某些此类数据可能会有助益，这样您就可以遵守组织的隐私政策。

## 上下文关键字和XDM元素

如果您包含给定的上下文关键词，则Web SDK会自动填充其所有关联的XDM元素。 如果要在允许其他元素的同时忽略特定XDM元素，可以使用[`onBeforeEventSend`](onbeforeeventsend.md)清除值。 如果您在一个页面上发送多个事件，则Web SDK会在每`SendEvent`调用中包含这些字段。

### Web

`"web"`关键字收集有关当前页面的信息。

| 维度 | 描述 | XDM 路径 | 示例值 |
| --- | --- | --- | --- |
| Page URL | 当前页面的URL。 | `xdm.web.webPageDetails.URL` | `https://example.com/index.html` |
| 反向链接URL | 访问的上一个页面的URL。 | `xdm.web.webReferrer.URL` | `http://example.org/linkedpage.html` |

### 设备

`"device"`关键字收集有关用户设备的信息。

| 维度 | 描述 | XDM 路径 | 示例值 |
| --- | --- | --- | --- |
| 屏幕高度 | 屏幕的高度（像素）。 | `xdm.device.screenHeight` | `900` |
| 屏幕宽度 | 屏幕的宽度（像素）。 | `xdm.device.screenWidth` | `1440` |
| 屏幕方向 | 屏幕的方向。 | `xdm.device.screenOrientation` | `landscape`或`portrait` |

### 环境

`"environment"`关键字收集有关用户浏览器的信息。

| 维度 | 描述 | XDM 路径 | 示例值 |
| --- | --- | --- | --- |
| 环境类型 | 体验通过哪种环境浮现。 Web SDK始终将此字段设置为`browser`。 | `xdm.environment.type` | `browser` |
| 视区高度 | 浏览器内容区域的高度（像素）。 | `xdm.environment.browserDetails.viewportHeight` | `679` |
| 视区宽度 | 浏览器内容区域的宽度（像素）。 | `xdm.environment.browserDetails.viewportWidth` | `642` |

### 地标上下文

`"placeContext"`关键字收集有关用户位置的信息。

| 维度 | 描述 | XDM 路径 | 示例值 |
| --- | --- | --- | --- |
| 本地时间 | 以简化的扩展[ISO 8601](https://datatracker.ietf.org/doc/html/rfc3339#section-5.6)格式表示的最终用户的本地时间戳。 | `xdm.placeContext.localTime` | `YYYY-08-07T15:47:17.129-07:00` |
| 本地时区偏移 | 用户从GMT偏移的分钟数。 | `xdm.placeContext.localTimezoneOffset` | `360` |
| 国家/地区代码 | 最终用户的国家/地区代码。 | `xdm.placeContext.geo.countryCode` | `US` |
| 省/市/自治区 | 最终用户的省/市/自治区代码。 | `xdm.placeContext.geo.stateProvince` | `CA` |
| 纬度 | 最终用户位置的纬度。 | `xdm.placeContext.geo._schema.latitude` | `37.3307447` |
| 经度 | 最终用户位置的经度。 | `xdm.placeContext.geo._schema.longitude` | `-121.8945965` |

### 时间戳

`"timestamp"`关键字收集有关事件时间戳的信息。 此上下文始终包含在内，无法删除。

| 维度 | 描述 | XDM 路径 | 示例值 |
| --- | --- | --- | --- |
| 事件的时间戳 | 以简化的扩展[ISO 8601](https://datatracker.ietf.org/doc/html/rfc3339#section-5.6)格式表示的最终用户的UTC时间戳。 | `xdm.timestamp` | `YYYY-08-07T22:47:17.129Z` |

### 实施详细信息

`implementationDetails`关键字收集有关用于收集事件的SDK版本的信息。

| 维度 | 描述 | XDM 路径 | 示例值 |
| --- | --- | --- | --- |
| 名称 | 软件开发工具包(SDK)标识符。 此字段使用URI来改进由不同软件库提供的标识符之间的唯一性。 | `xdm.implementationDetails.name` | 使用独立库时，值为`https://ns.adobe.com/experience/alloy`。 当库用作标记扩展的一部分时，值为`https://ns.adobe.com/experience/alloy+reactor`。 |
| 版本 | 软件开发工具包(SDK)版本。 | `xdm.implementationDetails.version` | 使用独立库时，该值为库版本。 当库用作标记扩展的一部分时，该值为库版本和使用`+`联接的标记扩展版本。 例如，如果库版本为`2.1.0`，而标记扩展版本为`2.1.3`，则值将为`2.1.0+2.1.3`。 |
| 环境 | 收集数据的环境。 使用JavaScript库时，此字段始终设置为`browser`。 | `xdm.implementationDetails.environment` | `browser` |

### 高熵客户端提示 {#high-entropy-client-hints}

`"highEntropyUserAgentHints"`关键字收集有关用户设备的详细信息。 此数据包含在发送到Adobe的请求的HTTP标头中。 数据到达Edge网络后，XDM对象填充其各自的XDM路径。 如果您在`sendEvent`调用中设置相应的XDM路径，则该路径优先于HTTP标头值。

如果在[配置数据流](/help/datastreams/configure.md)时使用设备查找，则可以清除数据，以支持设备查找值。 某些客户端提示字段和设备查找字段不能存在于同一点击中。

| 属性 | 描述 | HTTP标头 | XDM 路径 | 示例 |
| --- | --- | --- | --- | --- |
| 操作系统版本 | 操作系统的版本。 | `Sec-CH-UA-Platform-Version` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.platformVersion` | `10.15.7` |
| 架构 | 底层CPU架构。 | `Sec-CH-UA-Arch` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.architecture` | `x86` |
| 设备型号 | 使用的设备的名称。 | `Sec-CH-UA-Model` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.model` | `Intel Mac OS X 10_15_7` |
| 位数 | 基础CPU架构支持的位数。 | `Sec-CH-UA-Bitness` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.bitness` | `64` |
| 浏览器供应商 | 创建浏览器的公司。 低熵提示`Sec-CH-UA`也收集此元素。 | `Sec-CH-UA-Full-Version-List` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.vendor` | `Google` |
| 浏览器名称 | 使用的浏览器。 低熵提示`Sec-CH-UA`也收集此元素。 | `Sec-UA-Full-Version-List` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.brand` | `Chrome` |
| 浏览器版本 | 浏览器的重要版本。 低熵提示`Sec-CH-UA`也收集此元素。 不会自动收集确切的浏览器版本。 | `Sec-UA-Full-Version-List` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.version` | `105` |

有关详细信息，请参阅[用户代理客户端提示](/help/collection/use-cases/client-hints.md)。

运行`context`命令时设置`configure`字符串数组。 如果在配置SDK时省略此属性，则默认情况下将收集除`"highEntropyUserAgentHints"`之外的所有上下文信息。 如果要收集高熵客户端提示，或者要从数据收集中忽略其他上下文信息，请设置此属性。 字符串可以按任意顺序包含。

>[!NOTE]
>
>如果要收集所有上下文信息，包括高熵客户端提示，则必须在`context`数组字符串中包含每个值。 默认`context`值省略`highEntropyUserAgentHints`，如果您设置`context`属性，则任何省略的值都不会收集数据。

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  context: ["web", "device", "environment", "placeContext", "highEntropyUserAgentHints"]
});
```

## 使用Web SDK标记扩展收集上下文信息

请参阅Web SDK标记扩展文档中的数据收集配置设置下的[上下文设置](/help/tags/extensions/client/web-sdk/configure/data-collection.md#context-settings)。
