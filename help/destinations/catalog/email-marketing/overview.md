---
keywords: 电子邮件；电子邮件；电子邮件；电子邮件目标
title: 电子邮件营销目标概述
type: Tutorial
description: 电子邮件服务提供商(ESP)允许您管理电子邮件营销活动，如发送促销电子邮件促销活动。 了解哪些ESP支持作为Experience Platform目标。
exl-id: e07f8c5a-0424-4de5-810f-3d5711ef4606
source-git-commit: d6402f22ff50963b06c849cf31cc25267ba62bb1
workflow-type: tm+mt
source-wordcount: '374'
ht-degree: 5%

---

# 电子邮件营销目标概述 {#email-marketing-destinations}

## 概述 {#overview}

电子邮件服务提供商(ESP)使您能够管理电子邮件营销活动，如发送促销电子邮件营销活动。 Adobe Experience Platform通过允许您激活受众到电子邮件营销目标而与ESP集成。

## 支持的电子邮件营销目标 {#supported-destinations}

Adobe Experience Platform支持以下电子邮件营销目标：

* [Adobe Campaign](adobe-campaign.md)
* [Adobe Campaign Managed Cloud Services](adobe-campaign-managed-services.md)
* [Mailchimp 兴趣类别](mailchimp-interest-categories.md)
* [(API)OracleEloqua](oracle-eloqua-api.md)
* [(API) [!DNL Salesforce Marketing Cloud]](salesforce-marketing-cloud-exact-target.md)
* [（文件）OracleEloqua](oracle-eloqua.md)
* [（文件） [!DNL Salesforce Marketing Cloud]](salesforce-marketing-cloud.md)
* [[!DNL Salesforce Marketing Cloud Account Engagement]](salesforce-marketing-cloud-account-engagement.md)
* [oracleResponsys](oracle-responsys.md)
* [发送网格](sendgrid.md)

## 连接到新的电子邮件营销目标 {#connect-destination}

要将受众发送到营销活动的电子邮件营销目标，平台必须首先连接到目标。 请参阅 [目标创建教程](../../ui/connect-destination.md) 有关设置新目标的详细信息。

## 将受众激活到电子邮件营销目标时的最佳实践 {#best-practices}

### 身份选择 {#identity}

Adobe建议您从 [合并模式](../../../profile/home.md#profile-fragments-and-union-schemas). 这是您的用户标识的键值字段。 最常见的情况是，此字段是电子邮件地址，但也可以是忠诚度计划ID或电话号码。 有关架构中最常见的唯一标识符及其XDM字段，请参阅下表。

| 唯一标识符 | 统一架构中的XDM字段 |
|----------------- | ---------------------------|
| Email Address | `personalEmail.address` |
| Phone | `mobilePhone.number` |
| 忠诚度计划ID | `Customer-defined XDM field` |

{style="table-layout:auto"}

### 其他目标属性 {#other-destination-attributes}

在架构字段选择器中，选择要导出到电子邮件目标的其他字段。 一些推荐选项包括：

| 架构 | XDM字段 |
|------ | ---------|
| 名字 | `person.name.firstName` |
| 姓氏 | `person.name.lastName` |
| Phone | `mobilePhone.number` |
| 地址城市 | `homeAddress.city` |
| 地址状态 | `homeAddress.stateProvince` |
| 地址邮政编码 | `homeAddress.postalCode` |
| 生日 | `person.birthDayAndMonth` |
| 区段会员资格 | `segmentMembership.status` |

{style="table-layout:auto"}

## 将受众激活到电子邮件营销目标 {#activate}

目录中的某些电子邮件营销目标通过与目标的API集成以流式方式导出用户档案。

其他目标将文件导出到云存储位置。 导出完成后，您需要将数据从云存储位置导入电子邮件营销目标。

请访问以下链接中的 [支持的电子邮件营销目标](#supported-destinations) 部分，了解如何将受众激活到每个电子邮件营销目标。

## 其他资源 {#additional-resources}

* [将受众数据激活到批量配置文件导出目标](../../ui/activate-batch-profile-destinations.md)
* [使用流服务API创建电子邮件营销目标并激活数据](../../api/connect-activate-batch-destinations.md)
