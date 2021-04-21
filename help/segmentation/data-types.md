---
keywords: Experience Platform；主题；热门主题；数据类型；数据类型；数据类型；数据类型；分段数据类型；分段数据类型；分段；分段服务；分段服务数据类型；
solution: Experience Platform
title: 分段服务中支持的数据类型
topic-legacy: overview
description: Adobe分段服务支持所有体验数据模型(XDM)数据类型。 构成区段定义的规则通过以下数据类型进行情境化。
exl-id: 73f932a7-f864-4566-ade7-c148a12dc83c
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '514'
ht-degree: 3%

---

# 分段服务中支持的数据类型

Adobe Experience Platform分段服务支持所有体验数据模型(XDM)数据类型。 构成区段定义的规则通过以下数据类型进行情境化。

## 字符串数据

区段定义使用字符串数据来定义区段受众的非数值约束，如“国家/地区名称”或“忠诚度项目级别”。

字符串数据使用逻辑、包含/独占和比较语句包括在区段定义中。 在将字符串属性添加到区段定义后，您可以使用字符串相关语句根据其他字符串字段对其进行评估。

| 语句类型 | 示例 |
| -------------- | -------- |
| 逻辑 | `and`、`or`、`not` |
| 包容/排斥 | `include`,  `must` `exist`,  `exclude`  `must not exist` |
| 比较 | `equals`、`does not equal`、`contains`、`starts with` |

## 日期数据

日期数据允许您通过使用特定开始/结束日期或使用下表中所示的与日期相关的语句，将基于时间的上下文分配给区段定义。 一种实施方式可能是创建与您的品牌在&#x200B;*今年*&#x200B;任何时间有互动的客户受众，而且最近几天在&#x200B;*内也活跃*。

| 示例字段 | 与日期相关的声明 | 时间轴 |
| ------------- | ------------------------ | --------- |
| person.firstPurchase | `today`、`yesterday`、`this month`、`this year` | 与区段建立之日有关。 |
| person.lastPurchase | `in last`、`during`、`before`、`after`、`within` | 在任何给定周/月内相关。 |

## 体验事件

作为Adobe Experience Platform模式,[!DNL XDM ExperienceEvents]记录与[!DNL Platform]集成应用程序的显式和隐式客户交互，包括交互发生时系统的快照。 [!DNL ExperienceEvents] 是事实记录。因此，在区段定义期间，它们是可供您使用的数据源。

如下表所示，事件数据使用关键字进行呈现，这些关键字有助于优化事件行为和指定事件属性。

| 关键字 | 使用 |
| ------- | --- |
| 包括/排除 | 通过包含或遗漏数据描述事件的行为。 |
| 任意/全部 | 帮助确定符合条件的区段的数量。 |
| “应用时间规则”切换按钮 | 合并日期数据。 |
| 等于、不等于、开始与、不与开始、结尾与、不以、包含、不包含、存在、不存在 | 合并字符串数据。 |

### 受众共享

外部受众也可用作新区段定义的组件，将其属性规则添加到新区段。

目前，仅支持Adobe Audience Manager作为外部受众，将来会启用其他源。 有关将Adobe Audience Manager受众与平台结合使用的更多信息，请参阅Adobe Audience Manager文档](https://docs.adobe.com/content/help/en/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html)中的[受众共享指南。

### 区段共享

在平台中创建的区段可在其他[Adobe Experience Cloud核心服务](https://docs.adobe.com/content/help/zh-Hans/core-services/interface/experience-cloud.html)中使用。 要启用此功能，您需要与解决方案架构师或顾问联系。

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
- 数组
- 对象
- 地图
