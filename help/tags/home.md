---
title: 标记概述
description: Adobe Experience Platform 中的标记是 Adobe 推出的新一代标记管理功能。标记为客户提供了一种简单的方式，让客户可以部署和管理所有用来加强相关客户体验的分析、营销和广告标记。
exl-id: 23d882a5-1ddd-404b-a7e9-3000f1804971
source-git-commit: 13c02dd5930905e3851ff147c0ea4d914e3dc6c7
workflow-type: tm+mt
source-wordcount: '585'
ht-degree: 75%

---

# 标记概述

>[!NOTE]
>
>事件轉送是一項付費功能，屬於Adobe Real-time Customer Data Platform Connections、Prime或Ultimate方案的一部分。

>[!NOTE]
>
>Adobe Experience Platform Launch已經過品牌重塑，現在是Adobe Experience Platform中的一套資料收集技術。 因此，产品文档中的术语有一些改动。有关术语更改的综合参考，请参阅以下[文档](./term-updates.md)。

Adobe Experience Platform 中的标记是 Adobe 推出的新一代标记管理功能。标记为客户提供了一种简单的方式，让客户可以部署和管理所有用来加强相关客户体验的分析、营销和广告标记。

標籤可讓任何人建置和維護自己的整合，稱為 *擴充功能*. [!DNL Adobe Experience Cloud] 客户可在应用商店中获取这些扩展，从而可以快速安装、配置和部署自己的标记。

標籤提供給 [!DNL Adobe Experience Cloud] 內含增值功能的客戶。

## 主要优点 {#key-benefits}

* 更快的价值实现。
* 使用数据元素以集中方式收集、组织和提交值得信赖的数据。
* 通过使用规则生成器将数据和营销技术集成在一起，交付令人兴奋的体验。

## 主要功能 {#key-features}

### 扩展 {#extensions}

扩展是一种用于扩展标记功能的代码包（JavaScript、HTML 和 CSS）。使用几乎自助的界面构建、管理和更新您的集成。您可以將擴充功能視為用來完成工作的應用程式。

### 扩展目录 {#extension-catalog}

浏览、配置和部署由独立软件供应商构建和维护的营销/广告工具。

### 规则生成器 {#rule-builder}

创建强大的规则以用来合并多个事件，其排列顺序由您在条件和例外中使用的 if/then 逻辑来确定。规则提供以下相关选项：

* 事件
* 条件
* 例外
* 操作

规则生成器包括对自定义代码的实时错误检查和语法突出显示。

当满足规则中所列的标准并符合条件时，您定义的操作将按顺序执行。

### 数据元素 {#data-elements}

通过基于 Web 的营销和广告技术，收集、组织和提交数据。

### 企业发布 {#enterprise-publishing}

发布过程使团队能够将代码发布到页面。不同的人員可以建立實施、核准實施，然後發佈到您的頁面上。

* 程式碼變更會封裝在您定義的程式庫中。
* 您可指定希望部署代码的位置和时间。
* 不同的团队可同时构建多个库。
* 无限制的开发环境。
* 將程式庫合併在一起的程式是審慎的、以許可權為基礎的程式。

### 开放式 API {#open-apis}

將個別技術或一組技術的實作作業自動化。

* 標籤會與Reactor API互動。
* 部署可通过 API 自动进行。
* 将  API 与您自己的内部系统集成。
* 如有需要，您可以建置專屬的使用者介面。

### 轻便的模块化容器标记 {#modular-tag}

您的容器的内容将被缩小，包括您的自定义代码。一切都是模块化的。如果您不需要某个项目，它不会包含在您的库中。这样，实施就会变得快速而紧凑。请参阅[缩小](./ui/publishing/builds.md)。

## 其他亮点 {#other-highlights}

標籤在類似系統上提供數項改善功能，包括：

* 在 Chrome 不允许的情况下，不使用 `document.write ()`。
* Page Top 和 Page Bottom 规则捆绑在主库中，可最大程度地减少不必要的 HTTP 调用。
* 规则内的自定义操作脚本可并行加载，但会按顺序执行。
* 如果您避开 Page Top 和 Page Bottom 规则，则代码大部分是异步的，并最终会变得完全异步。
