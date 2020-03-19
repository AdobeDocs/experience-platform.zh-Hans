---
title: 自动收集的信息
seo-title: 由Adobe Experience Platform Web SDK自动收集的信息
description: Adobe Experience Cloud SDK自动收集的每条信息的说明
seo-description: Adobe Experience Cloud SDK自动收集的每条信息的说明
translation-type: tm+mt
source-git-commit: 0cc6e233646134be073d20e2acd1702d345ff35f

---


# （测试版）自动收集的信息

>[!IMPORTANT]
>
>Adobe Experience Platform Web SDK目前为测试版，并非所有用户都可用。 文档和功能可能会发生更改。

Adobe Experience Cloud SDK可自动收集大量信息，无需任何特殊配置。 但是，如果需要，可以使用命令中的选项禁 `context` 用此信 `configure` 息。 [请参阅配置SDK](../fundamentals/configuring-the-sdk.md)。 以下是这些信息的列表。 括号中的名称指示配置上下文时要使用的字符串。

## 设备 (`device`)

有关设备的信息。 这不包括可从用户代理字符串在服务器端查找的数据。

### 屏幕高度

| **有效负荷中的路径：** | **示例：** |
| ---------------------------------- | ------------ |
| `events[].xdm.device.screenHeight` | `900` |

屏幕的高度（以像素为单位）。

### 屏幕方向

| **有效负荷中的路径：** | **可能值：** |
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

Browser

| **有效负荷中的路径：** | **示例：** |
| ------------------------------- | ------------ |
| `events[].xdm.environment.type` | `browser` |

体验所通过的环境类型。 Adobe Experience Platform SDK for JavaScript始终可设置 `browser`。

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

有关用于收集活动的SDK的信息。

### 名称

| **有效负荷中的路径：** | **示例：** |
| ----------------------------------------- | --------------------------------------- |
| `events[].xdm.implementationDetails.name` | `https://ns.adobe.com/experience/alloy` |

软件开发工具包(SDK)标识符。  此字段使用URI来改进由不同软件库提供的标识符之间的唯一性。

### 版本

| **有效负荷中的路径：** | **示例：** |
| -------------------------------------------- | ------------ |
| `events[].xdm.implementationDetails.version` | `0.11.0` |

## 放置上下文(`placeContext`)

有关最终用户位置的信息。

### 本地时间

| **有效负荷中的路径：** | **示例：** |
| ------------------------------------- | ------------------------------- |
| `events[].xdm.placeContext.localTime` | `2019-08-07T15:47:17.129-07:00` |

最终用户的本地时间戳，采用简化的扩展ISO格式 [ISO 8601](https://tools.ietf.org/html/rfc3339#section-5.6)。

### 局部时区偏移

| **有效负荷中的路径：** | **示例：** |
| ----------------------------------------------- | ------------ |
| `events[].xdm.placeContext.localTimezoneOffset` | `360` |

用户从GMT偏移的分钟数。

## 时间戳

| **有效负荷中的路径：** | **示例：** |
| ------------------------ | -------------------------- |
| `events[].xdm.timestamp` | `2019-08-07T22:47:17.129Z` |

事件的时间戳。无法删除上下文的这一部分。

最终用户的UTC时间戳，采用简化的扩展ISO格 [式ISO 8601](https://tools.ietf.org/html/rfc3339#section-5.6)。

## Web详细信息(`web`)

有关用户所在页面的详细信息。

### 当前页面URL

| **有效负荷中的路径：** | **示例：** |
| ------------------------------------- | ------------------------------------ |
| `events[].xdm.web.webPageDetails.URL` | `https://somesite.com/somepage.html` |

当前页面的URL。

### 引用URL

| **有效负荷中的路径：** | **示例：** |
| ---------------------------------- | ----------------------------------------- |
| `events[].xdm.web.webReferrer.URL` | `http://somereferrer.com/linkedpage.html` |

访问的上一页的URL。
