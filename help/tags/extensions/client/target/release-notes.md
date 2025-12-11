---
title: Adobe Target扩展的发行说明
description: Adobe Experience Platform中的Adobe Target标记扩展的最新发行说明。
exl-id: ba29f614-c3cd-4e0b-b043-2b1c17567def
source-git-commit: 44e2b8241a8c348d155df3061d398c4fa43adcea
workflow-type: tm+mt
source-wordcount: '533'
ht-degree: 76%

---

# Adobe Target发行说明

## 2021 年 9 月 16 日

### Adobe Target 扩展 0.11.4

* 已更新至at.js v1.8.3
* 在设置Cookie时添加了`SameSite=None`和`Secure`属性

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
>请将您的ECID标记扩展升级到Adobe Experience Platform v4.4.1以实现此性能提升。

## 2019 年 7 月 31 日

### Adobe Target 扩展 0.10.1

* 用于处理Adobe Target标记扩展的参数的修补程序

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

* 更新了扩展以使用通过标记支持选择加入隐私功能的at.js 1.7.0，进而控制Target标记的触发方式和时间。 请查看标记文档，了解如何设置选择加入实施。 添加了用于自定义是否应将具有空值的 mbox 参数发送到 Target 的功能。

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

* 更新了 Target 扩展以使用 at.js v1.3.1。现在，将 Target 与 Analytics 一起部署时，我们会先等到所有 Target 调用均已解析（包括重定向产品建议），然后再触发 Analytics，从而解决之前存在的争用情况。

## 2018 年 2 月 22 日

### Adobe Target 扩展 0.4.1

#### **功能**

* 已将 Adobe Exchange 列表添加到 extension.json
* 添加了用于检查 Target 是否已禁用以及“创作”是否已启用的功能

#### **错误修复**

* 修复了Adobe Target扩展中的一个错误，该错误会导致通过标记部署该扩展后，可视化体验编辑器无法取消隐藏页面。

## 2018 年 2 月 8 日

### Adobe Target 扩展 0.4.0

#### **功能**

* 更新了扩展配置屏幕中的视图
* 已将 at.js 更新到版本 1.2.3（添加了对 JSON 产品建议的支持）
