---
title: Adobe Experience Platform Web SDK扩展发行说明
description: Adobe Experience Platform Launch 中的 Adobe Experience Platform Web SDK 扩展
seo-description: Adobe Experience Platform Launch 中的 Adobe Experience Platform Web SDK 扩展
exl-id: 91de8c91-023a-45b6-9f67-ac75ee471e50
source-git-commit: c3d66e50f647c2203fcdd5ad36ad86ed223733e3
workflow-type: tm+mt
source-wordcount: '1130'
ht-degree: 78%

---

# Adobe Experience Platform Web SDK扩展发行说明

本文档介绍了适用于Adobe Experience Platform Launch的Adobe Experience Platform Web SDK扩展的发行说明。 有关SDK本身的最新发行说明，请参阅[平台Web SDK发行说明](https://experienceleague.adobe.com/docs/experience-platform/edge/release-notes.html)。

## 2020 年 3 月 9 日

### Adobe Experience Platform Web SDK 2.4.0

包含 Adobe Experience Platform Web SDK 库的版本 2.4.0。

* 已将[&quot;document unloading&quot;](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/tracking-events.html?lang=en#using-the-sendbeacon-api)复选框添加到“发送事件操作UI”。
* 添加了对`out`选项的支持，当[配置默认同意](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#default-consent)时，该选项会丢弃所有事件直到收到同意（现有的`pending`选项会将事件排入队列，并在收到同意后发送它们）。
* 在默认同意字段中添加了工具提示。
* 添加了对[Adobe的“同意2.0”标准](https://experienceleague.adobe.com/docs/experience-platform/edge/consent/supporting-consent.html?communicating-consent-preferences-via-the-adobe-standard)的支持。
* 现在，如果用户的访问令牌无效或配置不正确，则XDM对象数据元素UI中会显示更好的错误。
* 修复了在查看XDM对象数据元素时显示在浏览器开发人员控制台中的跨域错误（这不会影响扩展的操作）。

## 2020 年 11 月 4 日

### Adobe Experience Platform Web SDK 2.3.0

包含 Adobe Experience Platform Web SDK 库的版本 2.3.0。

#### 功能

* 添加了对配置默认同意的过程中使用数据元素的支持。
* 添加了通过 XDM 对象数据元素类型搜索 XDM 模式的功能。
* 将 XDM 数据克隆添加到“发送事件”操作类型中，以确保任何对 XDM 数据对象的后续更改将不会反映在请求中。

## 2020 年 10 月 1 日

### Adobe Experience Platform Web SDK 2.2.0

#### 错误修复

* 当客户尝试按照沙盒模式创建 XDM 对象时，他们将会遇到身份验证问题。现在，调用平台的API可以感知到各种环境，因此用户只能看到他们有权编辑的架构。

#### 功能

* 使用 `identityMap` 数据元素时，命名空间会即时预填充到下拉框中，因此您不必手动进行填充。
* 翻新了 `xdmObject` 数据元素的 UI。在新的 UI 中，您无需输入对象中的每个项目，即可查看已填充字段。


## 2020 年 8 月 26 日

### Adobe Experience Platform Web SDK 2.1.1

#### 功能

* 修复了 XDM 对象视图上的 Adobe Experience Platform 沙箱显示不正确的问题。在使用该扩展版本时，如果列表中未显示预期的沙箱，则用户应与其 Adobe Experience Platform 管理员确认，以确保设置正确的访问权限。


## 2020 年 8 月 5 日

### Adobe Experience Platform Web SDK 2.1.0

#### 功能

* 重大变更：移除了 `syncIdentity` 操作，取而代之，在 `sendEvent` 操作中支持传递这些 ID。请在升级扩展之前，通过这项操作来禁用任何现有规则。
* 更新至 Alloy v. 2.1.0（[发行说明](https://experienceleague.adobe.com/docs/experience-platform/edge/release-notes.html)）
* 在 `setConsent` 操作中支持 IAB 2.0 Consent Standard。
* 在 `sendEvent` 操作中支持覆盖数据集 ID。
* 增加了 `IdentityMap` 类型的新数据元素，该数据元素可用于在（现已启用的）XDM 对象数据元素和 `setConsent` 操作中填充 `identityMap` 条目。
* 在 `setConsent` 操作中支持传递标识映射。
* 支持在XDM对象数据元素中选择平台沙盒。


## 2020 年 5 月 26 日

### Adobe Experience Platform Web SDK 1.0.0

#### 功能

* 支持从配置服务中选择环境。


## 2020 年 5 月 4 日

### Adobe Experience Platform Web SDK 0.1.2

#### 功能

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
* 现在，允许使用`_satellite`进行调试可在Adobe Experience Platform Web SDK中进行调试。
* 添加了对 XDM 对象中键入值的支持：布尔值、数字和小数。

## 2020 年 3 月 16 日

### Adobe Experience Platform Web SDK 0.0.10

#### 功能

* 将“选择启用”和“选择禁用”的概念组合在 `Consent` 下，并添加了新的 `setConsent` 命令。
* 添加了类型为 `XDM Object` 的新数据元素，这种类型的数据元素允许从 JavaScript/JSON 映射到 XDM。

## 2020 年 2 月 18 日

### Adobe Experience Platform Web SDK 0.0.7

#### 功能

* 删除了 idSyncContainerId、datasetId、schemaId、urlDestinationsEnabled 和 cookieDestinationsEnabled 选项
* 添加了对 edgeDomain 选项值中连字符的支持
* 在 ID 迁移期间发出的请求将发送到 demdex 端点，以改进未设置 demdex Cookie 时的跨域识别
* 在 ID 迁移过程中发出的请求始终需要响应，以确保设置身份标识 Cookie
* 执行无效命令时，控制台中将记录有效命令名称列表
* 向 Adobe Experience Platform Launch 扩展中添加了用于切换第三方 Cookie 支持的复选框。这将禁用对 demdex.net 的调用

## 2019 年 12 月 20 日

### Adobe Experience Platform Web SDK 0.0.5

#### 功能

* 将活动跟踪器配置添加到 Platform Launch 扩展
* 在事件命令中公开 EventType 和 EventMergeId
* 将 onBeforeEventSend 配置添加到 Platform Launch 扩展
* 将 edgeBasePath 配置添加到 Platform Launch 扩展

#### 更新至 Alloy v. 0.0.10，此版本包括以下更改:

* 实施客户端存储: 状态和 Cookie 逻辑已移至服务器
* 在事件命令中公开 EventType 和 EventMergeId
* 除退出链接以外，使用 sendBeacon 进行链接跟踪
* 恢复 ID 同步但不检查是否到期
* setCustomerIds 命令不会对非 SSL (http) 页面上的 ID 进行哈希处理
* 将 APEX 域传递到要在设置状态/Cookie 时使用的服务器
* 从使用新句柄类型的响应中获取 ECID
* 删除“激活和标识”配置的默认值
* 重命名并将查询选项移动到元
* 旧版 ECID 迁移

#### 错误修复

* 出现意外的状态代码时，解析并格式化错误消息的响应正文
* 运行调试命令或使用 alloy_debug 会被配置覆盖

## 2019 年 11 月 25 日

### Adobe Experience Platform Web SDK 0.0.3

#### 功能

* 在“Send Event”（发送事件）操作中，新增了“Merge ID”（合并 ID）和“Type”（类型）字段。“Merge ID”（合并 ID）映射到 XDM 架构中的 `xdm.eventMergeID`；“Type”（类型）则映射到 XDM 架构中的 `xdm.eventType`。
* 改进了错误处理和报告功能
* 现在，`sendBeacon` 可用于所有链接

#### 错误修复

* 修复了这样一个问题：通过一个查询字符串参数或使用 `debug` 命令切换调试时，不能在会话中持续。

## 2019 年 11 月 18 日

### Adobe Experience Platform Web SDK 0.0.2

#### 功能

* 扩展快速形成
* ECID 支持无需其他库或网络调用
* 选择加入支持
* 支持将XDM发送到平台
* 第一方域支持
* 自动收集浏览器上下文
* 完全开放源（[扩展](https://github.com/adobe/reactor-extension-alloy)、[SDK](https://github.com/adobe/reactor-extension-alloy)）
* 详细记录
* 隐藏生产中错误的能力
