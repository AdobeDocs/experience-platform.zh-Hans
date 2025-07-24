---
title: Adobe Experience Platform Web SDK扩展发行说明
description: Adobe Experience Platform Web SDK标记扩展
exl-id: 91de8c91-023a-45b6-9f67-ac75ee471e50
source-git-commit: cf8912aea5c46b3414486f638b92eebf556528a9
workflow-type: tm+mt
source-wordcount: '2733'
ht-degree: 24%

---


# Web SDK扩展发行说明

本文档介绍Adobe Experience Platform Web SDK标记扩展的发行说明。 有关SDK本身的最新发行说明，请参阅[Experience Platform Web SDK发行说明](/help/web-sdk/release-notes.md)。

## 2.31.0版 — 2025年7月24日

**新增功能**

- 包含Adobe Experience Platform Web SDK的[版本2.28.0](../../../../web-sdk/release-notes.md#2-28-0)。

**修复和改进**

- 修复了通过数据元素启用数据流覆盖时引发错误的问题。
- 修复了空`idSyncContainerId`覆盖将引发错误的问题。
- 解析媒体数据元素时，现在包含事件对象。

## 2.30.1版 — 2025年5月27日

**修复和改进**

- 修复了当组织未设置默认沙盒时更新变量视图崩溃的问题。

## 2.30.0版 — 2025年5月21日

**新增功能**

- 现在，您可以在启用第三方Cookie时指定数据元素。
- 向代码字段添加了清除按钮。
- 包含Adobe Experience Platform Web SDK的[版本2.27.0](../../../../web-sdk/release-notes.md#2-27-0)。

**修复和改进**

- 添加了验证，以防止在启用事件分组时设置`onBeforeLinkClickSend`。

## 版本2.29.1 - 2025年5月8日

**修复和改进**

- 修复了在编辑后立即单击“保存”时设置未保存的问题。

## 版本2.29.0 - 2025年3月5日

**新增功能**

- 您现在可以创建自定义Web SDK内部版本，并从标记扩展用户界面中选择所需的组件。 通过排除未使用的组件，这可能会导致生成更小的版本。 请参阅有关[创建自定义Web SDK内部版本](web-sdk-extension-configuration.md#custom-build)的文档。
- 包含Adobe Experience Platform Web SDK的[版本2.26.0](../../../../web-sdk/release-notes.md#2-26-0)。

**修复和改进**

- 在[更新变量](action-types.md#update-variable)操作中添加了对缺少的数据元素的正常处理。 以前，编辑缺少数据元素的更新变量操作会显示错误消息。 现在，您可以选择其他数据元素，并且更新变量操作的所有设置仍会应用。 如果删除数据元素或复制Tags属性，则可能缺少数据元素。
- 添加了对使用[带有标识](action-types.md#redirect-with-identity)的重定向操作打开新选项卡的支持。 现在，使用操作时，在重定向浏览器时使用锚点标记的`target`属性。
- 修复了在配置覆盖中无法禁用Adobe Audience Manager的问题。

## 版本2.28.0 - 2025年1月23日

**修复和改进**

- 修复了在未启用Audience Manager的情况下无法设置ID同步容器覆盖的问题。
- 修复了在升级到最新版本时禁用数据流配置覆盖的问题。
- 修复了用户无法保存Target自动点击收藏集设置的问题。

**新增功能**

- 添加了新功能，以便在XDM对象中的技术名称和显示名称之间进行切换。
- 包含Adobe Experience Platform Web SDK的[版本2.25.0](../../../../web-sdk/release-notes.md#2-25-0)。

## 版本2.27.0 - 2024年10月31日

**新增功能**

- [数据流覆盖](../web-sdk/web-sdk-extension-configuration.md#datastream-overrides)现在包含用于禁用Experience Cloud解决方案和Adobe Experience Platform服务的设置。
- 您现在可以为媒体会话创建[数据流覆盖](../web-sdk/web-sdk-extension-configuration.md)。

包含2.24.0版本的Adobe Experience Platform Web SDK。

## 版本2.26.1 - 2024年9月19日

**修复和改进**

- 修复了在本地运行Web SDK时无法正确写入Cookie的问题。

包含2.23.0版本的Adobe Experience Platform Web SDK。

## 版本2.26.0 - 2024年8月22日

**新增功能**

- 已添加监视挂接`triggered`事件。
- [引导式事件](action-types.md#instance)、[请求默认个性化](action-types.md#personalization)、[订阅规则集项](event-types.md#subscribe-ruleset-items)和[评估规则集](action-types.md#evaluate-rulesets)现已正式可用。

**修复和改进**

- 修复了重复的变量数据元素可能会相互覆盖的问题。
- 使用[请求默认个性化](action-types.md#personalization)引导式事件时，现在会自动启用可视化个性化决策。

包含2.22.0版本的Adobe Experience Platform Web SDK。

## 2.25.0版 — 2024年7月18日

**新增功能**

- 在Adobe Journey Optimizer中添加了对自动跟踪个性化的支持。
- 引入了新设置，用于管理改进的点击收藏集。

包含2.21.1版本的Adobe Experience Platform Web SDK。

## 版本2.24.0 - 2024年6月5日

**修复和改进**

- 修复了在定义配置覆盖时修改扩展配置时发生的错误。
- 允许为媒体收集Ping间隔设置空值。
- 修复了在修改更新变量操作时发生的错误。
- 允许重置配置覆盖中的ID同步容器。

包含2.20.0版本的Adobe Experience Platform Web SDK。

## 2.23.1版 — 2024年5月28日

**新增功能**

- 在扩展配置中添加了对[`Streaming Media Collection`](web-sdk-extension-configuration.md#streaming-media)组件的支持。
- 为[`Send Media Event`](action-types.md#send-media-event)功能添加了[!DNL Streaming Media Collection]操作。
- 为[`Media: Quality of Experience`](data-element-types.md#quality-experience)功能添加了[!DNL Streaming Media Collection]数据元素。

包含2.20.0版本的Adobe Experience Platform Web SDK。

**修复和改进**

- 修复了在[更新变量](action-types.md#update-variable)操作中搜索数据元素时发生的错误。
- 已从建议在[!UICONTROL 操作中使用的事件类型中删除]媒体`sendEvent`事件类型。

## 版本2.22.0 - 2024年5月3日

**新增功能**

- 扩展变量数据元素以支持数据对象。
- 更新变量操作现在支持修改传递的Adobe Analytics、Adobe Audience Manager和Adobe Target数据。

包含2.19.2版本的Adobe Experience Platform Web SDK。

## 版本2.21.4 - 2024年1月10日

**修复和改进**

- 修复了在未设置所有3个环境的情况下保存配置覆盖将会导致扩展UI崩溃的问题。
- 修复了在编辑更新变量操作时，根清除现有值复选框未填充的问题。

包含2.19.2版本的Adobe Experience Platform Web SDK。

## 版本 2.21.3 - 2023 年 11 月 10 日

包含2.19.1版本的Adobe Experience Platform Web SDK。

**修复和改进**

- 修复了`Send event complete`事件中可用的建议数组始终为空的问题。

## 版本2.21.2 - 2023年11月1日

**新增功能**

- 添加了用于发送事件操作的`Request default personalization`选项。
- 在“发送事件”操作中添加了对页面事件顶部和底部的支持。
- 添加了`Apply propositions`操作。
- 为应用程序内消息添加了`Evaluate rulesets`操作和`Subscribe ruleset items`事件。
- 已添加`Decision context`以发送事件操作。

**修复和改进**

- 包含2.19.0版本的Adobe Experience Platform Web SDK。

## 版本2.20.3 - 2023年8月8日

**修复和改进**

- 修复了数据元素无法保存在ID同步容器ID覆盖字段中的问题。

## 版本2.20.1 - 2023年8月3日

**修复和改进**

- 改进了已保存数据流覆盖设置的验证。

## 2.20.0版 — 2023年7月31日

**新增功能**

- 添加了对数据流ID[的每命令](../../../../datastreams/overrides.md)覆盖的支持。

**修复和改进**

- 已在SDK配置中弃用`edgeConfigId`以支持`datastreamId`。
- 数据流配置的多个用户体验增强功能会覆盖用户界面。

## 2.19.0版 — 2023年6月21日

- **[!UICONTROL 变量]**&#x200B;数据元素和&#x200B;**[!UICONTROL 更新变量]**&#x200B;操作现已正式可用。

## 2.18.0版 — 2023年5月18日

- 包含2.17.0版本的Adobe Experience Platform Web SDK。

## 版本2.17.0 - 2023年4月25日

**新增功能**

- 包含2.16.0版本的Adobe Experience Platform Web SDK。
- 添加了对[数据流配置覆盖](/help/datastreams/overrides.md)的支持。
- 向`datasetId`命令上的`sendEvent`选项添加弃用通知。

**修复和改进**

- 修复了Safari中的滚动操作将关闭数据流选择器的问题。

## 版本2.16.1 - 2023年4月14日

- 修复了XDM对象和变量数据元素的一个问题，该问题导致您无法从非默认沙盒中选择架构。

## 版本2.16.0 - 2023年3月30日

**新增功能**

- (Beta)已添加&#x200B;**[!UICONTROL Update variable]**&#x200B;操作和&#x200B;**[!UICONTROL Variable]**&#x200B;数据元素。
- 添加了[`onBeforeLinkClickSend`](/help/web-sdk/commands/configure/onbeforelinkclicksend.md)回调函数的配置。

**修复和改进**

- 修复了在使用具有标识&#x200B;**[!UICONTROL 的]**&#x200B;重定向操作时，导致单击锚点标记中的元素无法正常工作的问题。
- 修复了仅存在一个架构时，XDM对象数据元素无法工作的问题。
- 包含Adobe Experience Platform Web SDK的版本2.15.0。

## 版本2.15.1 - 2023年1月26日

- 修复了无权访问数据流的用户无法编辑扩展配置的问题。
- 在`sendEvent`操作中添加了对表面的支持。

包含Adobe Experience Platform Web SDK的版本2.14.0。

## 版本2.14.1 - 2022年10月13日

- 修复了Web SDK不接受来自Experience Cloud ID服务的ID的问题。

包含Adobe Experience Platform Web SDK库的版本2.13.1。

## 版本2.14.0 - 2022年9月28日

- 添加了新的`targetMigrationEnabled`配置，该配置支持逐页完全迁移。
- 添加了应用响应操作以启用混合服务器 — 客户端实施。
- 添加了高熵用户代理客户端提示上下文选项。

包含Adobe Experience Platform Web SDK库的版本2.13.0。

## 版本2.13.0 - 2022年6月29日

- 修复了XDM对象数据元素（例如eVar）中数值属性的排序顺序。

包含Adobe Experience Platform Web SDK库的版本2.12.0。

## 版本2.12.0 - 2022年6月13日

- 更新了`identityMap`数据元素，以根据扩展设置定义的沙盒填充命名空间选项。
- 添加了允许跨域身份共享的&#x200B;**[!UICONTROL 重定向（带有标识]**）操作。
- 添加了指向`sendEvent`操作的文档链接。
- 升级了React Spectrum UI库。
- 多个用户界面增强。

包含Adobe Experience Platform Web SDK库的版本2.11.0。

## 版本2.11.2 - 2022年5月3日

包含Adobe Experience Platform Web SDK库的版本2.10.1。

## 版本2.11.1 - 2022年4月22日

- 修复了2.11.0版中的配置命令错误。

包含Adobe Experience Platform Web SDK库的版本2.10.0。

## 版本2.11.0 - 2022年4月22日

- 改进了标记UI性能。
- 将沙盒选择器添加到数据流扩展配置。

包含Adobe Experience Platform Web SDK库的版本2.10.0。

## 版本2.10.0 - 2022年3月10日

- 更新可在配置页面上复制的预隐藏代码片段，以便与更新后的Adobe Target VEC编辑器配合使用。

包含 Adobe Experience Platform Web SDK 库的版本 2.9.0。

## 版本2.9.0 - 2022年1月19日

包含 Adobe Experience Platform Web SDK 库的版本 2.8.0。

## 版本 2.8.0 - 2021 年 10 月 26 日

包含 Adobe Experience Platform Web SDK 库的版本 2.7.0。

- 发送事件完成事件中提供了来自Edge Network的其他信息，包括`inferences`和`destinations`。 由于这些功能当前正在作为Beta的一部分推出，因此这些属性的格式可能会发生更改。

## 版本2.7.3 - 2021年9月7日

包含 Adobe Experience Platform Web SDK 库的版本 2.6.4。

- `container.buildInfo.environment.`不再有弃用警告

## 版本2.7.0 - 2021年8月16日

包含 Adobe Experience Platform Web SDK 库的版本 2.6.3。

- 使用身份映射数据元素类型时，其ID解析为未填充字符串的值的标识符现在将自动从身份映射中删除。
- 修复了尝试使用XDM对象数据元素类型保存数据元素时发生的错误，并且未选择架构。
- 改进了用户界面排版规则。

## 版本2.6.2 - 2021年8月4日

包含 Adobe Experience Platform Web SDK 库的版本 2.6.2。

## 版本2.6.1 - 2021年7月29日

包含 Adobe Experience Platform Web SDK 库的版本 2.6.1。

## 2.6.0版 — 2021年7月27日

包含 Adobe Experience Platform Web SDK 库的版本 2.6.0。

- 使用术语“边缘配置”的标签、描述和错误消息已更改为使用术语“数据流”以符合最新的Adobe Experience Platform术语。
- 在扩展配置视图中，增加了对处理大量数据流和数据流环境的支持。
- 在XDM对象数据元素视图中，增加了对处理大量架构的支持。
- 已添加“发送事件完成”事件类型，该事件类型可用于在将事件发送到服务器并收到响应后运行规则。 更多文档将很快发布。
- 已弃用接收决策的事件类型。 请改用发送事件完成事件类型。
- 用户界面和错误处理已得到普遍改进。

## 版本2.5.0 - 2021年6月1日

包含 Adobe Experience Platform Web SDK 库的版本 2.5.0。

- 向Send Event操作添加了`data`字段。 即将发布的文档将介绍如何在特定情况下使用它。
- 在XDM对象数据元素视图中，修复了以下问题：如果用户有权访问Adobe Experience Platform沙盒，但没有访问配置为组织默认值的沙盒，则会引发错误。
- 在XDM对象数据元素视图中，修复了即使父对象不包含任何值，必填架构字段也会被视为无效的问题。

## 版本2.4.0 - 2021年3月9日

包含 Adobe Experience Platform Web SDK 库的版本 2.4.0。

- 添加了[“文档卸载”](/help/web-sdk/commands/sendevent/documentunloading.md)复选框以发送事件操作UI。
- 在`out`配置默认同意[时添加了对](/help/web-sdk/commands/configure/defaultconsent.md)选项的支持，该默认同意会丢弃所有事件直到收到同意为止（现有`pending`选项将事件排入队列，并在收到同意后发送这些事件）。
- 向默认同意字段添加了工具提示。
- 添加了对使用[`setConsent`](/help/web-sdk/commands/setconsent.md)命令时Adobe的Consent 2.0标准的支持。
- 如果用户的访问令牌无效或配置不正确，则XDM对象数据元素UI中现在会显示更好的错误。
- 修复了在查看XDM对象数据元素时浏览器开发人员控制台上显示的跨源错误（不会影响扩展的操作）。

## 版本2.3.0 - 2020年11月4日

包含 Adobe Experience Platform Web SDK 库的版本 2.3.0。

- 添加了对配置默认同意的过程中使用数据元素的支持。
- 添加了通过 XDM 对象数据元素类型搜索 XDM 架构的功能。
- 将 XDM 数据克隆添加到“发送事件”操作类型中，以确保任何对 XDM 数据对象的后续更改将不会反映在请求中。

## 版本2.2.0 - 2020年10月1日

- 当客户尝试按照沙盒架构创建 XDM 对象时，他们将会遇到身份验证问题。由于调用Experience Platform的API现在能够识别环境，因此用户只会看到他们有权编辑的架构。
- 使用`identityMap`数据元素时，命名空间现在会预填充到下拉列表中，因此您不必手动进行填充。
- 翻新了 `xdmObject` 数据元素的 UI。在新的 UI 中，您无需输入对象中的每个项目，即可查看已填充字段。

## 版本2.1.1 - 2020年8月26日

- 修复了 XDM 对象视图上的 Adobe Experience Platform 沙盒显示不正确的问题。在使用该扩展版本时，如果列表中未显示预期的沙盒，则用户应与其 Adobe Experience Platform 管理员确认，以确保设置正确的访问权限。

## 版本2.1.0 - 2020年8月5日

- 重大变更：移除了 `syncIdentity` 操作，取而代之，在 `sendEvent` 操作中支持传递这些 ID。请在升级扩展之前，通过这项操作来禁用任何现有规则。
- 更新至 Alloy v. 2.1.0（[发行说明](/help/web-sdk/release-notes.md)）
- 在 `setConsent` 操作中支持 IAB 2.0 Consent Standard。
- 在 `sendEvent` 操作中支持覆盖数据集 ID。
- 增加了 `IdentityMap` 类型的新数据元素，该数据元素可用于在（现已启用的）XDM 对象数据元素和 `setConsent` 操作中填充 `identityMap` 条目。
- 在 `setConsent` 操作中支持传递身份标识映射。
- 支持在XDM对象数据元素中选择Experience Platform沙盒。

## 1.0.0版 — 2020年5月26日

- 支持从配置服务中选择环境。

## 0.1.2版 — 2020年5月4日

- 将 `configId` 重命名为 `edgeConfigId`。
- 将 `viewStart` 重命名为 `renderDecisions`，默认情况下设置为 false。如果设置为 true，则会获取并自动渲染个性化内容。
- 与 `Get Decisions` 相关的更改：
   - 删除了 `getDecisions` 命令。
   - 为 `sendEvent` 命令添加了一个 `scopes` 选项。将在 `sendEvent` 已解决的承诺中返回决策。
   - 添加了内置 `__view__` 范围，该范围将导致返回页面/视图范围的内容。（例如，Target中的VEC选件。）
仅当`sendEvent`设置为false时，才会从`renderDecisions`命令返回这些决策。
   - 添加了一个 `Decisions Received` 事件，当决策可用时会触发此事件。
- 在单个服务器调用下合并多个个性化通知。
- 修复了每次引用数据元素时都会重置事件合并 ID 的问题。
- 将 `setCustomerIds` 操作重命名为 `syncIdentity`。
- 添加了一个 `getIdentity` 命令。现在只能通过自定义代码使用此命令。
- 现在，允许使用`_satellite`进行调试可在Adobe Experience Platform Web SDK中进行调试。
- 添加了对 XDM 对象中键入值的支持：布尔值、数字和小数。

## 0.0.10版 — 2020年3月16日

- 将“选择启用”和“选择禁用”的概念组合在 `Consent` 下，并添加了新的 `setConsent` 命令。
- 添加了类型为 `XDM Object` 的新数据元素，这种类型的数据元素允许从 JavaScript/JSON 映射到 XDM。

## 0.0.7版 — 2020年2月18日

- 删除了 idSyncContainerId、datasetId、schemaId、urlDestinationsEnabled 和 cookieDestinationsEnabled 选项
- 添加了对 edgeDomain 选项值中连字符的支持
- 在 ID 迁移期间发出的请求将发送到 demdex 端点，以改进未设置 demdex Cookie 时的跨域识别
- 在 ID 迁移过程中发出的请求始终需要响应，以确保设置身份标识 Cookie
- 执行无效命令时，控制台中将记录有效命令名称列表
- 向标记扩展中添加了用于切换第三方Cookie支持的复选框。 这将禁用对 demdex.net 的调用

## 0.0.5版 — 2019年12月20日

- 将活动跟踪器配置添加到标记扩展
- 在事件命令中公开 EventType 和 EventMergeId
- 将onBeforeEventSend配置添加到标记扩展
- 将edgeBasePath配置添加到标记扩展

## 0.0.3版 — 2019年11月25日

- 在“Send Event”（发送事件）操作中，新增了“Merge ID”（合并 ID）和“Type”（类型）字段。“Merge ID”（合并 ID）映射到 XDM 架构中的 `xdm.eventMergeID`；“Type”（类型）则映射到 XDM 架构中的 `xdm.eventType`。

## 0.0.2版 — 2019年11月18日

- 初始版本
