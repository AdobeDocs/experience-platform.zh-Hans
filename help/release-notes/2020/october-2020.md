---
title: Adobe Experience Platform 发行说明
description: Experience Platform发行说明2020年10月
doc-type: release notes
last-update: October, 2020
author: crhoades, ens28527
translation-type: tm+mt
source-git-commit: 1b398e479137a12bcfc3208d37472aae3d6721e1
workflow-type: tm+mt
source-wordcount: '307'
ht-degree: 6%

---


# Adobe Experience Platform 发行说明

**发布日期：2020年10月**

Adobe Experience Platform的新增功能：

- [[!DNL访问控制]](#access-control)
- [[!DNL沙箱]](#sandboxes)

## [!DNL Access control] {#access-control}

[!DNL Experience Platform] 利用 [Adobe Admin Console](https://adminconsole.adobe.com) ()产品用户档案将用户与权限和沙箱关联起来。 权限控制对各种平台功能的访问，包括数据建模、用户档案管理和沙箱管理。

**主要功能**

| 功能 | 描述 |
|--- | ---|
| 权限 | 在中， [!DNL Admin Console]产品用户档案中的选 [!DNL Platform] 项卡允许您自定义哪些功能 [!DNL Platform] 可供附加到该用户档案的用户使用。 可用权限类别包括： [!UICONTROL 数据建模、]数据管理 [!UICONTROL 、]用户档案管理 [!UICONTROL 、身份、监控]、数据管理、 管理、沙箱管理、沙箱、、源。 |
| 访问沙箱 | 产品 [!UICONTROL _用户档案_] 中的“权限 [!DNL Platform] ”选项卡可授予用户对特定沙箱的访问权限。 有关更多信息，请 [参阅](#sandboxes) 以下沙箱部分。 |

有关详细信息，请参阅 [访问控制概述](../../access-control/home.md)。

## [!DNL Sandboxes] {#sandboxes}

[!DNL Experience Platform] 旨在在全球范围内丰富数字体验应用程序。 公司通常并行运行多个数字体验应用程序，需要满足这些应用程序的开发、测试和部署的需要，同时确保操作合规性。 为了满足这一需求，提 [!DNL Experience Platform] 供了沙箱，将单个实例分 [!DNL Platform] 为单独的虚拟环境，以帮助开发和发展数字体验应用程序。

**主要功能**

| 功能 | 描述 |
|--- | ---|
| 生产沙箱 | [!DNL Experience Platform] 提供一个无法删除或重置的生产沙箱。 |
| 非生产沙箱 | 可以为单个实例创建多个非生产沙箱， [!DNL Platform] 使您能够测试功能、运行实验并制作自定义配置，而不会影响生产沙箱。 |
| 沙箱切换器 | 在用 [!DNL Experience Platform] 户界面中，屏幕左上角的沙箱切换器允许您通过下拉菜单在可用沙箱之间切换。 |
| `x-sandbox-name` 标题 | 对API的所 [!DNL Experience Platform] 有调用现在必须包 `x-sandbox-name` 括新标头，其值引 `name` 用将执行操作的沙箱的属性。 |

有关详细信息，请参阅 [沙箱概述](../../sandboxes/home.md)。