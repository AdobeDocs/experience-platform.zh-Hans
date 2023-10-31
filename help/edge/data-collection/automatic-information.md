---
title: 自动收集的信息
description: Adobe Experience Platform Web SDK自动收集的数据概述。
exl-id: 901df786-df36-4986-9c74-a32d29c11b71
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '331'
ht-degree: 2%

---

# 自动收集的信息

Adobe Experience Platform Web SDK会自动收集一些现成的信息。 如果贵组织不希望自动收集此数据，则可以使用 `context` 中的选项 [`configure` 命令](../fundamentals/configuring-the-sdk.md).

关键字已从 `context` 数据收集中不包括数组。 如果 `context` 数组中不存在 `configure` 命令，则会自动收集下表中所有数据。

| 名称 | 描述 | `context` 数组关键词 | XDM 路径 | 示例值 |
| --- | --- | --- | --- | --- |
| 屏幕高度 | 屏幕的高度（像素）。 | `device` | `events[].xdm.device.screenHeight` | `900` |
| 屏幕宽度 | 屏幕的宽度（像素）。 | `device` | `events[].xdm.device.screenWidth` | `1440` |
| 屏幕方向 | 屏幕的方向。 | `device` | `events[].xdm.device.screenOrientation` | `landscape` 或 `portrait` |
| 环境类型 | 体验通过哪种环境浮现。 Adobe Experience Platform Web SDK始终将此字段设置为 `browser`. | `environment` | `events[].xdm.environment.type` | `browser` |
| 视区高度 | 浏览器内容区域的高度（像素）。 | `environment` | `events[].xdm.environment.browserDetails.viewportHeight` | `679` |
| 视区宽度 | 浏览器内容区域的宽度（像素）。 | `environment` | `events[].xdm.environment.browserDetails.viewportWidth` | `642` |
| SDK名称 | sdk标识符。 此字段使用URI来改进由不同软件库提供的标识符之间的唯一性。 使用独立库时，值为 `https://ns.adobe.com/experience/alloy`. 当库用作标记扩展的一部分时，值为 `https://ns.adobe.com/experience/alloy+reactor`. | | `events[].xdm.implementationDetails.name` | `https://ns.adobe.com/experience/alloy` |
| SDK版本 | 使用独立库时，该值为库版本。 当库用作标记扩展的一部分时，值是库版本与标记扩展版本的连接。 | | `events[].xdm.implementationDetails.version` | `2.1.0+2.1.3` |
| 环境 | 收集数据的环境。 Adobe Experience Platform Web SDK始终将此字段设置为 `browser`. | | `events[].xdm.implementationDetails.environment` | `browser` |
| 本地时间 | 简化扩展ISO格式的最终用户的本地时间戳 [ISO 8601](https://datatracker.ietf.org/doc/html/rfc3339#section-5.6). | `placeContext` | `events[].xdm.placeContext.localTime` | `YYYY-08-07T15:47:17.129-07:00` |
| 本地时区偏移 | 用户从GMT偏移的分钟数。 | `placeContext` | `events[].xdm.placeContext.localTimezoneOffset` | `360` |
| 时间戳 | 简化扩展ISO格式的最终用户的UTC时间戳 [ISO 8601](https://datatracker.ietf.org/doc/html/rfc3339#section-5.6). | 始终包含 | `events[].xdm.timestamp` | `YYYY-08-07T22:47:17.129Z` |
| 当前页面URL | 当前页面的URL。 | `web` | `events[].xdm.web.webPageDetails.URL` | `https://example.com/index.html` |
| 反向链接URL | 访问的上一个页面的URL。 | `web` | `events[].xdm.web.webReferrer.URL` | `http://example.org/linkedpage.html` |

{style="table-layout:auto"}
