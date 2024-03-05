---
title: 上下文
description: 自动收集设备、环境或位置数据。
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '684'
ht-degree: 5%

---

# `context`

此 `context` 属性是一个字符串数组，用于确定Web SDK可自动收集的内容。 虽然此数据可以带来巨大价值，但忽略某些此类数据可能会有助益，这样您就可以遵守组织的隐私政策。

## 上下文关键字和XDM元素

如果您包含给定的上下文关键词，则Web SDK会自动填充其所有关联的XDM元素。 如果要在允许其他元素的同时忽略特定的XDM元素，可以使用清除值 [`onBeforeEventSend`](onbeforeeventsend.md). 如果您在一个页面上发送多个事件，则Web SDK会在每一个 `SendEvent` 呼叫。

### Web

此 `"web"` keyword收集有关当前页面的信息。

| 维度 | 描述 | XDM 路径 | 示例值 |
| --- | --- | --- | --- |
| Page URL | 当前页面的URL。 | `xdm.web.webPageDetails.URL` | `https://example.com/index.html` |
| 反向链接URL | 访问的上一个页面的URL。 | `xdm.web.webReferrer.URL` | `http://example.org/linkedpage.html` |

{style="table-layout:auto"}

### 设备

此 `"device"` keyword收集有关用户设备的信息。

| 维度 | 描述 | XDM 路径 | 示例值 |
| --- | --- | --- | --- |
| 屏幕高度 | 屏幕的高度（像素）。 | `xdm.device.screenHeight` | `900` |
| 屏幕宽度 | 屏幕的宽度（像素）。 | `xdm.device.screenWidth` | `1440` |
| 屏幕方向 | 屏幕的方向。 | `xdm.device.screenOrientation` | `landscape` 或 `portrait` |

{style="table-layout:auto"}

### 环境

此 `"environment"` keyword收集有关用户浏览器的信息。

| 维度 | 描述 | XDM 路径 | 示例值 |
| --- | --- | --- | --- |
| 环境类型 | 体验通过哪种环境浮现。 Web SDK始终将此字段设置为 `browser`. | `xdm.environment.type` | `browser` |
| 视区高度 | 浏览器内容区域的高度（像素）。 | `xdm.environment.browserDetails.viewportHeight` | `679` |
| 视区宽度 | 浏览器内容区域的宽度（像素）。 | `xdm.environment.browserDetails.viewportWidth` | `642` |

{style="table-layout:auto"}

### 地标上下文

此 `"placeContext"` keyword收集有关用户位置的信息。

| 维度 | 描述 | XDM 路径 | 示例值 |
| --- | --- | --- | --- |
| 本地时间 | 用于最终用户的本地时间戳（以简化的扩展形式表示） [ISO 8601](https://datatracker.ietf.org/doc/html/rfc3339#section-5.6) 格式。 | `xdm.placeContext.localTime` | `YYYY-08-07T15:47:17.129-07:00` |
| 本地时区偏移 | 用户从GMT偏移的分钟数。 | `xdm.placeContext.localTimezoneOffset` | `360` |

{style="table-layout:auto"}

### 高熵客户端提示

此 `"highEntropyUserAgentHints"` 关键字收集有关用户设备的详细信息。 此数据包含在发送到Adobe的请求的HTTP标头中。 数据到达边缘网络后，XDM对象填充其各自的XDM路径。 如果您在中设置了相应的XDM路径， `sendEvent` 调用，其优先级高于HTTP标头值。

如果在以下情况下使用设备查找： [配置数据流](/help/datastreams/configure.md)，可以清除数据以支持设备查找值。 某些客户端提示字段和设备查找字段不能存在于同一点击中。

| 维度 | 描述 | HTTP 页头 | XDM 路径 | 示例值 |
| --- | --- | --- | --- | --- |
| 操作系统版本 | 操作系统的版本。 | `Sec-CH-UA-Platform-Version` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.platformVersion` | |
| 架构 | 底层CPU体系结构。 | `Sec-CH-UA-Arch` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.architecture` | |
| 设备型号 | 使用的设备的名称。 | `Sec-CH-UA-Model` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.model` | |
| 位数 | 基础CPU体系结构支持的位数。 | `Sec-CH-UA-Bitness` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.bitness` | |
| 浏览器供应商 | 创建浏览器的公司。 低熵提示 `Sec-CH-UA` 还会收集此元素。 | `Sec-CH-UA-Full-Version-List` | | |
| 浏览器名称 | 使用的浏览器。 低熵提示 `Sec-CH-UA` 还会收集此元素。 | `Sec-UA-Full-Version-List` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.brand` | |
| 浏览器版本 | 浏览器的重要版本。 低熵提示 `Sec-CH-UA` 还会收集此元素。 不会自动收集确切的浏览器版本。 | `Sec-UA-Full-Version-List` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.version` | |

{style="table-layout:auto"}

## 使用Web SDK标记扩展收集上下文信息

上下文信息设置是单选按钮和复选框的组合。 [配置标记扩展](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md). 每个复选框都映射到context关键字。

1. 登录 [experience.adobe.com](https://experience.adobe.com) 使用您的Adobe ID凭据。
1. 导航到 **[!UICONTROL 数据收集]** > **[!UICONTROL 标记]**.
1. 选择所需的标记属性。
1. 导航到 **[!UICONTROL 扩展]**，然后单击 **[!UICONTROL 配置]** 在 [!UICONTROL Adobe Experience Platform Web SDK] 卡片。
1. 向下滚动到 [!UICONTROL 数据收集] 部分，然后选择 **[!UICONTROL 所有默认上下文信息]** 或 **[!UICONTROL 特定上下文信息]**.
1. 如果您选择 **[!UICONTROL 特定上下文信息]**，启用每个所需的上下文信息元素旁边的复选框。
1. 单击 **[!UICONTROL 保存]**，然后发布更改。

## 使用Web SDK JavaScript库收集上下文信息

设置 `context` 字符串数组 `configure` 命令。 如果在配置SDK时省略此属性，则所有上下文信息( `"highEntropyUserAgentHints"` 默认收集。 如果要收集高熵客户端提示，或者要从数据收集中忽略其他上下文信息，请设置此属性。 字符串可以按任意顺序包含。

>[!NOTE]
>
>如果要收集所有上下文信息，包括高熵客户端提示，则必须将每个值都包含在 `context` 数组字符串。 默认 `context` 值忽略 `highEntropyUserAgentHints`，如果将 `context` 属性，则任何省略的值都不会收集数据。

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "context": ["web", "device", "environment", "placeContext", "highEntropyUserAgentHints"]
});
```
