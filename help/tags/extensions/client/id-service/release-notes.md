---
title: Adobe Experience Cloud Identity Service扩展的发行说明
description: Adobe Experience Platform中的Adobe Experience Cloud Identity服务标签扩展的最新发行说明。
exl-id: f9bfbed7-1eec-4916-9235-a75b5e2efcf8
source-git-commit: 88939d674c0002590939004e0235d3da8b072118
workflow-type: tm+mt
source-wordcount: '688'
ht-degree: 62%

---

# Adobe Experience Cloud Identity Service扩展发行说明

>[!NOTE]
>
>Adobe Experience Platform Launch已更名为Adobe Experience Platform中的一套数据收集技术。 因此，产品文档中的术语有一些改动。 有关术语更改的综合参考，请参阅以下[文档](../../../term-updates.md)。

本文档介绍Adobe Experience Cloud Identity服务标签扩展的发行说明。 有关Experience CloudIdentity服务本身的发行说明，请参阅[Identity服务文档](https://experienceleague.adobe.com/docs/id-service/using/release-notes/release-notes.html?lang=zh-Hans)。

## 2022 年 10 月 17 日

### Experience Cloud ID 扩展 5.5.0

* 该扩展现在支持[访客JS客户端](https://github.com/Adobe-Marketing-Cloud/id-service)的5.5.0版本。 有关具体更新，请参阅[访客发行说明](https://github.com/Adobe-Marketing-Cloud/id-service/releases/tag/5.5.0)。

## 2022年3月9日

### Experience Cloud ID 扩展 5.4.0

* 此版本包含最新的访客5.4.0，该版本具有以下更新：

   * 能够使用cookieLifetime配置配置`s_ecid` Cookie的生命周期
   * 更新在子iFrame中加载页面时发生的Firefox浏览器问题

## 2021 年 10 月 10 日

### Experience Cloud ID 扩展 5.3.1

* 此版本包含最新的访客5.3.0，该版本具有以下新更新：

   * 更新了生成本地ECID的算法
   * 隐私Cookie的最新选择加入带有`Secure`和`SameSite`标记
   * 修复了将页面加载到子iFrame中时的Firefox浏览器问题

## 2021年1月12日

### Experience Cloud ID 扩展 5.2.0

* 在收到同意时，无法将更新到VisitorJS 5.2.0修补程序并修复了ECID DataElement。

## 2020 年 11 月 3 日

### Experience Cloud ID 扩展 5.2.1

* 该修补程序修复了在 Google Chrome 浏览器中，从带有 `SameSite=None` 属性的 iFrame 写入 Cookie 的问题。

## 2020 年 10 月 27 日

### Experience Cloud ID 扩展 5.1.0

* 添加 `sameSiteCookie` 配置，以指定 `AMCV` Cookie 的 `SameSite` 属性。此配置支持 `SameSite` 属性的以下值：

   * `Strict`
   * `Lax`
   * `None`

有关这些属性值的详细信息，可访问 [web.dev](https://web.dev/samesite-cookies-explained/) 和 [chromium](https://www.chromium.org/updates/same-site)


## 2020 年 8 月 13 日

### Experience Cloud ID 扩展 5.0.1

* 将更新到 VisitorJS 5.0.1 修补程序，该修补程序修复了在 IAB 同意字符串发生更改时添加 d_cf 标记的问题。

## 2020 年 6 月 15 日

### Experience Cloud ID 扩展 5.0.0

* 添加对 `IAB TCF`（透明度和同意框架）`Version 2.0` 的支持。

## 2020 年 4 月 13 日

### Experience Cloud ID 扩展 4.6.0

* 默认情况下将 `loadSSL` 标记设为开启。所有对 Identity 服务的调用都将默认开启 `https`。如果客户希望在 http 上从其非 ssl 页面调用 Identity 服务，则客户可以将其设置为 false。
* 更新了用于检测 Internet-Explorer (IE) 版本的功能，以修复由 ESLint 报告的问题。
* 修复了一个错误：当为 ECID 提供 optIn 批准并稍后更新时，Internet-Explorer (IE) 11 上出现性能问题。

## 2020 年 1 月 22 日

### Experience Cloud ID 扩展 4.5.2

* 已将 visitor.js 更新到 4.5.2
* 访客 4.5.1 包含针对适用于 Optin 的 IAB 插件的错误修复
* 更新了 `setCustomerIDs` 方法以拒绝发送的任何空 ID。

## 2020 年 1 月 7 日

### Experience Cloud ID 扩展 4.4.2

* 已将 visitor.js 更新到 4.4.2
* 改进了 `getVisitorValues` 方法以更快地获取值


## 2019 年 9 月 19 日

### Experience Cloud ID 扩展 4.4.1

* 已将 visitor.js 更新到 4.4.1
* 修复了获取选择启用预批准输入的错误
* 在 preOptInApprovals 中将 VIDEO_ANALYTICS 重命名为 MEDIA_ANALYTICS

  ![](../../../images/ecid-media-analytics.png)

## 2019 年 7 月 17 日

### Experience Cloud ID 扩展 4.4.0

* 已将 visitor.js 更新到 4.4.0
* 添加了对 setCustomerIDs 的 SHA256 哈希支持

  ![](../../../images/ecid-setCustomerIDs-hash.png)

## 2019 年 5 月 13 日

### Experience Cloud ID 扩展 4.3.1

* 已将 visitor.js 更新到 4.3
* 在标记扩展中添加了ECID的数据元素类型

  ![](../../../images/ecid-data-element.png)

## 2019 年 4 月 9 日

### Experience Cloud ID 扩展 4.2.0

* 已将 visitor.js 更新到 4.2，其中包含对 Audience Manager IAB TCF 插件的支持

## 2019 年 2 月 25 日

### Experience Cloud ID 扩展 4.1.0

* 已将 visitor.js 更新为 4.1，新版本根据新的 API 变化更新了 publishDestinations。通过此更新，可以根据需要在 ID 同步期间公开此页面的反向链接信息。

## 2019 年 2 月 15 日

### Experience Cloud ID 扩展 4.0.0

* 已将 visitor.js 更新到 4.0
* 为新的“选择启用”内置对象添加了配置选项。“选择启用”设置可用于阻止 Adobe 解决方案的 Cookie 和信标调用，从而更好地支持 GDPR 等法规

  ![](../../../images/ext-mcid-opt-in.png)

## 2018 年 3 月 20 日

### Experience Cloud ID 扩展 3.1.0

* 已将 visitor.js 更新到 3.1
* 添加了两个配置属性：`resetBeforeVersion` 和 `serverState`
