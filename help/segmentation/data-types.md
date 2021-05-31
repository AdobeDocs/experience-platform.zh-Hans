---
keywords: Experience Platform；主页；热门主题；数据类型；数据类型；数据类型；分段数据类型；分段；分段服务；分段服务数据类型；
solution: Experience Platform
title: Segmentation Service中支持的数据类型
topic-legacy: overview
description: Adobe分段服务支持所有体验数据模型(XDM)数据类型。 构成区段定义的规则通过以下数据类型进行了上下文相关化。
exl-id: 73f932a7-f864-4566-ade7-c148a12dc83c
source-git-commit: c3d66e50f647c2203fcdd5ad36ad86ed223733e3
workflow-type: tm+mt
source-wordcount: '510'
ht-degree: 1%

---

# Segmentation Service中支持的数据类型

Adobe Experience Platform Segmentation Service支持所有体验数据模型(XDM)数据类型。 构成区段定义的规则通过以下数据类型进行了上下文相关化。

## 字符串数据

区段定义使用字符串数据为区段受众定义非数值约束，如“国家/地区名称”或“忠诚度计划级别”。

使用逻辑、包含/排除和比较语句将字符串数据包含在区段定义中。 在将字符串属性添加到区段定义后，您可以使用字符串相关语句根据其他字符串字段对其进行评估。

| 语句类型 | 示例 |
| -------------- | -------- |
| 逻辑 | `and`、`or`、`not` |
| 包容/排斥 | `include`,  `must` `exist`,  `exclude`  `must not exist` |
| 比较 | `equals`、`does not equal`、`contains`、`starts with` |

## 日期数据

日期数据允许您通过使用特定的开始/结束日期或使用与日期相关的语句（如下表所示），将基于时间的上下文分配给区段定义。 其中一个实施可能是创建一个受众，该受众在&#x200B;*今年*&#x200B;任何时间与您的品牌进行交互，并且在最近几天&#x200B;*内一直处于活动状态*。

| 示例字段 | 与日期相关的报表 | 时间轴 |
| ------------- | ------------------------ | --------- |
| person.firstPurchase | `today`、`yesterday`、`this month`、`this year` | 与区段构建日期相关。 |
| person.lastPurchase | `in last`、`during`、`before`、`after`、`within` | 在任何给定周/月内相关。 |

## 体验事件

作为Adobe Experience Platform架构，[!DNL XDM ExperienceEvents]记录客户与集成了[!DNL Platform]的应用程序的显式和隐式交互，包括交互发生时系统的快照。 [!DNL ExperienceEvents] 是事实记录。因此，它们是区段定义期间可供您使用的数据源。

如下表所示，事件数据使用有助于优化事件行为和指定事件属性的关键词进行呈现。

| 关键词 | 使用 |
| ------- | --- |
| 包含/排除 | 通过包含或遗漏数据描述事件的行为。 |
| 任意/全部 | 帮助确定符合条件的区段的数量。 |
| “应用时间规则”切换按钮 | 合并日期数据。 |
| 等于、不等于、开始于、不开始于、结束于、不结束于、包含、不包含、存在、不存在 | 合并字符串数据。 |

### 受众共享

外部受众还可以用作新区段定义的组件，从而将其属性规则添加到新区段。

目前，仅Adobe Audience Manager作为外部受众受支持，并且将来会启用其他源。 有关在Platform中使用Adobe Audience Manager受众的更多信息，请参阅Adobe Audience Manager文档](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html)中的[受众共享指南。

### 区段共享

在Platform中创建的区段可以在其他[Adobe Experience Cloud核心服务](https://experienceleague.adobe.com/docs/core-services/interface/experience-cloud.html)中使用。 要启用此功能，您需要联系解决方案架构师或顾问。

## 其他数据类型

除了上述数据类型之外，支持的数据类型列表还包括：

- 统一资源标识符(URI)
- 枚举
- 数值
- 长
- 整数
- 短
- 字节
- 布尔值
- 数组
- 对象
- 地图
