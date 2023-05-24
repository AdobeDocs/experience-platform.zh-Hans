---
title: 常見Analytics外掛程式擴充功能的發行說明
description: Adobe Experience Platform中常見Analytics外掛程式標籤擴充功能的最新發行說明。
exl-id: 5ea4b709-4e21-4f5d-be99-e72e4889ed99
source-git-commit: 88939d674c0002590939004e0235d3da8b072118
workflow-type: tm+mt
source-wordcount: '329'
ht-degree: 55%

---

# 常見Analytics外掛程式發行說明

## 2022 年 6 月 03 日

### “常用 Analytics 插件”扩展 3.0.7

#### 功能

* 設定Cookie的外掛程式現在會使用安全標幟

## 2021年6月23日

### “常用 Analytics 插件”扩展 3.0.6

#### 错误修复

* 修正使用特殊字元時getPercentPageViewed中斷的問題

## 2021 年 5 月 20 日

### “常用 Analytics 插件”扩展 3.0.5

#### 错误修复

* 修正使用一般初始化動作時，getTimeParting無法正確初始化的問題

## 2021年3月26日

### “常用 Analytics 插件”扩展 3.0.4

#### 错误修复

* 修正getPageLoadTime在視窗物件上設定變數時發生錯誤
* 修正當queryParam不存在於查詢字串中時，getQueryParam傳回undefined而非「」的問題
* 修正初始化動作中顯示錯誤版本號碼的問題

## 2021 年 3 月 19 日

### “常用 Analytics 插件”扩展 3.0.2

#### 功能

* 所有外掛程式都已更新，自動包含版本資訊作為內容資料
* 新增getPercentPageViewed外掛程式
* 為下列外掛程式新增資料元素
   * getGeoCoordinates
   * getNewRepeat
   * getPageName
   * getResponsiveLayout
   * getTimeParting
   * getTimeSinceLastVisit
   * getVisitDuration
   * getVisitNum
* 已更新樣式

## 2020 年 4 月 9 日

### “常用 Analytics 插件”扩展 2.2.0

#### 错误修复

* 修正了扩展视图中的措辞

#### 功能

* 更新了初始化操作中的文档

## 2019年12月5

### “常用 Analytics 插件”扩展 2.1.1

#### 错误修复

* 修复了妨碍向后兼容版本 2.0.X 的问题
* 修复了文档链接指向错误文档的问题
* 修复了初始化操作中 `getTimeSinceLastVisit` 显示两次的问题

## 2019 年 11 月 15 日

### “常用 Analytics 插件”扩展 2.1.0

#### 错误修复

* 重新推出個別外掛程式動作，以支援回溯相容性
* 修复了 `cleanStr` 插件的问题
* 修复了 `getResponsiveLayout` 插件的问题
* 修复了 `getPageName` 插件的问题

#### 功能

* 更新了 `getTimeParting` 的版本
* 更新了 `numberSuite` 的版本
* 更新了 `getNewRepeat` 的版本
* 更新了所有插件的文档

## 2019 年 10 月 30 日

### “常用 Analytics 插件”扩展 2.0.3

#### 错误修复

* 修复了文档链接断开的问题

## 2019 年 10 月 11 日

### “常用 Analytics 插件”扩展 2.0.2

#### 功能

* 为扩展添加了 15 个插件
* 创建了新的初始化操作以支持更轻松的实施

## 2019 年 7 月 11 日

### “常用 Analytics 插件”扩展 1.0.4

#### 功能

* 擴充功能隨7個外掛程式發行
* 可用于分别初始化每个插件的单个操作
