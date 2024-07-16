---
title: “常用Analytics插件”扩展的发行说明
description: Adobe Experience Platform中的“常用Analytics插件”标记扩展的最新发行说明。
exl-id: 5ea4b709-4e21-4f5d-be99-e72e4889ed99
source-git-commit: 88939d674c0002590939004e0235d3da8b072118
workflow-type: tm+mt
source-wordcount: '352'
ht-degree: 55%

---

# 常用Analytics插件发行说明

## 2022年6月3日

### “常用 Analytics 插件”扩展 3.0.7

#### 功能

* 设置Cookie的插件现在使用secure标记

## 2021年6月23日

### “常用 Analytics 插件”扩展 3.0.6

#### 错误修复

* 修复了使用特殊字符时getPercentPageViewed中断的问题

## 2021 年 5 月 20 日

### “常用 Analytics 插件”扩展 3.0.5

#### 错误修复

* 修复了在使用通用初始化操作时getTimeParting无法正确初始化的问题

## 2021年3月26日

### “常用 Analytics 插件”扩展 3.0.4

#### 错误修复

* 修复了getPageLoadTime在窗口对象上错误设置变量的问题
* 修复了以下问题：如果查询字符串中不存在queryParam，则getQueryParam返回undefined而非“”
* 修复了在初始化操作中显示错误版本号的问题

## 2021 年 3 月 19 日

### “常用 Analytics 插件”扩展 3.0.2

#### 功能

* 更新了所有插件，以自动包含版本信息作为上下文数据
* 添加了getPercentPageViewed插件
* 为以下插件添加了数据元素
   * getGeoCoordinates
   * getNewRepeat
   * getPageName
   * getResponsiveLayout
   * getTimeParting
   * getTimeSinceLastVisit
   * getVisitDuration
   * getVisitNum
* 已更新样式

## 2020 年 4 月 9 日

### “常用 Analytics 插件”扩展 2.2.0

#### 错误修复

* 修正了扩展视图中的措辞

#### 功能

* 更新了初始化操作中的文档

## 2019年12月5日

### “常用 Analytics 插件”扩展 2.1.1

#### 错误修复

* 修复了妨碍向后兼容版本 2.0.X 的问题
* 修复了文档链接指向错误文档的问题
* 修复了初始化操作中 `getTimeSinceLastVisit` 显示两次的问题

## 2019 年 11 月 15 日

### “常用 Analytics 插件”扩展 2.1.0

#### 错误修复

* 为支持向后兼容性，重新引入了各个插件操作
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

* 扩展发布，其中七个插件
* 可用于分别初始化每个插件的单个操作
