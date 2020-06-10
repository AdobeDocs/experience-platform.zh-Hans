---
title: Adobe Experience Platform 发行说明
description: Experience Platform发行说明2020年8月10日
doc-type: release notes
last-update: August 10, 2020
author: crhoades, ens28527
translation-type: tm+mt
source-git-commit: 7f9d1120ac323c60f899cb1cf855e55db20437ed
workflow-type: tm+mt
source-wordcount: '328'
ht-degree: 7%

---


# Adobe Experience Platform 发行说明

**发布日期：2020 年 6 月 10 日**

Adobe Experience Platform的新增功能：

- [访问控制](#access-control)
- [沙箱](#sandboxes)

## 访问控制 {#access-control}

Experience Platform利用 [Adobe Admin Console产品用户档案](https://adminconsole.adobe.com) ，将用户与权限和沙箱关联起来。 权限控制对各种平台功能的访问，包括数据建模、用户档案管理和沙箱管理。

**主要功能**

| 功能 | 描述 |
|--- | ---|
| 权限 | 在Admin Console中，平台产 _品用户档案_ 中的“权限”选项卡允许您自定义哪些平台功能可供附加到该用户档案的用户使用。 可用权限类别包括： 数据建模、数据管理、用户档案管理、身份、数据监控、沙箱管理、目标、源。 |
| 访问沙箱 | 平台 _产品用户档案_ 中的“权限”选项卡可授予用户对特定沙箱的访问权限。 有关更多信息，请 [参阅](#sandboxes) 下面沙箱的部分。 |

有关详细信息，请参阅 [访问控制概述](../../access-control/home.md)。

## 沙箱 {#sandboxes}

Experience Platform旨在在全球范围内丰富数字体验应用程序。 公司通常并行运行多个数字体验应用程序，需要满足这些应用程序的开发、测试和部署的需要，同时确保操作合规性。 为了满足这一需求，Experience Platform提供了沙箱，可将单个平台实例分为单独的虚拟环境，以帮助开发和发展数字体验应用程序。

**主要功能**

| 功能 | 描述 |
|--- | ---|
| 生产沙箱 | Experience Platform提供单个生产沙箱，无法删除或重置。 |
| 非生产沙箱 | 可以为单个平台实例创建多个非生产沙箱，使您能够测试功能、运行实验和制作自定义配置，而不会影响生产沙箱。 |
| 沙箱切换器 | 在Experience Platform用户界面中，屏幕左上角的沙箱切换器允许您通过下拉菜单在可用沙箱之间切换。 |
| `x-sandbox-name` 标题 | 对Experience Platform API的所有调用现在必 `x-sandbox-name` 须包括新标头，其值引 `name` 用将执行操作的沙箱的属性。 |

有关详细信息，请参阅 [沙箱概述](../../sandboxes/home.md)。