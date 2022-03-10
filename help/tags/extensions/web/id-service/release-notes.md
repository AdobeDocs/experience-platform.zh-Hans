---
title: Adobe Experience Cloud Identity Service扩展的发行说明
description: Adobe Experience Platform中Adobe Experience Cloud Identity Service标记扩展的最新发行说明。
exl-id: f9bfbed7-1eec-4916-9235-a75b5e2efcf8
source-git-commit: 04dfe55fec06d08a0caef7aee5bf8d85c6056149
workflow-type: tm+mt
source-wordcount: '614'
ht-degree: 68%

---

# Adobe Experience Cloud Identity Service扩展发行说明

>[!NOTE]
>
>Adobe Experience Platform Launch已在Adobe Experience Platform中重新命名为一套数据收集技术。 因此，产品文档中的术语有一些改动。有关术语更改的综合参考，请参阅以下[文档](../../../term-updates.md)。

有关Experience CloudIdentity Service本身，而不只是Adobe Experience Platform标记扩展的发行说明，请参阅： [https://experienceleague.adobe.com/docs/id-service/using/release-notes/release-notes.html](https://experienceleague.adobe.com/docs/id-service/using/release-notes/release-notes.html)

## 2022年3月9日

### Experience Cloud ID 扩展 5.4.0

#### **功能**

* 此版本包含最新的访客5.4.0，该版本具有以下更新：

   * 能够配置 `s_ecid` cookie（使用cookieLifetime配置）
   * 在子iFrame中加载页面时发生的Firefox浏览器问题的更新

## 2021年10月10日

### Experience Cloud ID 扩展 5.3.1

#### **功能**

* 此版本包含最新的访客5.3.0，该版本具有以下新更新：

   * 更新了生成本地ECID的算法
   * 最新选择加入功能 `Secure` 和 `SameSite` 隐私cookie标记
   * 修复了在子iFrame中加载页面时出现的Firefox浏览器问题

## 2021 年 1 月 12 日

### Experience Cloud ID 扩展 5.2.0

#### **功能**

* 在收到同意后，无法更新到VisitorJS 5.2.0修补程序（该修补程序修复了ECID DataElement）。

## 2020 年 11 月 3 日

### Experience Cloud ID 扩展 5.2.1

#### **功能**

* 该修补程序修复了在 Google Chrome 浏览器中，从带有 `SameSite=None` 属性的 iFrame 写入 Cookie 的问题。

## 2020 年 10 月 27 日

### Experience Cloud ID 扩展 5.1.0

#### **功能**

* 添加 `sameSiteCookie` 配置，以指定 `AMCV` Cookie 的 `SameSite` 属性。此配置支持 `SameSite` 属性的以下值：

   * `Strict`
   * `Lax`
   * `None`

有关这些属性值的详细信息，可访问 [web.dev](https://web.dev/samesite-cookies-explained/) 和 [chromium](https://www.chromium.org/updates/same-site)


## 2020 年 8 月 13 日

### Experience Cloud ID 扩展 5.0.1

#### **功能**

* 将更新到 VisitorJS 5.0.1 修补程序，该修补程序修复了在 IAB 同意字符串发生更改时添加 d_cf 标记的问题。

## 2020 年 6 月 15 日

### Experience Cloud ID 扩展 5.0.0

#### **功能**

* 添加对 `IAB TCF`（透明度和同意框架）`Version 2.0` 的支持。

## 2020 年 4 月 13 日

### Experience Cloud ID 扩展 4.6.0

#### **功能**

* 默认情况下将 `loadSSL` 标记设为开启。所有对 Identity 服务的调用都将默认开启 `https`。如果客户希望在 http 上从其非 ssl 页面调用 Identity 服务，则客户可以将其设置为 false。
* 更新了用于检测 Internet-Explorer (IE) 版本的功能，以修复由 ESLint 报告的问题。
* 修复了一个错误：当为 ECID 提供 optIn 批准并稍后更新时，Internet-Explorer (IE) 11 上出现性能问题。

## 2020 年 1 月 22 日

### Experience Cloud ID 扩展 4.5.2

#### **功能**

* 已将 visitor.js 更新到 4.5.2
* 访客 4.5.1 包含针对适用于 Optin 的 IAB 插件的错误修复
* 更新了 `setCustomerIDs` 方法以拒绝发送的任何空 ID。

## 2020 年 1 月 7 日

### Experience Cloud ID 扩展 4.4.2

#### **功能**

* 已将 visitor.js 更新到 4.4.2
* 改进了 `getVisitorValues` 方法以更快地获取值


## 2019 年 9 月 19 日

### Experience Cloud ID 扩展 4.4.1

#### **功能**

* 已将 visitor.js 更新到 4.4.1
* 修复了获取选择启用预批准输入的错误
* 在 preOptInApprovals 中将 VIDEO_ANALYTICS 重命名为 MEDIA_ANALYTICS

   ![](../../../images/ecid-media-analytics.png)

## 2019 年 7 月 17 日

### Experience Cloud ID 扩展 4.4.0

#### **功能**

* 已将 visitor.js 更新到 4.4.0
* 添加了对 setCustomerIDs 的 SHA256 哈希支持

   ![](../../../images/ecid-setCustomerIDs-hash.png)

## 2019 年 5 月 13 日

### Experience Cloud ID 扩展 4.3.1

#### **功能**

* 已将 visitor.js 更新到 4.3
* 在标记扩展中添加了ECID的数据元素类型

   ![](../../../images/ecid-data-element.png)

## 2019 年 4 月 9 日

### Experience Cloud ID 扩展 4.2.0

#### **功能**

* 已将 visitor.js 更新到 4.2，其中包含对 Audience Manager IAB TCF 插件的支持

## 2019 年 2 月 25 日

### Experience Cloud ID 扩展 4.1.0

#### **功能**

* 已将 visitor.js 更新为 4.1，新版本根据新的 API 变化更新了 publishDestinations。通过此更新，可以根据需要在 ID 同步期间公开此页面的反向链接信息。

## 2019 年 2 月 15 日

### Experience Cloud ID 扩展 4.0.0

#### **功能**

* 已将 visitor.js 更新到 4.0
* 为新的“选择启用”内置对象添加了配置选项。“选择启用”设置可用于阻止 Adobe 解决方案的 Cookie 和信标调用，从而更好地支持 GDPR 等法规

   ![](../../../images/ext-mcid-opt-in.png)

## 2018 年 3 月 20 日

### Experience Cloud ID 扩展 3.1.0

#### **功能**

* 已将 visitor.js 更新到 3.1
* 添加了两个配置属性：`resetBeforeVersion` 和 `serverState`
