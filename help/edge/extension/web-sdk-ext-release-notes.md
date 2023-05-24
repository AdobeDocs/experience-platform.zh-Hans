---
title: Adobe Experience Platform Web SDK擴充功能發行說明
description: Adobe Experience Platform Web SDK標籤擴充功能
exl-id: 91de8c91-023a-45b6-9f67-ac75ee471e50
source-git-commit: edd1745467a95804681b5d6c6d33458329641c39
workflow-type: tm+mt
source-wordcount: '1663'
ht-degree: 38%

---


# Adobe Experience Platform Web SDK擴充功能發行說明

本檔案涵蓋Adobe Experience Platform Web SDK標籤擴充功能的發行說明。 如需SDK本身的最新發行說明，請參閱 [Platform Web SDK發行說明](https://experienceleague.adobe.com/docs/experience-platform/edge/release-notes.html).

## 2.17.0版 — 2023年4月25日

**新增功能**

* 包含2.16.0版的Adobe Experience Platform Web SDK。
* 新增支援 [資料流設定覆寫](../datastreams/overrides.md).
* 將淘汰通知新增至 `datasetId` 上的選項 `sendEvent` 命令。


**修复和改进功能**

* 修正Safari中的捲動會關閉資料流選擇器的問題。

## 2.16.1版 — 2023年4月14日

* 修正XDM物件和變數資料元素無法從非預設沙箱選取結構描述的問題。

## 2.16.0版 — 2023年3月30日

**新增功能**

* （測試版）已新增 **[!UICONTROL 更新變數]** 動作和 **[!UICONTROL 變數]** 資料元素。
* 已新增的設定 [`onBeforeLinkClickSend`](../fundamentals/configuring-the-sdk.md#onBeforeLinkClickSend) 回呼函式。

**修复和改进功能**

* 修正在錨點標籤內點選元素時無法運作的問題。 **[!UICONTROL 使用身分重新導向]** 已使用動作。
* 修正只有一個結構描述時，XDM物件資料元素無法運作的問題。
* 包含2.15.0版的Adobe Experience Platform Web SDK。


## 2.15.1版 — 2023年1月26日

* 修正無權存取資料串流的使用者無法編輯擴充功能設定的問題。
* 新增對中的曲面的支援 `sendEvent` 動作。

包含2.14.0版Adobe Experience Platform Web SDK。


## 2.14.1版 — 2022年10月13日

* 修正Web SDK未採用來自Experience CloudID服務的ID的問題。

包含2.13.1版的Adobe Experience Platform Web SDK程式庫。

## 2.14.0版 — 2022年9月28日

* 已新增 `targetMigrationEnabled` 可逐頁完整移轉的設定。
* 新增套用回應動作，以啟用混合式伺服器 — 使用者端實作。
* 新增高平均資訊量使用者代理程式使用者端提示內容選項。

包含2.13.0版的Adobe Experience Platform Web SDK程式庫。

## 2.13.0版 — 2022年6月29日

* 修正XDM物件資料元素（例如eVars）中數值屬性的排序順序。

包含2.12.0版的Adobe Experience Platform Web SDK程式庫。

## 2.12.0版 — 2022年6月13日

* 已更新 `identityMap` 資料元素，以根據擴充功能設定所定義的沙箱填入名稱空間選項。
* 已新增 **[!UICONTROL 使用身分重新導向]** 動作以允許跨網域身分共用。
* 新增檔案連結至 `sendEvent` 動作。
* 升級React Spectrum UI程式庫。
* 多項使用者介面增強功能。

包含2.11.0版的Adobe Experience Platform Web SDK程式庫。

## 2.11.2版 — 2022年5月3日

包含2.10.1版的Adobe Experience Platform Web SDK程式庫。

## 2.11.1版 — 2022年4月22日

* 修正2.11.0版中的設定命令錯誤。

包含2.10.0版的Adobe Experience Platform Web SDK程式庫。

## 2.11.0版 — 2022年4月22日

* 已改善標籤UI效能。
* 將沙箱選擇器新增到資料串流擴充功能設定。

包含2.10.0版的Adobe Experience Platform Web SDK程式庫。

## 2.10.0版 — 2022年3月10日

* 更新可在設定頁面上複製的預先隱藏程式碼片段，以搭配更新的Adobe Target VEC編輯器使用。

包含 Adobe Experience Platform Web SDK 库的版本 2.9.0。

## 2.9.0版 — 2022年1月19日

包含 Adobe Experience Platform Web SDK 库的版本 2.8.0。

## 2.8.0版 — 2021年10月26日

包含 Adobe Experience Platform Web SDK 库的版本 2.7.0。

* 「傳送事件完成」事件中提供Experience Edge的其他資訊，包括 `inferences` 和 `destinations`. 這些屬性的格式可能會隨著這些功能目前在Beta版中推出而改變。 如需詳細資訊，請參閱 [追蹤事件。](../fundamentals/tracking-events.md)

## 2.7.3版 — 2021年9月7日

包含 Adobe Experience Platform Web SDK 库的版本 2.6.4。

* 「 」不再出現「淘汰」警告 `container.buildInfo.environment.`

## 2.7.0版 — 2021年8月16日

包含 Adobe Experience Platform Web SDK 库的版本 2.6.3。

* 使用「身分對應」資料元素型別時，其ID解析為未填入字串之值的識別碼現在會自動從身分對應中移除。
* 修正嘗試使用XDM物件資料元素型別儲存資料元素時，若未選取任何結構描述時發生的錯誤。
* 改善使用者介面印刷樣式。

## 2.6.2版 — 2021年8月4日

包含 Adobe Experience Platform Web SDK 库的版本 2.6.2。

## 2.6.1版 — 2021年7月29日

包含 Adobe Experience Platform Web SDK 库的版本 2.6.1。

## 2.6.0版 — 2021年7月27日

包含 Adobe Experience Platform Web SDK 库的版本 2.6.0。

* 使用術語「邊緣設定」的標籤、說明和錯誤訊息已變更為使用術語「資料流」，以符合最新的Adobe Experience Platform術語。
* 在擴充功能設定檢視中，新增了處理大量資料串流和資料串流環境的支援。
* 在XDM物件資料元素檢視中，新增了處理大量結構描述的支援。
* 已新增「傳送事件完成」事件型別，可用於在事件已傳送至伺服器並收到回應後執行規則。 近期將提供更多檔案。
* 已棄用「收到的決定」事件型別。 請改用傳送事件完成事件型別。
* 使用者介面和錯誤處理已普遍改善。

## 2.5.0版 — 2021年6月1日

包含 Adobe Experience Platform Web SDK 库的版本 2.5.0。

* 已新增 `data` 「傳送事件」動作的欄位。 即將推出的檔案將說明如何在特定情況下使用此功能。
* 在XDM物件資料元素檢視上，已修正如果使用者有權存取Adobe Experience Platform沙箱，但無權存取設定為組織預設的沙箱，則會擲回錯誤的問題。
* 在XDM物件資料元素檢視上，即使父物件不包含任何值，必要結構描述欄位仍會被視為無效的問題，已獲得修正。

## 2.4.0版 — 2021年3月9日

包含 Adobe Experience Platform Web SDK 库的版本 2.4.0。

* 已新增 [&quot;document unloading&quot;](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/tracking-events.html?lang=en#using-the-sendbeacon-api) 核取方塊以傳送事件動作UI。
* 新增對的支援 `out` 選項時機 [設定預設同意](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#default-consent) 會捨棄所有事件，直到收到同意為止(現有 `pending` 選項會將事件排入佇列，並在收到同意後傳送事件)。
* 新增工具提示至預設同意欄位。
* 新增支援 [Adobe的Consent 2.0標準](https://experienceleague.adobe.com/docs/experience-platform/edge/consent/supporting-consent.html?communicating-consent-preferences-via-the-adobe-standard).
* 如果使用者的存取權杖無效或布建不正確，XDM物件資料元素UI中現在會顯示更好的錯誤。
* 修正檢視XDM物件資料元素時，瀏覽器開發人員主控台顯示的跨來源錯誤（不會影響擴充功能的操作）。

## 2.3.0版 — 2020年11月4日

包含 Adobe Experience Platform Web SDK 库的版本 2.3.0。

* 添加了对配置默认同意的过程中使用数据元素的支持。
* 添加了通过 XDM 对象数据元素类型搜索 XDM 模式的功能。
* 将 XDM 数据克隆添加到“发送事件”操作类型中，以确保任何对 XDM 数据对象的后续更改将不会反映在请求中。

## 2.2.0版 — 2020年10月1日

* 当客户尝试按照沙盒模式创建 XDM 对象时，他们将会遇到身份验证问题。呼叫Platform的API現在可感知環境，因此使用者只會看到他們有權編輯的結構描述。
* 使用時 `identityMap` 資料元素中，下拉式清單現在會預先填入名稱空間，因此您不必手動填寫。
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
* 支援在XDM物件資料元素中選擇Platform沙箱。

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
* 啟用偵錯，使用 `_satellite` 現在會在Adobe Experience Platform Web SDK中啟用除錯功能。
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
* 在標籤擴充功能中新增切換第三方Cookie支援的核取方塊。 这将禁用对 demdex.net 的调用

## 0.0.5版 — 2019年12月20日

* 將活動追蹤器設定新增至標籤擴充功能
* 在事件命令中公开 EventType 和 EventMergeId
* 將onBeforeEventSend設定新增至標籤延伸模組
* 將edgeBasePath設定新增至標籤延伸模組

## 0.0.3版 — 2019年11月25日

* 在“Send Event”（发送事件）操作中，新增了“Merge ID”（合并 ID）和“Type”（类型）字段。“Merge ID”（合并 ID）映射到 XDM 架构中的 `xdm.eventMergeID`；“Type”（类型）则映射到 XDM 架构中的 `xdm.eventType`。

## 0.0.2版 — 2019年11月18日

* 初始版本
