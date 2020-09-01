---
keywords: Experience Platform;home;popular topics;data type;data types;Data types;Data type;Segmentation data types;Segmentation;segmentation;Segmentation Service;Segmentation service data types;
solution: Experience Platform
title: Adobe Experience Platform分段服务数据类型
topic: overview
description: 分段服务支持所有XDM数据类型。 构成区段定义的规则根据以下数据类型进行情境化。
translation-type: tm+mt
source-git-commit: 17ef6c1c6ce58db2b65f1769edf719b98d260fc6
workflow-type: tm+mt
source-wordcount: '479'
ht-degree: 3%

---


# Adobe Experience Platform [!DNL Segmentation Service] 支持的数据类型

中支持所有XDM数据类型 [!DNL Segmentation Service]。 构成区段定义的规则根据以下数据类型进行情境化。

## 字符串数据

区段定义使用字符串数据为区段受众定义非数值约束，如“国家／地区名称”或“忠诚度项目级别”。

字符串数据使用逻辑、包含／独占和比较语句包括在段定义中。 在将字符串属性添加到区段定义后，您可以使用字符串相关语句根据其他字符串字段对其进行评估。

| 语句类型 | 示例 |
| -------------- | -------- |
| 逻辑 | `and`, `or`, `not` |
| 包含／排斥 | `include`, `must` `exist`, `exclude`, `must not exist` |
| 比较 | `equals`、`does not equal`、`contains`、`starts with` |

## 日期数据

日期数据允许您通过使用特定开始/结束日期或使用下表所示的与日期相关的语句，将基于时间的上下文分配给您的区段定义。 一种实施方式可能是创建与您的品牌在今年任何时候互动 *的受众* ，并且在过 *去几天内* 也很活跃。

| 示例字段 | 与日期相关的声明 | 时间轴 |
| ------------- | ------------------------ | --------- |
| person.firstPurchase | `today`、`yesterday`、`this month`、`this year` | 与区段构建日期相关。 |
| person.lastPurchase | `in last`、`during`、`before`、`after`、`within` | 在任何给定周／月内相关。 |

## 体验事件

作为Adobe Experience Platform的 [!DNL XDM ExperienceEvents] 模式，记录与集成应用程序的显 [!DNL Platform]式和隐式客户交互，包括交互发生时系统的快照。 [!DNL ExperienceEvents] 是事实记录。 因此，在段定义过程中，它们是可供您使用的数据源。

如下表所示，事件数据使用关键字呈现，这些关键字有助于优化事件行为和指定事件属性。

| 关键字 | 使用 |
| ------- | --- |
| 包含／排除 | 通过包含或遗漏数据描述事件的行为。 |
| 任意／全部 | 帮助确定符合条件的细分数。 |
| “应用时间规则”切换按钮 | 整合日期数据。 |
| 等于、不等于、开始与、不开始与、结尾与、不结尾与、包含、不包含、存在、不存在 | 合并字符串数据。 |

### 受众共享

外部受众还可用作新区段定义的组件，从而将其属性规则添加到新区段。

目前，只有Adobe Audience Manager作为外部受众受支持，今后还将启用其他来源。 有关将Adobe Audience Manager受众与平台结合使用的更多信息，请参 [阅Adobe Audience Manager文档中的受众共享指南](https://docs.adobe.com/content/help/en/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html)。

### 区段共享

在平台中创建的细分可用于其他 [Adobe Experience Cloud核心服务](https://docs.adobe.com/content/help/zh-Hans/core-services/interface/experience-cloud.html)。 要启用此功能，您需要联系您的解决方案架构师或顾问。

## 其他数据类型

除了上述数据类型之外，支持的数据类型的列表还包括：

- 统一资源标识符(URI)
- 枚举
- 数值
- 长
- 整数
- 短
- 字节
- 布尔值
- 阵列
- 对象
- 地图