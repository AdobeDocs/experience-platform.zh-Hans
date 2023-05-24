---
title: Adobe Target擴充功能發行說明
description: Adobe Experience Platform中Adobe Target標籤擴充功能的最新發行說明。
exl-id: ba29f614-c3cd-4e0b-b043-2b1c17567def
source-git-commit: 88939d674c0002590939004e0235d3da8b072118
workflow-type: tm+mt
source-wordcount: '520'
ht-degree: 74%

---

# Adobe Target 发行说明

>[!NOTE]
>
>Adobe Experience Platform Launch已經過品牌重塑，現在是Adobe Experience Platform中的一套資料收集技術。 因此，产品文档中的术语有一些改动。有关术语更改的综合参考，请参阅以下[文档](../../../term-updates.md)。

## 2021 年 9 月 16 日

### Adobe Target 扩展 0.11.4

* 更新至at.js v1.8.3
* 已新增 `SameSite=None` 和 `Secure` 設定Cookie時的屬性

## 2020 年 7 月 24 日

### Adobe Target 扩展 0.11.3

* 修复了脚本或代码将 `default` 属性添加到 `window` 或 `document` 时扩展失败的错误

## 2020 年 6 月 15 日

### Adobe Target 扩展 0.11.2

* 修复了以下问题：使用 CNAME 和 Edge 覆盖时，at.js 1.x 可能会错误地创建服务器域，从而导致 Target 请求失败

## 2020 年 3 月 25 日

### Adobe Target 扩展 0.11.1

* 已将 at.js 更新至 v1.8.1
* 修复了参数和页面加载参数无法正确处理的问题

## 2019 年 10 月 10 日

### Adobe Target 扩展 0.11.0

* 已将 at.js 更新至 v1.8。
* 改进了 Experience Cloud ID 库 (ECID) v4.4 和 at.js 1.8 之间集成的性能。
* 以前，ECID 库要发出两次阻止调用，at.js 才能获取体验。现已减少为一次调用，显著提高了性能。

>[!NOTE]
>請將Adobe Experience Platform的ECID標籤擴充功能升級至v4.4.1，以運用此效能增強功能。

## 2019 年 7 月 31 日

### Adobe Target 扩展 0.10.1

* 處理Adobe Target標籤擴充功能的引數Hotfix

## 2019 年 5 月 4 日

### Adobe Target 扩展 0.10.0

* 修复了由最新的 Google Chrome 更改所导致的数据元素问题

## 2019 年 3 月 14 日

### Adobe Target 扩展 0.9.3

* 更新了扩展版本以使用 at.js 1.7.1

## 2019 年 2 月 20 日

### Adobe Target 扩展 0.9.2

* 修复了 Target 与 Analytics 扩展之间的争用情况

## 2019 年 2 月 12 日

### Adobe Target 扩展 0.9.1

#### **功能**

* 更新擴充功能，以使用透過標籤支援選擇加入隱私權功能的at.js 1.7.0，進而控制Target標籤的引發方式和時機。 請查閱標籤檔案，瞭解如何設定您的選擇加入實施作法。 添加了用于自定义是否应将具有空值的 mbox 参数发送到 Target 的功能。

## 2019 年 1 月 23 日

### Adobe Target 扩展 0.8.4

* 已将 at.js 更新到版本 1.6.4
* 已将扩展用户界面迁移到 Adobe Spectrum

## 2018 年 11 月 15 日

### Adobe Target 扩展 0.8.2

* 已将 at.js 更新到版本 1.6.3

## 2018 年 10 月 24 日

### Adobe Target 扩展 0.8.1

* 已将 at.js 更新到版本 1.6.2

## 2018 年 8 月 23 日

### Adobe Target 扩展 0.8.0

* 已将 at.js 更新到版本 1.6.0

## 2018 年 8 月 10 日

### Adobe Target 扩展 0.7.2

* 次要更改
* 更新了 `extension.json` 文件中的 `exchangeUrl` 属性

## 2018 年 8 月 1 日

### Adobe Target 扩展 0.7.1

* 次要修复

## 2018 年 6 月 18 日

### Adobe Target 扩展 0.7.0

* 已将 at.js 版本更新到 1.5.0
* 修复了 Media Optimizer 在 IE 11 中抛出空引用错误的问题

## 2018 年 6 月 15 日

### Adobe Target 扩展 0.6.0

#### **功能**

* 更新了 Target 扩展以使用 at.js v1.3.1。现在，将 Target 与 Analytics 一起部署时，我们会先等到所有 Target 调用均已解析（包括重定向选件），然后再触发 Analytics，从而解决之前存在的争用情况。

## 2018 年 2 月 22 日

### Adobe Target 扩展 0.4.1

#### **功能**

* 已将 Adobe Exchange 列表添加到 extension.json
* 添加了用于检查 Target 是否已禁用以及“创作”是否已启用的功能

#### **错误修复**

* 修正Adobe Target擴充功能中，視覺化體驗撰寫器在透過標籤部署時無法取消隱藏頁面的錯誤。

## 2018 年 2 月 8 日

### Adobe Target 扩展 0.4.0

#### **功能**

* 更新了扩展配置屏幕中的视图
* 已将 at.js 更新到版本 1.2.3（添加了对 JSON 选件的支持）
