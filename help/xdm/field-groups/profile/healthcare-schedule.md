---
title: 计划架构字段组
description: 了解计划架构字段组。
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: e01a6cd4cf42338f87222a5e2871cd6c3683309a
workflow-type: tm+mt
source-wordcount: '234'
ht-degree: 5%

---

# [!UICONTROL 计划]架构字段组

[!UICONTROL 计划]是[[!DNL XDM Individual Profile] 类](../../classes/individual-profile.md)和[[!DNL Provider class]](../../classes/provider.md)的标准架构字段组。 它提供单个对象类型字段`healthcareSchedule`，该字段是可用于预订约会的时隙的容器。

![字段组结构](../../images/field-groups/schedule.png)

| 显示名称 | 属性 | 数据类型 | 描述 |
| --- | --- | --- | --- |
| [!UICONTROL 操作者] | `actor` | [[!UICONTROL 引用]](../../data-types/healthcare/reference.md)的数组 | 引用此计划的插槽，可提供这些引用资源的可用性详细信息。 |
| [!UICONTROL 标识符] | `identifier` | [[!UICONTROL 标识符]](../../data-types/healthcare/identifier.md)的数组 | 计划的外部标识符。 |
| [!UICONTROL 计划展望期] | `planningHorizon` | [[!UICONTROL 周期]](../../data-types/healthcare/period.md) | 引用此计划的插槽涵盖的时间段，即使不存在任何时间段。 |
| [!UICONTROL 服务类别] | `serviceCategory` | [[!UICONTROL 可编码概念]](../../data-types/healthcare/codeable-concept.md)的数组 | 要在约会期间执行的服务的广泛分类。 |
| [!UICONTROL 服务类型] | `serviceType` | [[!UICONTROL 可编码引用]](../../data-types/healthcare/codeable-reference.md)的数组 | 在约会期间要执行的特定服务。 |
| [!UICONTROL 专业] | `specialty` | [[!UICONTROL 可编码概念]](../../data-types/healthcare/codeable-concept.md)的数组 | 执行指定时要求的服务所需的从业人员的专长。 |
| [!UICONTROL 活动] | `active` | 布尔值 | 指示计划记录是否正在被使用。 |
| [!UICONTROL 评论] | `comment` | 字符串 | 对可用性的注释，用于描述任何扩展信息，例如插槽上的自定义约束。 |
| [!UICONTROL 名称] | `name` | 字符串 | 在搜索时向使用者呈现的时间表的描述。 |

有关字段组的更多详细信息，请参阅公共XDM存储库：

* [填充示例](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/schedule.example.1.json)
* [完整架构](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/schedule.schema.json)
