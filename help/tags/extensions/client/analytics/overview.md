---
title: Adobe Analytics擴充功能概觀
description: 瞭解Adobe Experience Platform中的Adobe Analytics標籤擴充功能。
exl-id: 33ebdcb6-9bf0-44e6-b016-e93fe78af578
source-git-commit: 88939d674c0002590939004e0235d3da8b072118
workflow-type: tm+mt
source-wordcount: '2275'
ht-degree: 83%

---

# Adobe Analytics 扩展概述

>[!NOTE]
>
>Adobe Experience Platform Launch已經過品牌重塑，現在是Adobe Experience Platform中的一套資料收集技術。 因此，产品文档中的术语有一些改动。有关术语更改的综合参考，请参阅以下[文档](../../../term-updates.md)。

使用本参考可了解有关配置 Adobe Analytics 扩展以及使用此扩展构建规则时可用的选项的信息。

## 配置 Adobe Analytics 扩展

此部分提供有关配置 Adobe Analytics 扩展时可用的选项的参考。

如果尚未安裝Adobe Analytics擴充功能，請開啟您的屬性，然後選取「 」 **[!UICONTROL 擴充功能>目錄]**，將游標暫留在Adobe Analytics擴充功能上，然後選取「 」 **[!UICONTROL 安裝]**.

若要設定擴充功能，請開啟「擴充功能」標籤、將游標暫留在擴充功能上方，然後選取「 」 **[!UICONTROL 設定]**.

![](../../../images/ext-analytics-config.png)

## Library Management

从配置页面的 Library Management 部分中选择一个选项。可以使用以下配置选项：

### Manage the library for me

#### Report Suites

为以下每个环境指定一个或多个报表包：

* 开发
* 暂存
* 生产

### Use the library already installed on the page

#### Set the following report suites on tracker

如果选择此选项，则需为以下每个环境指定一个或多个报表包：

* 开发
* 暂存
* 生产

#### 使用 Activity Map 模块

Activity Map 作为单独的模块（与 AAM 模块类似）加载。默认情况下，Activity Map 处于打开状态，但如果您希望关闭它，可以通过取消选中配置中的复选框将其关闭。

#### Tracker is accessible on the global variable named

选中此框后，可以全局使用跟踪器对象。例如，您可以在网站上的任意位置定义变量 `window.s.pageName`。

### Load the library from a custom URL

#### HTTP URL

指定库所在的 URL。

#### HTTPS URL

指定库所在的 URL。

#### Set the following report suites on tracker

如果选择此选项，则需为以下每个环境指定一个或多个报表包：

* 开发
* 暂存
* 生产

#### Tracker is accessible on the global variable named

指定要全局使用的跟踪器对象。

### Let me provide custom library code

#### Open Editor

可讓您插入核心 [AppMeasurement.js](https://experienceleague.adobe.com/docs/analytics/implementation/js/overview.html) 程式碼。 使用自动配置方法时会自动填充此代码。

>[!NOTE]
>
>標籤程式碼編輯器中使用的驗證器，專門用於識別開發人員所編寫程式碼的問題。 經過縮製程式的程式碼（例如從Code Manager下載的AppMeasurement.js程式碼）可能會遭標籤驗證器誤判而標示為有問題，通常可予以忽略。

#### Set the following report suites on tracker

如果选择此选项，则需为以下每个环境指定一个或多个报表包：

* 开发
* 暂存
* 生产

#### Tracker is accessible on the global variable named

指定要全局使用的跟踪器对象。

## General

从配置页面的 General 部分中选择一个选项。可以使用以下配置选项：

### Enable EU compliance for Adobe Analytics

基于 EU 隐私 Cookie，启用或禁用跟踪。

當您勾選「歐盟法規遵循」核取方塊時， [!UICONTROL 追蹤Cookie名稱] 欄位隨即顯示。 跟踪 Cookie 会覆盖默认的跟踪 Cookie 名称。您可以自訂標籤在追蹤您對於接收其他Cookie的選擇退出狀態時所使用的名稱。

在加载页面时，系统会检查是否设置了名为 sat\_track 的 Cookie（或在 Edit Property 页面中指定的自定义 Cookie 名称）。请考虑以下信息：

* 如果 Cookie 不存在，或者如果 Cookie 存在但设置为 true 之外的其他内容，则启用此设置后将跳过该工具的加载。这表示，使用该工具的规则的任何部分均不适用。如果规则具有启用欧盟合规性的 Analytics 和第三方代码，并且该 Cookie 设置为 false，则第三方代码仍会运行。但是，将不设置 Analytics 变量。
* 如果 Cookie 存在且设置为 true，则会正常加载该工具。

如果访客选择禁用，则由您负责将 sat\_track（或命名的自定义）Cookie 设置为 false。您可以使用以下自定义代码实现此操作：

```javascript
_satellite.cookie.set("sat_track", "false");
```

如果希望访客能够在以后选择启用，则必须具备一个机制将该 Cookie 设置为 true：

```javascript
_satellite.cookie.set("sat_track", "true");
```

### Character Set

确定图像请求的编码方式。如果您的实施或网站使用非 ASCII 字符，请务必在此处定义字符集。您可以选择预设字符集或指定自定义字符集。Adobe 建议使用与您的网站相同的字符编码。通常，此值为 UTF-8。

可以使用变量 `s.charSet` 在 Analytics 自定义代码中设置字符集。有关字符集的更多信息，请参阅 [charSet 文档](https://experienceleague.adobe.com/docs/analytics/implementation/vars/config-vars/charset.html)。

### Currency Code

确定要应用于收入和货币事件的转换率。如果您的网站允许访客以多种货币进行购买，则设置货币代码可确保正确转换和存储货币金额。

有关支持的货币代码的更多信息，请参阅 [currencyCode](https://experienceleague.adobe.com/docs/analytics/implementation/vars/config-vars/currencycode.html?lang=zh-Hans)。

### Tracking Server

用于第一方 Cookie 实施，以指示存储第一方 Cookie 的位置。如果您使用 Experience Cloud ID 服务，Adobe 建议不要填充此字段。

可以使用变量 `s.trackingServer` 在 Analytics 自定义代码中设置跟踪服务器。

请参阅“Adobe Analytics 实施指南”中的 [trackingServer](https://experienceleague.adobe.com/docs/analytics/implementation/vars/config-vars/trackingserver.html)。

### SSL Tracking Server

用于 SSL 第一方 Cookie 实施，以指示存储第一方 Cookie 的位置。如果您使用 Experience Cloud ID 服务，Adobe 建议不要填充此字段。如果未定义，SSL 数据将使用跟踪服务器。

可以使用变量 `s.trackingServerSecure` 在 Analytics 自定义代码中设置 SSL 跟踪服务器。

请参阅 [trackingServerSecure](https://experienceleague.adobe.com/docs/analytics/implementation/vars/config-vars/trackingserversecure.html)。

## Global Variables

可以使用此部分设置 [eVars 和 Props](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/evar.html?lang=zh-Hans)，并创建层级。

全局变量是在页面上初始化 Analytics 跟踪对象时在该对象上设置的变量。在每个页面上创建跟踪对象时，将设置您在此处设置的任何变量。设置这些变量后，它们就如同以任何其他方式设置的任何其他变量一样。具体而言，这意味着规则可以修改、更改或清除这些变量。

如果您的 Web 应用程序通常每页发送一个信标，则此部分可以帮助您在一个位置轻松设置变量。如果您的应用程序每页发送多个信标（例如在单页面应用程序中），并且您需要清除变量并使用相同的跟踪对象重置它们，则依赖规则设置和清除变量会更简单。

## Link Tracking

从配置页面的 Link Tracking 部分中选择一个选项。可以使用以下配置选项：

### Enable ClickMap

[ClickMap](https://experienceleague.adobe.com/docs/analytics/analyze/activity-map/activity-map.html?lang=zh-Hans) 是一个适用于 Internet Explorer 和 Firefox 的插件，而且也是“Reports &amp; Analytics”中的一个模块。

### Track download links

跟踪指向网站上可下载文件的链接。

请参阅 [s.trackDownLoadLinks](https://experienceleague.adobe.com/docs/analytics/implementation/vars/config-vars/trackdownloadlinks.html)。

### Download Extensions

如果启用了 Track Download Links 选项，则可以选择 Downloads Report 中包含的文件链接的扩展名。如果您的网站包含指向具有任何已列出扩展名的文件的链接，则这些链接的 URL 将显示在报表中。

请参阅 [s.linkDownloadFileTypes](https://experienceleague.adobe.com/docs/analytics/implementation/vars/config-vars/linkdownloadfiletypes.html)。

### Track outbound links

确定任何选择的链接是否为退出链接。

请参阅 [s.trackExternalLinks](https://experienceleague.adobe.com/docs/analytics/implementation/vars/config-vars/trackexternallinks.html)。

**单页面应用程序注意事项：**&#x200B;由于某些 SPA 网站的编码方式，指向 SPA 网站上页面的内部链接的外观可能与出站链接类似。

您可以使用以下方法之一跟踪来自 SPA 网站的出站链接：

* 如果不希望跟踪来自 SPA 的任何出站链接，则在 Never Track 部分插入一个条目。例如，`http://testsite.com/spa/\#`。将忽略此主机的所有 \# 链接。并跟踪指向其他主机的所有出站链接，如 [https://www.google.com](https://www.google.com)。
* 如果希望跟踪 SPA 上的某些链接，则使用 Always Track 部分。

例如，如果希望跟踪 spa/\#/about 页面，则可以将“about”放置在 Always Track 部分。

“about”页面是唯一跟踪的出站链接。不会跟踪页面上的任何其他链接（例如 [https://www.google.com](https://www.google.com)）。

>[!NOTE]
>
>这两个选项相互排斥。

### Keep URL Parameters

保留查询字符串。

请参阅 [s.linkLeaveQueryString](https://experienceleague.adobe.com/docs/analytics/implementation/vars/config-vars/linkleavequerystring.html)。

## Cookie

为用于部署 Adobe Analytics 扩展的 Cookie 全局设置配置字段描述。可以使用以下配置选项：

### Visitor ID

唯一值，表示位于在线和离线系统中的客户。

请参阅 [visitorID](https://experienceleague.adobe.com/docs/analytics/implementation/vars/config-vars/visitorid.html?lang=zh-Hans)。

### Visitor Namespace

用于确定设置了 Cookie 的域的变量。

请参阅 [visitorNamespace](https://experienceleague.adobe.com/docs/analytics/implementation/vars/config-vars/visitornamespace.html)。

### Domain Periods

在域中设置了 Analytics Cookie（`s_cc` 和 `s_sq`），以此来确定页面 URL 的域中句点的数量。某些插件还会使用此变量来确定要设置插件 Cookie 的正确域。

请参阅 [s.cookieDomainPeriods](https://experienceleague.adobe.com/docs/analytics/implementation/vars/config-vars/cookiedomainperiods.html)。

### First-Party Domain Periods

`fpCookieDomainPeriods` 变量适用于由 JavaScript 设置的内置第一方 Cookie（`s_sq`、`s_cc`、插件），即使您的实施使用的是第三方 2o7.net 或 omtrdc.net 域也是如此。

请参阅 [s.fpCookieDomainPeriods](https://experienceleague.adobe.com/docs/analytics/implementation/vars/config-vars/fpcookiedomainperiods.html)。

### Cookie Lifetime

确定 Cookie 的生命期限。

请参阅 [s.cookieLifetime](https://experienceleague.adobe.com/docs/analytics/implementation/vars/config-vars/cookielifetime.html?lang=zh-Hans)。

### Secure Cookies

此变量允许 AppMeasurement 编写安全 Cookie。

请参阅 [writeSecureCookies](https://experienceleague.adobe.com/docs/analytics/implementation/vars/config-vars/writesecurecookies.html)


## Customize Page Code

使用编辑器自定义页面代码。

## Adobe Audience Manager

使用扩展配置的此部分指定 Audience Manager 如何与 Analytics 配合使用。

启用 **Automatically share Analytics data with Audience Manager**。

将显示以下选项：

![](../../../images/an-ext-aam.png)

Audience Manager 子域由 Adobe Audience Manager 分配。它有时称为“合作伙伴名称”或“合作伙伴子域”。如果您不知道自己的合作伙伴名称，请联系您的 Adobe 顾问或 Adobe 客户关怀团队。

您可以選取「 」，設定進階設定 **顯示進階設定** 並輸入您的偏好設定。

![](../../../images/an-ext-aam-adv.png)

有关每个设置的信息，请选择信息图标，或参阅 [Adobe Audience Manager 文档](https://experienceleague.adobe.com/docs/audience-manager/user-guide/aam-home.html)。

## Analytics 扩展操作类型

此部分介绍 Analytics 扩展中可用的操作类型。

Analytics 扩展提供了以下操作：

* [设置变量](#set-variables)
* [Send Beacon](#send-beacon)
* [清除变量](#clear-variables)

### 设置变量 {#set-variables}

重要信息：使用“set variables”操作不会发送信标。您必须使用“send beacon”操作才能实现此目的。

#### eVar

设置一个或多个 [eVar](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/evar.html?lang=zh-Hans)。

1. 从下拉菜单中选择一个 eVar。
1. 指定是要将 eVar 设置为值 (Set As) 还是复制 (Duplicate From) 其他 eVar。
1. 提供 Set As 值，或选择要复制的 eVar。
1. （可选）选择 Add eVar 以设置更多 eVar。
1. 选择&#x200B;**[!UICONTROL 保留更改]**。

#### Prop

设置一个或多个 [prop](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/prop.html)。

1. 从下拉菜单中选择一个 prop。
1. 指定是要将 prop 设置为值 (Set As) 还是复制 (Duplicate From) 其他 eVar。
1. 提供 Set As 值，或选择要从中复制 prop 的 eVar。
1. （選用）選取 **[!UICONTROL 新增prop]** 以設定更多prop。
1. 选择&#x200B;**[!UICONTROL 保留更改]**。

#### 事件

设置一个或多个[事件](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/events/events-overview.html)。

1. 从下拉菜单中选择一个事件。
1. （可选）选择或指定用于[事件序列化](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/events/event-serialization.html?lang=zh-Hans)的数据元素。
1. （選用）選取 **[!UICONTROL 新增事件]** 以設定更多事件。
1. 选择&#x200B;**[!UICONTROL 保留更改]**。

#### 层级

设置 Analytics [层级](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/hier.html)变量。

指定层级中的每个级别。

如果需要，请配置其他层级。

#### 頁面名稱

此值是指指定頁面的名稱，並與 [`pageName` 變數](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/pagename.html) （在Analytics中）。

>[!IMPORTANT]
>
>在Adobe Experience Manager實作中，此變數可告知AEM將擷取的Analytics報表儲存於何處。 為確保報表能正確持續儲存，頁面名稱字串必須格式化為以冒號分隔的網站路徑。
>
>例如，位於以下位置的網頁 `content/we-retail/language-masters/en/men.html` 的頁面名稱值應為 `content:we-retail:language-masters:en:men`.

#### Other information

指定页面使用的其他信息。

这些设置包括：

* Page URL
* Server
* Channel
* Referrer
* Campaign
* Purchase ID

   指定值或查询参数

* State
* Zip
* Transaction ID

通过选中“Additional Settings”复选框，可以在“Global Variables”菜单中找到这些设置。

#### Custom Page Code

**Description**

使用编辑器指定自定义页面代码。

**Settings**

1. 選取 **[!UICONTROL 開啟編輯器]**.
1. 键入自定义代码。
1. 选择&#x200B;**[!UICONTROL 保存]**。

### Send Beacon {#send-beacon}

#### Increment a pageview - s.t()

选择是否要递增一次页面查看。

#### 不要遞增頁面檢視 — s.tl()

选择是否不要递增一次页面查看。

**Settings**

1. 选择链接类型。

   您可以选择以下选项之一：

   * Custom Link
   * Download Link
   * Exit Link

1. 为选定的链接设置参数。
   * Custom Link：指定链接名称。
   * Download Link：指定文件名。
   * Exit Link：指定目标 URL。
1. 选择&#x200B;**[!UICONTROL 保留更改]**。

### 清除变量 {#clear-variables}

如果选择 Clear Variables 操作类型，则没有配置选项。
