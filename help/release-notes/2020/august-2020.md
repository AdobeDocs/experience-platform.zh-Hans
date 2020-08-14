---
title: Adobe Experience Platform 发行说明
description: Experience Platform发行说明2020年8月10日
doc-type: release notes
last-update: August 10, 2020
author: crhoades, ens28527
translation-type: tm+mt
source-git-commit: 8b540a108336ae4475f072b71a34e37cac064826
workflow-type: tm+mt
source-wordcount: '452'
ht-degree: 6%

---


# Adobe Experience Platform 发行说明

**发行日期：2020 年 8 月 12 日**

Adobe Experience Platform现有功能更新：

- [[!DNL数据科学工作区]](#dsw)
- [!DNL Destinations](#destinations)
- [[!DNL源]](#sources)

## [!DNL Data Science Workspace] {#dsw}

[!DNL Data Science Workspace] 使用机器学习和人工智能从数据中释放洞察。 集成到Adobe Experience Platform，帮 [!DNL Data Science Workspace] 助您跨Adobe解决方案使用内容和数据资产进行预测。

**新增功能**

| 功能 | 描述 |
| ------- | ----------- |
| VM改进 [!DNL JupyterLab] | 提高了长运行虚拟机的 [!DNL JupyterLab notebook] 稳定性。 |

有关的详细信 [!DNL JupyterLab]息，请参阅 [[!DNL JupyterLab] 用户指南](../../data-science-workspace/jupyterlab/overview.md)。

## 目标 {#destinations}

在 [Adobe实时数据平台中](../../rtcdp/overview.md)，目标是预建的与目标平台集成，以无缝方式向这些合作伙伴激活数据。

**新目标**

您可以在新的目的地激活Adobe Experience Platform数据。 有关详细信息，请参阅以下内容：

| 目标 | 描述 |
|--- | ---|
| [!DNL Google Customer Match] | Google客户匹配允许您使用线上和线下数据在Google自有和运营的资产中触及客户并与其重新互动，例如： [!DNL Search]、 [!DNL Shopping]Gmail和YouTube。 <br><br> 请访 [!DNL Google Customer Match] 问目 [标目录中的页](/help/rtcdp/destinations/google-customer-match-destination.md) ，以了解有关目标以及如何在Adobe实时CDP中设置它的更多信息。 |

**新增功能**

| 功能 | 描述 |
|------- | -----------|
| 自定义文件名编辑器 | 更新至电子邮件营销目标和云激活目标的存储工作流，以便编辑导出文件的名称。 有关详细信息，请参阅激活 [ 工作流中](/help/rtcdp/destinations/activate-destinations.md#configure) 的配置步骤。 |
| 推荐属性 | 更新至电子邮件营销目标和云激活目标的存储工作流，以显示您要添加到导出文件的推荐属性。 有关详细信息，请参阅激活 [工作流中的](/help/rtcdp/destinations/activate-destinations.md#select-attributes) “选择属性”步骤。 |

## 源 {#sources}

Adobe Experience Platform可以从外部来源收集数据，同时允许您使用服务来构建、标记和增强该 [!DNL Platform] 数据。 您可以从各种来源(如Adobe应用程序、基于云的存储、第三方软件和您的CRM系统)收集数据。

[!DNL Experience Platform] 提供REST风格的API和交互式UI，让您可以轻松为各种数据提供者设置源连接。 这些源连接允许您验证并连接到外部存储系统和CRM服务，设置获取运行的时间，以及管理数据获取吞吐量。

**新增功能**

| 功能 | 描述 |
| ------- | ----------- |
| 流运行监控 | 用户可以监视所有流运行并查看每个运行的详细视图，包括完成状态、运行持续时间、已处理文件的列表、错误和度量。 有关详细 [信息，请参见](../../sources/tutorials/ui/monitor.md) “监视数据流”文档。 |
| 流运行通知 | 用户可以订阅事件并注册网络挂接，以接收有关流运行的状态、度量和错误的实时通知。 |
| UI目录改进 | 对源目录屏幕进行更新，以便更轻松地访问选定对象的主要操作。 |

要进一步了解源，请参阅 [源概述](../../sources/home.md)。
