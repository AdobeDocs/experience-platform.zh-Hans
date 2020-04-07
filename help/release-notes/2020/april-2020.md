---
title: Adobe Experience Platform 发行说明
description: Experience Platform发行说明2020年4月8日
doc-type: release notes
last-update: March 4, 2020
author: ens71067
translation-type: tm+mt
source-git-commit: c3166bea873572fe6ee2e63dfd13bc64d81e252b

---


# Adobe Experience Platform 发行说明

## 发行日期：2020 年 4 月 8 日

## 隐私服务

新的法律和组织法规授予用户根据请求从数据存储中访问或删除其个人数据的权利。 Adobe Experience Platform Privacy Service提供RESTful API和用户界面，帮助您管理来自客户的这些数据请求。 通过隐私服务，您可以提交从Adobe Experience Cloud应用程序访问和删除私人或个人客户数据的请求，从而促进自动遵守法律和组织隐私法规。

**新增功能**

| 功能 | 描述 |
| --- | --- |
| PDPA支持 | 现在，可以根据泰国的个人数据保护法(PDPA)创建和跟踪隐私请求。 在API中发出隐私请求时，数 `regulation` 组接受值“pdpa_tha”。 |
| 命名空间UI中的类型 | 您现在可以在隐私服务UI的Request Builder中指定不同的命名空间类型。 有关详细 [信息，请参阅](../../privacy-service/ui/user-guide.md) 《用户指南》。 |
| 旧端点弃用 | 旧API端点(`data/privacy/gdpr`)已弃用。 |

已知问题

* None

有关隐私服务的更多信息，请阅读隐私服务 [概述开始](../../privacy-service/home.md)。

<!-- ## Access control

Experience Platform leverages [Adobe Admin Console](https://adminconsole.adobe.com) product profiles to link users with permissions and sandboxes. Permissions control access to a variety of Platform capabilities, including data modeling, profile management, and sandbox administration.

### Key features

|Feature | Description|
|--- | ---|
|Permissions | In the Admin Console, the _Permissions_ tab within a Platform product profile allows you customize which Platform capabilities are available for the users attached to that profile. Available permission categories include: Data Modeling, Data Management, Profile Management, Identities, Data Monitoring, Sandbox Administration, Destinations, Sources.|
|Access to sandboxes | The _Permissions_ tab within a Platform product profile can grant users access to specific sandboxes. See the section on [sandboxes](#sandboxes) below for more information.|

For more information, please see the [access control overview](../../access-control/home.md).

## Sandboxes

Experience Platform is built to enrich digital experience applications on a global scale. Companies often run multiple digital experience applications in parallel and need to cater for the development, testing, and deployment of these applications while ensuring operational compliance. In order to address this need, Experience Platform provides sandboxes which partition a single Platform instance into separate virtual environments to help develop and evolve digital experience applications.

### Key features

|Feature | Description|
|--- | ---|
|Production sandbox | Experience Platform provides a single production sandbox, which cannot be deleted or reset.|
|Non-production sandboxes | Multiple non-production sandboxes can be created for a single Platform instance, allowing you to test features, run experiments, and make custom configurations without impacting your production sandbox.|
|Sandbox switcher | In the Experience Platform user interface, the sandbox switcher in the top-left corner of the screen allows you to switch between available sandboxes through a dropdown menu.|
|`x-sandbox-name` header | All calls to Experience Platform APIs must now include the new `x-sandbox-name` header, whose value references the `name` attribute of the sandbox the operation will take place in.|

For more information, please see the [sandboxes overview](../../sandboxes/home.md). -->