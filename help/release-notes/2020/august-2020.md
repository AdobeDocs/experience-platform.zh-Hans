---
title: Adobe Experience Platform发行说明2020年8月
description: 2020年8月版Adobe Experience Platform发行说明。
doc-type: release notes
last-update: August 10, 2020
author: crhoades, ens28527
exl-id: 9347147f-e830-4487-aa12-f56723abb3c8
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '572'
ht-degree: 6%

---

# Adobe Experience Platform 发行说明

**发行日期：2020 年 8 月 12 日**

Adobe Experience Platform 现有功能的更新包括：

- [[!DNL Data Science Workspace]](#dsw)
- [[!DNL Destinations]](#destinations)
- [[!DNL Real-Time Customer Data Platform]](#rtcdp)
- [[!DNL Sources]](#sources)

## [!DNL Data Science Workspace] {#dsw}

[!DNL Data Science Workspace] 使用机器学习和人工智能从数据中释放洞察信息。 集成到Adobe Experience Platform, [!DNL Data Science Workspace] 可帮助您跨Adobe解决方案使用内容和数据资产进行预测。

**新增功能**

| 功能 | 描述 |
| ------- | ----------- |
| 在 [!DNL JupyterLab] | 提高了长跑的稳定性 [!DNL JupyterLab notebook] 虚拟机。 |

有关 [!DNL JupyterLab]，请参阅 [[!DNL JupyterLab] 用户指南](../../data-science-workspace/jupyterlab/overview.md).

## 目标 {#destinations}

在 [Real-time Customer Data Platform](../../rtcdp/overview.md)，目标是与目标平台的预建集成，可无缝地向这些合作伙伴激活数据。

**新目标**

您可以在新目标中激活Adobe Experience Platform数据。 有关详细信息，请参阅下文：

| 目标 | 描述 |
|--- | ---|
| [!DNL Google Customer Match] | Google客户匹配允许您使用在线和离线数据，跨Google自有和运营的资产访问客户并与其重新互动，例如： [!DNL Search], [!DNL Shopping]、Gmail和YouTube。 <br><br> 访问 [!DNL Google Customer Match] [页面](../../destinations/catalog/advertising/google-customer-match.md) （位于目标目录中），以了解有关目标以及如何在Real-Time CDP中设置该目标的更多信息。 |

**新增功能**

| 功能 | 描述 |
|------- | -----------|
| 自定义文件名编辑器 | 更新了电子邮件营销目标和云存储目标的数据激活工作流，以便您编辑导出文件的名称。 有关更多信息，请参阅 [ 配置步骤](../../destinations/ui/activate-batch-profile-destinations.md) 激活工作流中。 |
| 推荐属性 | 更新了电子邮件营销目标和云存储目标的数据激活工作流程，以显示向导出文件添加的推荐属性。 有关更多信息，请参阅 [选择属性步骤](../../destinations/ui/activate-batch-profile-destinations.md) 激活工作流中。 |

## [!DNL Real-Time Customer Data Platform] {#rtcdp}

构建于Experience Platform,Real-time Customer Data Platform([!DNL Real-Time CDP])可帮助公司整合已知和未知数据，在整个客户历程中通过智能决策激活客户用户档案。 [!DNL Real-Time CDP] 整合多个企业数据源，以实时创建客户配置文件。 然后，可以将这些配置文件构建的区段发送到下游目标，以便在所有渠道和设备上提供一对一的个性化客户体验。

**新增功能**

| 功能 | 描述 |
| ------- | ----------- |
| 支持IAB TCF 2.0 | [!DNL Real-Time CDP] 现在是2.0版本的 [!DNL Transparency & Consent Framework] (TCF)，如 [!DNL Interactive Advertising Bureau] (IAB)。 您可以将数据操作和配置文件架构配置为接受由CMP生成的客户同意数据，并在将区段激活到下游目标时强制执行客户同意首选项。 |

有关 [!DNL Real-Time CDP]，请参阅 [[!DNL Real-Time CDP] 概述](../../rtcdp/overview.md).

## 源 {#sources}

Adobe Experience Platform可以从外部源摄取数据，同时允许您使用 [!DNL Platform] 服务。 您可以从各种来源摄取数据，如Adobe应用程序、基于云的存储、第三方软件和您的CRM系统。

[!DNL Experience Platform] 提供了RESTful API和交互式UI，让您能够轻松为各种数据提供程序设置源连接。 这些源连接允许您验证并连接到外部存储系统和CRM服务，设置摄取运行的时间，以及管理数据摄取吞吐量。

**新增功能**

| 功能 | 描述 |
| ------- | ----------- |
| 流量运行监控 | 用户可以监视所有流运行并查看每个运行的详细视图，包括完成状态、运行持续时间、已处理文件列表、错误和量度。 请参阅 [监控数据流](../../sources/tutorials/ui/monitor.md) 文档以了解更多信息。 |
| 流运行通知 | 用户可以订阅事件并注册Web挂接，以接收有关流量运行的状态、量度和错误的实时通知。 |
| UI目录改进 | 更新了源目录屏幕，以便更轻松地访问选定对象的主要操作。 |

要进一步了解源，请参阅 [源概述](../../sources/home.md).
