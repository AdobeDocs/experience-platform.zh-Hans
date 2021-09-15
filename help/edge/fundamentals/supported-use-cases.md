---
title: Adobe Experience Platform Web SDK支持的用例
description: 了解Adobe Experience Platform Web SDK支持哪些用例。
keywords: Web SDK；用例
exl-id: e0643c2c-ceb3-4ea2-aafa-1e18e0c66453
source-git-commit: ed092b85d74eaa0fdc29f3a8d28f84fe81ccca17
workflow-type: tm+mt
source-wordcount: '445'
ht-degree: 18%

---

# 支持的用例

本页列出了Web SDK支持的用例，以及指向其他信息的链接。

## General

| 用例 | 更多信息 |
| --- | --- |
| 单一简化的SDK |  |
| 全局数据收集网络 |  |
| 课程粒度同意 |  |
| 根据各种标准收集客户同意 | <ul><li>[Adobe同意2.0支持](../../landing/governance-privacy-security/consent/adobe/overview.md)</li><li>[支持IAB TCF 2.0](../../landing/governance-privacy-security/consent/iab/overview.md)</li><li>[集成SDK以向边缘网络发送同意信号](../../landing/governance-privacy-security/consent/sdk.md)</li></ul> |
| ECID支持 | 有关检索ECID的信息，请参阅我们的文档[此处](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html?lang=en#first-party-identity)和[此处](https://experienceleague.adobe.com/docs/experience-platform/edge/extension/accessing-the-ecid.html?lang=en#extension) |
| 收集多个实体 |  |
| 设备图支持（公共/专用） | [文档](https://experienceleague.adobe.com/docs/analytics/components/cda/device-graph.html?lang=en) |
| 将数据发送到页面上的多个组织 | [文档](./interacting-with-multiple-properties.md) |
| 详细的错误报告和日志 |  |
| 跟踪请求客户端和服务器端 |  |
| 标记扩展 | [Web SDK扩展文档](../../tags/extensions/web/sdk/overview.md) |
| 提供调试工具 | [Debugger扩](https://experienceleague.adobe.com/docs/debugger-learn/tutorials/experience-platform-debugger/introduction-to-the-experience-platform-debugger.html?lang=en) 展和 [Griffon](https://aep-sdks.gitbook.io/docs/beta/project-griffon) |

{style=&quot;table-layout:auto&quot;}

## Adobe Experience Platform

| 用例 | 更多信息 |
| --- | --- |
| 发送体验事件 |  |
| Offer Decisioning | [文档](../personalization/offer-decisioning/offer-decisioning-overview.md) |
| 如果为用户档案启用了数据集，则能够实时将数据发送到实时客户数据用户档案 |  |
| 实时将数据发送到Customer Journey Analytics |  |
| 将同意写入用户档案 | [文档](../../landing/governance-privacy-security/consent/sdk.md) |
| 实时将数据服务器端转发给第三方 | [文档](../../tags/ui/event-forwarding/overview.md) |
| 身份命名空间支持 |  |

{style=&quot;table-layout:auto&quot;}

## Adobe Analytics

| 用例 | 更多信息 |
| --- | --- |
| Analytics for Target (A4T) |  |
| 没有Analytics for Target(A4T)延迟 |  |
| 多包标记 |  |
| 机器人过滤 |  |
| Prop、eVar和事件 |  |
| 对Adobe Analytics的ListVar支持 |  |
| 操作系统和浏览器版本 |  |
| 现成变量 | [自动映射的变量](../data-collection/adobe-analytics/automatically-mapped-vars.md) |
| VISTA规则/处理规则 |  |
| 访客属性支持 |  |
| 退出链接支持 |  |
| 自定义链接/下载链接 |  |
| 状态和操作跟踪 |  |
| 标准事件的事件序列化 |  |
| Products 变量 | [文档](../data-collection/collect-commerce-data.md#actions-related-to-products) |

{style=&quot;table-layout:auto&quot;}

## Adobe Target

| 用例 | 更多信息 |
| --- | --- |
| 所有活动类型 |  |
| 本机和SPA可视化体验编辑器支持 | [文档](../personalization/adobe-target/spa-implementation.md) |
| 基于表单的编辑器 |  |
| 支持全局mbox | [文档](../personalization/rendering-personalization-content.md#automatically-rendering-content) |
| 自定义 mbox | [文档](../personalization/rendering-personalization-content.md#manually-rendering-content) |
| Analytics for Target(A4T) |  |
| 环境支持 |  |
| 工作区支持 |  |
| Adobe Target中的QA链接 |  |
| 在Adobe Target中根据地理/设备进行定位 |  |
| 访客属性支持 |  |
| 个人资料脚本 |  |
| XDM成为mbox参数 |  |
| A4T报表支持的重定向选件 | [文档](https://experienceleague.adobe.com/docs/target/using/experiences/offers/offer-redirect.html?lang=en) |
| 更新Target配置文件 | [文档](../personalization/adobe-target/target-overview.md#single-profile-update) |
| 推荐 |  |
| mBox第三方ID |  |
| 响应令牌 | [文档](../personalization/adobe-target/accessing-response-tokens.md) |

{style=&quot;table-layout:auto&quot;}

## Adobe Audience Manager

| 用例 | 更多信息 |
| --- | --- |
| Audience Analytics |  |
| 区段共享到Adobe Analytics |  |
| 访客属性支持 |  |
| 合作伙伴同步 |  |
| URL目标 |  |
| Cookie目标 |  |
| 环境支持 |  |
| 同步Adobe Experience Platform命名空间以Audience Manager数据源 |  |
| 已验证或已知的ID |  |

{style=&quot;table-layout:auto&quot;}
