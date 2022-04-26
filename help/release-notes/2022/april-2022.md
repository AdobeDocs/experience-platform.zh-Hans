---
title: Adobe Experience Platform发行说明2022年4月
description: 2022年4月的Adobe Experience Platform发行说明。
source-git-commit: 4bbf7642a456f36ea0fe7fc1c8d68ad37351ff4c
workflow-type: tm+mt
source-wordcount: '907'
ht-degree: 4%

---

# Adobe Experience Platform 发行说明

**发布日期：2022 年 4 月 27 日**

Adobe Experience Platform 现有功能的更新包括：

- [体验数据模型(XDM)](#xdm)

## 体验数据模型(XDM) {#xdm}

XDM是一种开源规范，为引入Adobe Experience Platform的数据提供通用结构和定义（架构）。 通过遵循XDM标准，可以将所有客户体验数据纳入到通用的表示形式中，以更快、更集成的方式提供洞察。 您可以从客户操作中获得有价值的分析，通过区段定义客户受众，以及将客户属性用于个性化目的。

**新增功能**

| 功能 | 描述 |
| --- | --- |
| 添加或删除架构的单个标准字段 | 架构编辑器UI现在允许您向架构中添加部分标准字段组，从而为您选择包含的字段提供了更大的灵活性，而无需从头开始构建自定义资源。<br><br>现在，您还可以直接在架构结构中定义临时自定义字段，并将它们分配给新的或现有的自定义字段组，而无需事先创建或编辑字段组。<br><br>请参阅 [在UI中创建和编辑架构](../../xdm/ui/resources/schemas.md) 以了解有关这些新工作流的更多信息。 |

{style=&quot;table-layout:auto&quot;}

**新的XDM组件**

| 组件类型 | 名称 | 描述 |
| --- | --- | --- |
| 全局模式 | [[!UICONTROL 数据卫生操作请求]](https://github.com/adobe/xdm/blob/master/schemas/hygiene/aep-hygiene-ops-record.schema.json) | 捕获用于删除或修改指定数据集或沙盒中记录的数据清理请求的详细信息。 |
| 描述符 | [[!UICONTROL 时间序列粒度描述符]](https://github.com/adobe/xdm/blob/master/schemas/descriptors/time-series/descriptorTimeSeriesGranularity.schema.json) | 指示时间系列和概要数据的粒度。 当应用到架构时，该架构的 `timestamp` 字段是此粒度的时段中的第一个时间戳。 |
| 类 | [[!UICONTROL XDM概要量度]](https://github.com/adobe/xdm/blob/master/components/classes/summary_metrics.schema.json) | 提供具有分组维的预汇总量度，例如具有GROUP BY的SQL SELECT的结果。 |
| 字段组 | [[!UICONTROL 同意策略评估结果图]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-site-search.schema.json) | 捕获个人的同意策略评估结果。 |
| 字段组 | [[!UICONTROL 网站搜索]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-site-search.schema.json) | 捕获与网站搜索相关的信息，如搜索查询、过滤和排序。 |
| 字段组 | [[!UICONTROL 合并潜在客户]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/events/merge-leads.schema.json) | 捕获合并两个或更多潜在客户的事件的详细信息。 |
| 字段组 | [[!UICONTROL 已发送电子邮件]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/events/emailsent.schema.json) | 捕获向收件人发送电子邮件的事件的详细信息。 |
| 字段组 | [[!UICONTROL 拼合字段]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-stitching.schema.json) | 捕获通过事件的身份拼合流程计算的值。 |
| 字段组 | [[!UICONTROL 审核的辅助收件人详细信息]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/customerJourneyManagement/secondary-recipient-detail.schema.json) | 用于捕获审核的辅助收件人详细信息的Adobe Journey Optimizer字段组。 |
| 字段组 | [[!UICONTROL XDM业务帐户人员关系详细信息]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/account-person/account-person-details.schema.json) | 捕获与帐户与人员关系相关的详细信息。 |
| 字段组 | [[!UICONTROL 帐户人员详细信息]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/account-person/account-person-details.schema.json) | 捕获与帐户与人员关系相关的详细信息。 |
| 数据类型 | [[!UICONTROL 购物车]](https://github.com/adobe/xdm/blob/master/components/datatypes/cart.schema.json) | 捕获有关电子商务购物车的信息。 |
| 数据类型 | [[!UICONTROL 装运]](https://github.com/adobe/xdm/blob/master/components/datatypes/shipping.schema.json) | 捕获一个或多个产品的装运信息。 |
| 数据类型 | [[!UICONTROL 网站搜索]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-site-search.schema.json) | 捕获有关网站搜索活动的信息。 |
| 扩展(Workfront) | [[!UICONTROL 操作任务属性]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/opTask.schema.json) | 捕获与操作任务相关的详细信息。 |
| 扩展(Workfront) | [[!UICONTROL 工作Portfolio属性]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/portfolio.schema.json) | 捕获与工作组合相关的详细信息。 |
| 扩展(Workfront) | [[!UICONTROL 工作计划属性]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/program.schema.json) | 捕获与工作程序相关的详细信息。 |
| 扩展(Workfront) | [[!UICONTROL 工作项目属性]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/project.schema.json) | 捕获与工作项目相关的详细信息。 |

{style=&quot;table-layout:auto&quot;}

**更新了XDM组件**

| 组件类型 | 名称 | 更新描述 |
| --- | --- | --- |
| 全局模式 | [[!UICONTROL 目标]](https://github.com/adobe/xdm/blob/master/schemas/destinations/destination.schema.json) | 的新枚举值 `destinationCategory`. |
| 描述符 | [[!UICONTROL 友好名称描述符]](https://github.com/adobe/xdm/blob/master/schemas/descriptors/display/alternateDisplayInfo.schema.json) | 添加了对删除建议值(`meta:enum`)，而不是标准字段中需要的字段。 |
| 字段组 | [[!UICONTROL 用户登录过程]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-user-login-details.schema.json) | `createProfile` 字段。 |
| 数据类型 | [[!UICONTROL 商务]](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/commerce.schema.json) | 添加了几个与购物车相关的字段。 |
| 数据类型 | [[!UICONTROL 产品列表项]](https://github.com/adobe/xdm/blob/master/components/datatypes/productlistitem.schema.json) | 为选定选项和折扣金额添加了新字段。 |
| 扩展（智能服务） | [[!UICONTROL 智能服务历程AI发送时间优化]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/intelligentServices/profile-journeyai-sendtimeoptimization.schema.json) | 优化发送时间得分的存储格式。 |
| 扩展(Workfront) | [[!UICONTROL Workfront更改事件]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/changeevent.schema.json) | 多个字段替换为 `workfront:customData` 字段。 |
| 扩展(Workfront) | [[!UICONTROL 工作任务属性]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/task.schema.json) | 添加了多个字段。 |
| 扩展(Workfront) | [[!UICONTROL 工作对象]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/workobject.schema.json) | 父对象类型和自定义表单字段的新字段。 |

{style=&quot;table-layout:auto&quot;}

有关Platform中XDM的更多信息，请参阅 [XDM系统概述](../../xdm/home.md).
