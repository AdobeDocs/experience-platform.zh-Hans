---
keywords: Experience Platform；主页；热门主题；数据类型；数据类型；数据类型；分段数据类型；分段；分段；分段服务；分段服务数据类型；
solution: Experience Platform
title: 分段服务中支持的数据类型
description: Adobe分段服务中支持所有Experience Data Model (XDM)数据类型。 构成区段定义的规则由以下数据类型进行上下文化。
exl-id: 73f932a7-f864-4566-ade7-c148a12dc83c
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '510'
ht-degree: 3%

---

# 分段服务中支持的数据类型

Adobe Experience Platform Segmentation Service支持所有Experience Data Model (XDM)数据类型。 构成区段定义的规则由以下数据类型进行上下文化。

## 字符串数据

区段定义使用字符串数据定义区段受众的非数字约束，如“国家/地区名称”或“忠诚度计划级别”。

字符串数据使用逻辑、包含/排除和比较语句包含在区段定义中。 将字符串属性添加到区段定义后，您可以使用字符串相关语句根据其他字符串字段评估该属性。

| 语句类型 | 示例 |
| -------------- | -------- |
| 逻辑 | `and`、`or`、`not` |
| 包含/排除 | `include`, `must` `exist`, `exclude`, `must not exist` |
| 比较 | `equals`、`does not equal`、`contains`、`starts with` |

## 日期数据

通过使用特定的开始/结束日期或使用与日期相关的语句，日期数据允许您为区段定义分配基于时间的上下文，如下表所示。 一种实施可能是创建随时与您的品牌进行交互的客户受众 *今年* 并且一直处于活动状态 *范围* 过去几天。

| 示例字段 | 日期相关报表 | 时间线 |
| ------------- | ------------------------ | --------- |
| person.firstPurchase | `today`、`yesterday`、`this month`、`this year` | 与生成区段的日期相关。 |
| person.lastPurchase | `in last`、`during`、`before`、`after`、`within` | 在任何给定周/月内相关。 |

## 体验事件

作为Adobe Experience Platform架构， [!DNL XDM ExperienceEvents] 记录与以下项的显性和隐性客户交互： [!DNL Platform] — 集成应用程序，包括进行交互时的系统快照。 [!DNL ExperienceEvents] 是事实记录。 因此，它们是在区段定义期间可供您使用的数据源。

如下表所示，使用关键字呈现事件数据，关键字有助于优化事件行为和指定事件属性。

| 关键词 | 使用 |
| ------- | --- |
| 包括/排除 | 通过包含或遗漏数据描述事件的行为。 |
| 任意/全部 | 帮助确定符合条件的区段数量。 |
| “应用时间规则”切换按钮 | 合并日期数据。 |
| 等于、不等于、开头为、开头为、结尾为、结尾为、包含、不包含、存在、不存在 | 合并字符串数据。 |

### 受众共享

外部受众也可以用作新区段定义的组件，将其属性规则添加到新区段。

目前，仅支持将Adobe Audience Manager作为外部受众，并且将来会启用其他源。 有关将Adobe Audience Manager受众与Platform结合使用的更多信息，请参阅 [Adobe Audience Manager文档中的受众共享指南](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html).

### 区段共享

在Platform中创建的区段可以在其他 [Adobe Experience Cloud核心服务](https://experienceleague.adobe.com/docs/core-services/interface/experience-cloud.html). 要启用此功能，您需要联系解决方案架构师或顾问。

## 其他数据类型

除了上述数据类型之外，受支持的数据类型列表还包括：

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
