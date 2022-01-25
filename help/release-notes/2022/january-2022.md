---
title: Adobe Experience Platform 发行说明
description: Adobe Experience Platform的最新发行说明。
source-git-commit: 641fcab89b849d91a075fa5058421950bc7fecd7
workflow-type: tm+mt
source-wordcount: '431'
ht-degree: 9%

---

# Adobe Experience Platform 发行说明

**发行日期：2021 年 1 月 26 日**

Adobe Experience Platform 现有功能的更新包括：

- [警报](#alerts)
- [数据准备](#data-prep)
- [沙盒](#sandboxes)
- [分段服务](#segmentation)

## 警报 {#alerts}

Experience Platform允许您订阅各种平台活动的基于事件的警报。 您可以通过 [!UICONTROL 警报] 选项卡，可以选择通过UI本身或电子邮件通知接收警报消息。

**更新功能**

| 功能 | 描述 |
| --- | --- |
| 新警报规则 | 现在，有几个新的警报规则可用于与数据获取、身份、用户档案、分段和激活相关的工作流。 请参阅 [警报规则](../../observability/alerts/rules.md) ，以了解更新的警报类型列表。 |

有关平台中警报的更多信息，请参阅 [警报概述](../../observability/alerts/overview.md).

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] 允许数据工程师在体验数据模型(XDM)之间映射、转换和验证数据。

**更新功能**

| 功能 | 描述 |
| --- | --- |
| 整合的映射体验 | Platform UI中的新映射界面为您提供了一致的映射体验，以便利用智能映射推荐、手动配置映射规则以及调试映射集中发生的任何错误。 有关更多信息，请参阅 [[!DNL Data Prep] UI指南](../../data-prep/home.md). |

有关 [!DNL Data Prep]，请参阅 [[!DNL Data Prep] 概述](../../data-prep/home.md).

## 沙盒 {#sandboxes}

Adobe Experience Platform旨在在全球范围内丰富数字体验应用程序。 公司通常并行运行多个数字体验应用程序，需要满足这些应用程序的开发、测试和部署的需要，同时确保操作合规性。 为了满足这一需求，Experience Platform提供了将单个Platform实例分区为单独虚拟环境的沙盒，以帮助开发和改进数字体验应用程序。

**更新功能**

| 功能 | 描述 |
| --- | --- |
| 沙盒UI增强 | 沙盒指示器现在集成在所有Platform UI应用程序的标头中。 沙盒指示器可显示沙盒名称、区域和类型，并允许您访问下拉菜单以在沙盒之间切换。 有关更多信息，请参阅 [sandbox UI指南](../../sandboxes/ui/user-guide.md). |

有关沙箱的详细信息，请参阅 [沙箱概述](../../sandboxes/home.md).

## 分段服务 {#segmentation}

[!DNL Segmentation Service] 通过描述区分客户群中可销售人群的标准来定义特定的用户档案子集。 区段可以基于记录数据（如人口统计信息）或表示客户与您的品牌交互的时间序列事件。

**更新功能**

| 功能 | 描述 |
| --- | --- |
| 区段匹配 | 区段匹配是一项数据协作服务，允许两个或更多Platform用户以安全、受管理和隐私友好的方式，基于通用标识符交换数据。 有关更多信息，请参阅 [区段匹配概述](../../segmentation/ui/segment-match/overview.md). |

有关 [!DNL Segmentation Service]，请参阅 [分段概述](../../segmentation/home.md).
