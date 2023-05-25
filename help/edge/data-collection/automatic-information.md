---
title: Adobe Experience Platform Web SDK中自动收集的信息
description: Adobe Experience Platform SDK自动收集的每个信息段的概述。
keywords: 收集信息；上下文；配置；设备；screenHeight；屏幕高度；屏幕方向；屏幕方向；屏幕宽度；环境；视区高度；视区高度；视区宽度；视区详细信息；浏览器详细信息；实施详细信息；实施详细信息；名称；版本；placeContext；本地时间；本地时区Offset；本地时区偏移；时间戳；Web；URL；WebPageDetails；网页详细信息；WebReferrer；横向；纵向；
exl-id: 901df786-df36-4986-9c74-a32d29c11b71
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '511'
ht-degree: 6%

---

# 自动收集的信息

Adobe Experience Platform Web SDK无需任何特殊配置即可自动收集大量信息。 但是，如果需要，可以使用禁用此信息 `context` 中的选项 `configure` 命令。 [请参阅配置SDK](../fundamentals/configuring-the-sdk.md). 以下是这些信息的列表。 括号中的名称表示配置上下文时要使用的字符串。

## 设备 (`device`)

有关设备的信息。 这不包括可以从用户代理字符串在服务器端查找的数据。

### 屏幕高度

| **有效负载中的路径：** | **示例：** |
| ---------------------------------- | ------------ |
| `events[].xdm.device.screenHeight` | `900` |

屏幕的高度（像素）。

### 屏幕方向

| **有效负载中的路径：** | **可能值:** |
| --------------------------------------- | ------------------------- |
| `events[].xdm.device.screenOrientation` | `landscape` 或 `portrait` |

屏幕的方向。

### 屏幕宽度

| **有效负载中的路径：** | **示例：** |
| --------------------------------- | ------------ |
| `events[].xdm.device.screenWidth` | `1440` |

屏幕的宽度（像素）。

## 环境 (`environment`)

有关浏览器环境的详细信息。

### 环境类型

浏览器

| **有效负载中的路径：** | **示例：** |
| ------------------------------- | ------------ |
| `events[].xdm.environment.type` | `browser` |

体验浮现的环境类型。 Adobe Experience Platform Web SDK始终将此参数设置为 `browser`.

### 视区高度

| **有效负载中的路径：** | **示例：** |
| -------------------------------------------------------- | ------------ |
| `events[].xdm.environment.browserDetails.viewportHeight` | `679` |

浏览器内容区域的高度（像素）。

### 视区宽度

| **有效负载中的路径：** | **示例：** |
| ------------------------------------------------------- | ------------ |
| `events[].xdm.environment.browserDetails.viewportWidth` | `642` |

浏览器内容区域的宽度（像素）。

## 实施详细信息

有关用于收集事件的SDK的信息。

### 名称

| **有效负载中的路径：** | **示例：** |
| ----------------------------------------- | --------------------------------------- |
| `events[].xdm.implementationDetails.name` | `https://ns.adobe.com/experience/alloy` |

软件开发工具包(SDK)标识符。  此字段使用URI来改进由不同软件库提供的标识符之间的唯一性。 使用独立库时，值为 `https://ns.adobe.com/experience/alloy`. 当库用作标记扩展的一部分时，值为 `https://ns.adobe.com/experience/alloy+reactor`.

### 版本

| **有效负载中的路径：** | **示例：** |
| -------------------------------------------- | ------------ |
| `events[].xdm.implementationDetails.version` | `0.11.0` |

使用独立库时，值只是库版本。 当库用作标记扩展的一部分时，这是使用“+”连接的库版本和标记扩展版本。 例如，如果库版本为2.1.0，而标记扩展版本为2.1.3，则值将为 `2.1.0+2.1.3`.

### 环境

| **有效负载中的路径：** | **示例：** |
| ------------------------------------------------ | ------------ |
| `events[].xdm.implementationDetails.environment` | `browser` |

收集数据的环境。 此参数始终设置为 `browser`.

## 地标上下文(`placeContext`)

有关最终用户位置的信息。

### 本地时间

| **有效负载中的路径：** | **示例：** |
| ------------------------------------- | ------------------------------- |
| `events[].xdm.placeContext.localTime` | `2019-08-07T15:47:17.129-07:00` |

简化扩展ISO格式的最终用户的本地时间戳 [ISO 8601](https://tools.ietf.org/html/rfc3339#section-5.6).

### 本地时区偏移

| **有效负载中的路径：** | **示例：** |
| ----------------------------------------------- | ------------ |
| `events[].xdm.placeContext.localTimezoneOffset` | `360` |

用户与GMT偏移的分钟数。

## 时间戳

| **有效负载中的路径：** | **示例：** |
| ------------------------ | -------------------------- |
| `events[].xdm.timestamp` | `2019-08-07T22:47:17.129Z` |

事件的时间戳。  无法删除上下文的这一部分。

简化扩展ISO格式的最终用户的UTC时间戳 [ISO 8601](https://tools.ietf.org/html/rfc3339#section-5.6).

## Web详细信息(`web`)

有关用户所在页面的详细信息。

### 当前页面URL

| **有效负载中的路径：** | **示例：** |
| ------------------------------------- | ------------------------------------ |
| `events[].xdm.web.webPageDetails.URL` | `https://somesite.com/somepage.html` |

当前页面的URL。

### 反向链接URL

| **有效负载中的路径：** | **示例：** |
| ---------------------------------- | ----------------------------------------- |
| `events[].xdm.web.webReferrer.URL` | `http://somereferrer.com/linkedpage.html` |

访问的上一页的URL。
