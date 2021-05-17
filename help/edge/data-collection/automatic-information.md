---
title: 在Adobe Experience Platform Web SDK中自动收集信息
description: Adobe Experience Platform SDK自动收集的每条信息的概述。
keywords: 收集信息；上下文；配置；设备；屏幕高度；屏幕方向；屏幕方向；屏幕方向；屏幕宽度；环境；视口高度；视口高度；viewport Height;viewportWidth;viewport Width;crowserDetails；浏览器详细信息；实现详细信息；实现详细信息；名称；版本；placeContext;localTime；本地时间timezoneOffset；本地时区偏移；timestamp;web;url;webPageDetails;web页详细信息；webReferrer;web推荐人；横向；纵向；
exl-id: 901df786-df36-4986-9c74-a32d29c11b71
source-git-commit: 0f671a967a67761e0cfef6fa0d022e3c3790c2d8
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 6%

---

# 自动收集的信息

Adobe Experience Platform Web SDK可自动收集大量信息，无需任何特殊配置。 但是，如果需要，可以使用`configure`命令中的`context`选项禁用此信息。 [请参阅配置SDK](../fundamentals/configuring-the-sdk.md)。以下是这些信息的列表。 括号中的名称表示配置上下文时要使用的字符串。

## 设备 (`device`)

有关设备的信息。 这不包括可从用户代理字符串中查找的服务器端数据。

### 屏幕高度

| **有效负荷中的路径：** | **示例：** |
| ---------------------------------- | ------------ |
| `events[].xdm.device.screenHeight` | `900` |

屏幕的高度（以像素为单位）。

### 屏幕方向

| **有效负荷中的路径：** | **可能值:** |
| --------------------------------------- | ------------------------- |
| `events[].xdm.device.screenOrientation` | `landscape` 或 `portrait` |

屏幕的方向。

### 屏幕宽度

| **有效负荷中的路径：** | **示例：** |
| --------------------------------- | ------------ |
| `events[].xdm.device.screenWidth` | `1440` |

屏幕的宽度（以像素为单位）。

## 环境 (`environment`)

有关浏览器环境的详细信息。

### 环境类型

浏览器

| **有效负荷中的路径：** | **示例：** |
| ------------------------------- | ------------ |
| `events[].xdm.environment.type` | `browser` |

体验通过的环境类型。 Adobe Experience Platform Web SDK始终将此值设置为`browser`。

### 视口高度

| **有效负荷中的路径：** | **示例：** |
| -------------------------------------------------------- | ------------ |
| `events[].xdm.environment.browserDetails.viewportHeight` | `679` |

浏览器内容区域的高度（以像素为单位）。

### 视口宽度

| **有效负荷中的路径：** | **示例：** |
| ------------------------------------------------------- | ------------ |
| `events[].xdm.environment.browserDetails.viewportWidth` | `642` |

浏览器内容区域的宽度（以像素为单位）。

## 实施详细信息

有关用于收集事件的SDK的信息。

### 名称

| **有效负荷中的路径：** | **示例：** |
| ----------------------------------------- | --------------------------------------- |
| `events[].xdm.implementationDetails.name` | `https://ns.adobe.com/experience/alloy` |

软件开发工具包(SDK)标识符。  此字段使用URI来改进由不同软件库提供的标识符之间的唯一性。 使用独立库时，值为`https://ns.adobe.com/experience/alloy`。 将库用作Platform launch扩展的一部分时，该值为`https://ns.adobe.com/experience/alloy+reactor`。

### 版本

| **有效负荷中的路径：** | **示例：** |
| -------------------------------------------- | ------------ |
| `events[].xdm.implementationDetails.version` | `0.11.0` |

当使用独立库时，其值只是库版本。 将库用作Platform launch扩展的一部分时，这是与“+”联接的库版本和Platform launch扩展版本。 例如，如果库版本为2.1.0，而Platform launch扩展版本为2.1.3，则值为`2.1.0+2.1.3`。

### 环境

| **有效负荷中的路径：** | **示例：** |
| ------------------------------------------------ | ------------ |
| `events[].xdm.implementationDetails.environment` | `browser` |

收集数据的环境。 此值始终设置为`browser`。

## 放置上下文(`placeContext`)

有关最终用户位置的信息。

### 本地时间

| **有效负荷中的路径：** | **示例：** |
| ------------------------------------- | ------------------------------- |
| `events[].xdm.placeContext.localTime` | `2019-08-07T15:47:17.129-07:00` |

以简化的扩展ISO格式[ISO 8601](https://tools.ietf.org/html/rfc3339#section-5.6)为最终用户的本地时间戳。

### 本地时区偏移

| **有效负荷中的路径：** | **示例：** |
| ----------------------------------------------- | ------------ |
| `events[].xdm.placeContext.localTimezoneOffset` | `360` |

用户从GMT偏移的分钟数。

## 时间戳

| **有效负荷中的路径：** | **示例：** |
| ------------------------ | -------------------------- |
| `events[].xdm.timestamp` | `2019-08-07T22:47:17.129Z` |

事件的时间戳。  无法删除上下文的这一部分。

最终用户的UTC时间戳，采用简化的扩展ISO格式[ISO 8601](https://tools.ietf.org/html/rfc3339#section-5.6)。

## Web详细信息(`web`)

有关用户所在页面的详细信息。

### 当前页面URL

| **有效负荷中的路径：** | **示例：** |
| ------------------------------------- | ------------------------------------ |
| `events[].xdm.web.webPageDetails.URL` | `https://somesite.com/somepage.html` |

当前页面的URL。

### 推荐人URL

| **有效负荷中的路径：** | **示例：** |
| ---------------------------------- | ----------------------------------------- |
| `events[].xdm.web.webReferrer.URL` | `http://somereferrer.com/linkedpage.html` |

上一页访问的URL。
