---
keywords: 电子邮件；电子邮件；电子邮件；电子邮件目标
title: 电子邮件营销目标概述
type: Tutorial
description: 电子邮件服务提供商(ESP)允许您管理电子邮件营销活动，例如发送促销电子邮件活动。 了解哪些ESP作为Experience Platform目标受支持。
exl-id: e07f8c5a-0424-4de5-810f-3d5711ef4606
source-git-commit: d6ea94b275ab0ed7c0638200188fe7ada7bacf5c
workflow-type: tm+mt
source-wordcount: '377'
ht-degree: 4%

---

# 电子邮件营销目标概述 {#email-marketing-destinations}

## 概述 {#overview}

电子邮件服务提供商(ESP)使您能够管理电子邮件营销活动，如发送促销电子邮件活动。 Adobe Experience Platform通过允许您将区段激活到电子邮件营销目标来与ESP集成。

## 支持的电子邮件营销目标 {#supported-destinations}

Adobe Experience Platform支持以下电子邮件营销目标：

* [Adobe Campaign](adobe-campaign.md)
* [Adobe Campaign Managed Cloud Services](adobe-campaign-managed-services.md)
* [(API)OracleEloqua](oracle-eloqua-api.md)
* [(API)SalesforceMarketing Cloud](salesforce-marketing-cloud-exact-target.md)
* [（文件）OracleEloqua](oracle-eloqua.md)
* [（文件）SalesforceMarketing Cloud](salesforce-marketing-cloud.md)
* [OracleResponsys](oracle-responsys.md)
* [SendGrid](sendgrid.md)

## 连接到新的电子邮件营销目标 {#connect-destination}

要将区段发送到营销活动的电子邮件营销目标，Platform必须先连接到该目标。 请参阅 [目标创建教程](../../ui/connect-destination.md) 以了解有关设置新目标的详细信息。

## 将受众激活到电子邮件营销目标时的最佳实践 {#best-practices}

### 身份选择 {#identity}

Adobe建议您从 [合并模式](../../../profile/home.md#profile-fragments-and-union-schemas). 这是您的用户身份已从中键出的字段。 最常见的情况是，此字段是电子邮件地址，但也可以是忠诚度计划ID或电话号码。 有关架构中最常见的唯一标识符及其XDM字段，请参阅下表。

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

## 将区段激活到电子邮件营销目标 {#activate}

目录中的某些电子邮件营销目标通过与目标的API集成，以流式方式导出用户档案。

其他目标会将文件导出到云存储位置。 导出完成后，您需要将数据从云存储位置导入电子邮件营销目标。

访问 [支持的电子邮件营销目标](#supported-destinations) 部分以了解如何将区段激活到每个电子邮件营销目标。

## 其他资源 {#additional-resources}

* [激活受众数据以批量配置文件导出目标](../../ui/activate-batch-profile-destinations.md)
* [使用流量服务API创建电子邮件营销目标并激活数据](../../api/connect-activate-batch-destinations.md)
