---
title: Adobe Experience Platform Web SDK扩展发行说明
description: Adobe Experience Platform Web SDK标记扩展
exl-id: 91de8c91-023a-45b6-9f67-ac75ee471e50
source-git-commit: bb06dd63de1a36d3e3d065a986f3d34f63783895
workflow-type: tm+mt
source-wordcount: '1290'
ht-degree: 48%

---

# Adobe Experience Platform Web SDK扩展发行说明

本文档介绍Adobe Experience Platform Web SDK标记扩展的发行说明。 有关SDK本身的最新发行说明，请参阅 [平台Web SDK发行说明](https://experienceleague.adobe.com/docs/experience-platform/edge/release-notes.html).

## 版本2.10.0 - 2022年3月10日

* 更新可在配置页面上复制的预隐藏代码片段，以便与更新的Adobe Target VEC编辑器一起使用。

包含 Adobe Experience Platform Web SDK 库的版本 2.9.0。

## 2.9.0版 — 2022年1月19日

包含 Adobe Experience Platform Web SDK 库的版本 2.8.0。

## 2.8.0版 — 2021年10月26日

包含 Adobe Experience Platform Web SDK 库的版本 2.7.0。

* Experience Edge中的其他信息可在发送事件结束事件中获取，包括 `inferences` 和 `destinations`. 由于这些功能当前作为测试版的一部分推出，因此这些属性的格式可能会发生更改。 有关更多信息，请参阅 [跟踪事件。](../fundamentals/tracking-events.md)

## 2.7.3版 — 2021年9月7日

包含 Adobe Experience Platform Web SDK 库的版本 2.6.4。

* 不再有弃用警告 `container.buildInfo.environment.`

## 2.7.0版 — 2021年8月16日

包含 Adobe Experience Platform Web SDK 库的版本 2.6.3。

* 现在，使用身份映射数据元素类型时，其ID解析为未填充字符串值的标识符将自动从身份映射中删除。
* 修复了尝试使用XDM对象数据元素类型保存数据元素时，未选择架构时可能发生的错误。
* 改进了用户界面排版规则。

## 2.6.2版 — 2021年8月4日

包含 Adobe Experience Platform Web SDK 库的版本 2.6.2。

## 2.6.1版 — 2021年7月29日

包含 Adobe Experience Platform Web SDK 库的版本 2.6.1。

## 2.6.0版 — 2021年7月27日

包含 Adobe Experience Platform Web SDK 库的版本 2.6.0。

* 使用术语“边缘配置”的标签、描述和错误消息已更改为使用术语“datastream”来与最新的Adobe Experience Platform术语保持一致。
* 在扩展配置视图中，添加了对处理大量数据流和数据流环境的支持。
* 在XDM对象数据元素视图中，添加了对处理大量架构的支持。
* 添加了“发送事件结束”事件类型，该事件类型可用于在将事件发送到服务器并收到响应后运行规则。 更多文档即将发布。
* 已弃用“收到的决定”事件类型。 请改用发送事件结束事件类型。
* 用户界面和错误处理通常已得到改进。

## 2.5.0版 — 2021年6月1日

包含 Adobe Experience Platform Web SDK 库的版本 2.5.0。

* 添加了 `data` 字段。 即将发布的文档将介绍如何在某些情况下使用此功能。
* 在XDM对象数据元素视图中，修复了以下问题：如果用户有权访问Adobe Experience Platform沙箱，但没有访问配置为组织默认内容的沙箱，则会引发错误。
* 在XDM对象数据元素视图中，修复了一个问题，即即使父对象不包含任何值，必填字段也会被视为无效。

## 2.4.0版 — 2021年3月9日

包含 Adobe Experience Platform Web SDK 库的版本 2.4.0。

* 添加了 [&quot;文档卸载&quot;](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/tracking-events.html?lang=en#using-the-sendbeacon-api) 复选框以发送事件操作UI。
* 添加了对 `out` 选项时 [配置默认同意](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#default-consent) 会丢弃所有事件，直到收到同意(现有 `pending` 选项会将事件排入队列，并在收到同意后发送它们)。
* 在默认同意字段中添加了工具提示。
* 添加了 [Adobe的同意2.0标准](https://experienceleague.adobe.com/docs/experience-platform/edge/consent/supporting-consent.html?communicating-consent-preferences-via-the-adobe-standard).
* 现在，如果用户的访问令牌无效或配置不正确，则XDM对象数据元素UI中会显示更好的错误。
* 修复了在查看XDM对象数据元素时显示在浏览器开发人员控制台中的跨域错误（这不会影响扩展的操作）。

## 2.3.0版 — 2020年11月4日

包含 Adobe Experience Platform Web SDK 库的版本 2.3.0。

* 添加了对配置默认同意的过程中使用数据元素的支持。
* 添加了通过 XDM 对象数据元素类型搜索 XDM 模式的功能。
* 将 XDM 数据克隆添加到“发送事件”操作类型中，以确保任何对 XDM 数据对象的后续更改将不会反映在请求中。

## 2.2.0版 — 2020年10月1日

* 当客户尝试按照沙盒模式创建 XDM 对象时，他们将会遇到身份验证问题。现在，调用平台的API可以感知到各种环境，因此用户只能看到他们有权编辑的架构。
* 使用 `identityMap` 数据元素中，命名空间现在会预填充到下拉列表中，因此您无需手动进行填充。
* 翻新了 `xdmObject` 数据元素的 UI。在新的 UI 中，您无需输入对象中的每个项目，即可查看已填充字段。

## 2.1.1版 — 2020年8月26日

* 修复了 XDM 对象视图上的 Adobe Experience Platform 沙箱显示不正确的问题。在使用该扩展版本时，如果列表中未显示预期的沙箱，则用户应与其 Adobe Experience Platform 管理员确认，以确保设置正确的访问权限。

## 2.1.0版 — 2020年8月5日

* 重大变更：移除了 `syncIdentity` 操作，取而代之，在 `sendEvent` 操作中支持传递这些 ID。请在升级扩展之前，通过这项操作来禁用任何现有规则。
* 更新至 Alloy v. 2.1.0（[发行说明](https://experienceleague.adobe.com/docs/experience-platform/edge/release-notes.html)）
* 在 `setConsent` 操作中支持 IAB 2.0 Consent Standard。
* 在 `sendEvent` 操作中支持覆盖数据集 ID。
* 增加了 `IdentityMap` 类型的新数据元素，该数据元素可用于在（现已启用的）XDM 对象数据元素和 `setConsent` 操作中填充 `identityMap` 条目。
* 在 `setConsent` 操作中支持传递标识映射。
* 支持在XDM对象数据元素中选择平台沙盒。

## 1.0.0版 — 2020年5月26日

* 支持从配置服务中选择环境。

## 0.1.2版 — 2020年5月4日

* 将 `configId` 重命名为 `edgeConfigId`。
* 将 `viewStart` 重命名为 `renderDecisions`，默认情况下设置为 false。如果设置为 true，则会获取并自动渲染个性化内容。
* 与 `Get Decisions` 相关的更改：
   * 删除了 `getDecisions` 命令。
   * 为 `sendEvent` 命令添加了一个 `scopes` 选项。将在 `sendEvent` 已解决的承诺中返回决策。
   * 添加了内置 `__view__` 范围，该范围将导致返回页面/视图范围的内容。（例如，Target 中的 VEC 内容。）仅当将 `renderDecisions` 设置为 false 时，才会从 `sendEvent` 命令返回这些决策。
   * 添加了一个 `Decisions Received` 事件，当决策可用时会触发此事件。
* 在单个服务器调用下合并多个个性化通知。
* 修复了每次引用数据元素时都会重置事件合并 ID 的问题。
* 将 `setCustomerIds` 操作重命名为 `syncIdentity`。
* 添加了一个 `getIdentity` 命令。现在只能通过自定义代码使用此命令。
* 使用启用调试 `_satellite` 现在可在Adobe Experience Platform Web SDK中进行调试。
* 添加了对 XDM 对象中键入值的支持：布尔值、数字和小数。

## 0.0.10版 — 2020年3月16日

* 将“选择启用”和“选择禁用”的概念组合在 `Consent` 下，并添加了新的 `setConsent` 命令。
* 添加了类型为 `XDM Object` 的新数据元素，这种类型的数据元素允许从 JavaScript/JSON 映射到 XDM。

## 0.0.7版 — 2020年2月18日

* 删除了 idSyncContainerId、datasetId、schemaId、urlDestinationsEnabled 和 cookieDestinationsEnabled 选项
* 添加了对 edgeDomain 选项值中连字符的支持
* 在 ID 迁移期间发出的请求将发送到 demdex 端点，以改进未设置 demdex Cookie 时的跨域识别
* 在 ID 迁移过程中发出的请求始终需要响应，以确保设置身份标识 Cookie
* 执行无效命令时，控制台中将记录有效命令名称列表
* 向标记扩展中添加了用于切换第三方Cookie支持的复选框。 这将禁用对 demdex.net 的调用

## 0.0.5版 — 2019年12月20日

* 将活动跟踪器配置添加到标记扩展
* 在事件命令中公开 EventType 和 EventMergeId
* 将onBeforeEventSend配置添加到标记扩展
* 将edgeBasePath配置添加到标记扩展

## 0.0.3版 — 2019年11月25日

* 在“Send Event”（发送事件）操作中，新增了“Merge ID”（合并 ID）和“Type”（类型）字段。“Merge ID”（合并 ID）映射到 XDM 架构中的 `xdm.eventMergeID`；“Type”（类型）则映射到 XDM 架构中的 `xdm.eventType`。

## 0.0.2版 — 2019年11月18日

* 初始版本
