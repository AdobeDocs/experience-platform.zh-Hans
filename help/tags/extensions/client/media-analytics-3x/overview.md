---
title: Adobe Medium Analytics (3.x SDK) for Audio and Video擴充功能概觀
description: 瞭解Adobe Experience Platform中的Adobe Medium Analytics (3.x SDK) for Audio and Video標籤擴充功能。
exl-id: 7289d57d-7e7f-4832-9469-3b5a62183a32
source-git-commit: e21ed1e9fd0c2678551cfc664b611076c198a157
workflow-type: tm+mt
source-wordcount: '752'
ht-degree: 74%

---

# Adobe Medium Analytics (3.x SDK) for Audio and Video擴充功能概觀

>[!NOTE]
>
>Adobe Experience Platform Launch已經過品牌重塑，現在是Adobe Experience Platform中的一套資料收集技術。 因此，产品文档中的术语有一些改动。有关术语更改的综合参考，请参阅以下[文档](../../../term-updates.md)。

使用本文档了解有关安装、配置和实施 Adobe Media Analytics (3.x SDK) for Audio and Video 扩展（Media Analytics 扩展）的信息。其中包括使用此扩展构建规则时可用的选项，以及一些示例和指向示例的链接。

Media Analytics (MA) 扩展添加了核心 JavaScript Media SDK (Media 3.x SDK)。此擴充功能提供新增 `Media` 追蹤器例項至啟用標籤的網站或專案。 MA 扩展需要使用其他两个扩展：

* [Analytics 扩展](../analytics/overview.md)
* [Experience Cloud ID 扩展](../id-service/overview.md)

>[!IMPORTANT]
>
>此扩展随 Media 3.x SDK 一起部署，无法向后兼容 Media 2.x SDK。自2.x版已棄用，請更新至3.x版。

在啟用標籤的專案中納入上述的三個擴充功能後，您可以使用下列兩種方式之一繼續操作：

* 使用您的 Web 应用程序中的 `Media` API
* 包含或构建特定于播放器的扩展，以便将特定媒体播放器事件映射到 `Media` 跟踪器实例上的 API。此实例将通过 MA 扩展公开。

## 安装和配置 MA 扩展

* **安裝：** 若要安裝MA擴充功能，請開啟您的擴充功能屬性，選取 **[!UICONTROL 擴充功能>目錄]**，將游標暫留在 **[!UICONTROL 適用於音訊和視訊的Adobe Medium Analytics (3.x SDK)]** 擴充功能，並選取 **[!UICONTROL 安裝]**.

* **設定：** 若要設定MA擴充功能，請開啟 [!UICONTROL 擴充功能] 索引標籤，將游標停留在擴充功能上，然後選取「 」 **[!UICONTROL 設定]**：

![MA 扩展配置](../../../images/ext-ma-config.png)

### 配置选项：

| 选项 | 描述 |
| :--- | :--- |
| 收集 API 服务器 | 定义媒体收集 API 服务器（请联系 Adobe 代表以获取此服务器） |
| Application Version | 媒体播放器应用程序/SDK 的版本 |
| Player Name | 正在使用的媒体播放器的名称（例如“AVPlayer”、“HTML5 播放器”、“我的自定义视频播放器”） |
| Channel | 渠道名称属性 |
| Debug Logging | 启用或禁用日志记录 |
| Enable SSL | 允许或禁止通过 HTTPS 发送 ping |
| Export APIs to Window Object | 允许或禁止将 Media Analytics API 导出到全局范围 |
| Variable Name | `window` 对象下用于导出 Media Analytics API 的变量 |

**提醒：** MA 扩展要求使用 [Analytics](../analytics/overview.md) 和 [Experience Cloud ID](../id-service/overview.md) 扩展。您还必须将这些扩展添加到您的扩展资产并对其进行配置。

## 使用 MA 扩展

### 通过网页/JS 应用程序使用

MA擴充功能會啟用「 」中的「匯出視窗物件API」設定，匯出全域視窗物件中的Media API。 [!UICONTROL 設定] 頁面。 它将在配置的变量名称下导出 API。例如，如果变量名称配置为 `ADB`，则 `window.ADB.Media` 可以访问 Media API。

>[!IMPORTANT]
>
>MA 扩展仅在 `window["CONFIGURED_VARIABLE_NAME"]` 未定义时才导出 API，并且不会覆盖现有变量。

1. **Media API：**`window["CONFIGURED_VARIABLE_NAME"].Media`

   这会公开 Media SDK 中的所有 API 和常量：[https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript_3x/APIReference.html](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript_3x/APIReference.html)

1. **创建媒体跟踪器实例：**`window["CONFIGURED_VARIABLE_NAME"].Media.getInstance`

   **返回值：**&#x200B;用于跟踪媒体会话的 `Media` 跟踪器实例。

   ```javascript
   var Media = window["CONFIGURED_VARIABLE_NAME"].Media;
   
   var tracker = Media.getInstance();
   ```

1. 使用媒体跟踪器实例，按照 [JS API 文档](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript_3x/index.html)来实施媒体跟踪。

您可在此处获得示例播放器：[MA 示例播放器](https://github.com/Adobe-Marketing-Cloud/media-sdks/tree/master/samples/launch/js/3.x)。示例播放器作为参考，展示了如何使用 MA 扩展直接从 Web 应用程序支持 Media Analytics。


### 通过其他扩展使用

MA擴充功能會公開 `media` 作為其他擴充功能的共用模組。 （有关共享模块的其他信息，请参阅[共享模块文档](../../../extension-dev/web/shared.md)。）

>[!IMPORTANT]
>
>只能从其他扩展访问共享模块。也就是说，网页/JavaScript 应用程序既无法访问共享模块，也无法在扩展之外使用 `turbine`（请参阅下面的代码示例）。

1. **Media API：**`media`共享模块

   这会公开 Media SDK 中的所有 API 和常量：[https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript_3x/APIReference.html](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript_3x/APIReference.html)

1. 按如下方式创建媒体跟踪器实例：

   **返回值：**&#x200B;用于跟踪媒体会话的 `Media` 跟踪器实例。

   ```javascript
   var Media =
     turbine.getSharedModule('adobe-media-analytics', 'media');
   
   var tracker = Media.getInstance();
   ```

1. 使用媒体跟踪器实例，按照 [JS API 文档](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript_3x/index.html)来实施媒体跟踪。

>[!NOTE]
>
>**测试：**&#x200B;对于此版本，要测试您的扩展，必须将其上传到 [ Platform ](../../../extension-dev/submit/upload-and-test.md)，您可以在其中访问所有依赖的扩展。
