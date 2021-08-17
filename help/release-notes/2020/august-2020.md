---
title: Adobe Experience Platform 发行说明
description: Experience Platform发行说明2020年8月10日
doc-type: release notes
last-update: August 10, 2020
author: crhoades, ens28527
exl-id: 9347147f-e830-4487-aa12-f56723abb3c8
source-git-commit: a619227de30513bb06a22ce7b4f2fc13847c1ab6
workflow-type: tm+mt
source-wordcount: '568'
ht-degree: 7%

---

# Adobe Experience Platform 发行说明

**发行日期：2020 年 12 月 8 日**

Adobe Experience Platform 现有功能的更新包括：

- [[!DNL Data Science Workspace]](#dsw)
- [[!DNL Destinations]](#destinations)
- [[!DNL Real-time Customer Data Platform]](#rtcdp)
- [[!DNL Sources]](#sources)

## [!DNL Data Science Workspace] {#dsw}

[!DNL Data Science Workspace] 使用机器学习和人工智能从数据中释放洞察信息。[!DNL Data Science Workspace]集成到Adobe Experience Platform中，可帮助您跨Adobe解决方案使用内容和数据资产进行预测。

**新增功能**

| 功能 | 描述 |
| ------- | ----------- |
| [!DNL JupyterLab]中的VM改进 | 改进了长时间运行的[!DNL JupyterLab notebook]虚拟机的稳定性。 |

有关[!DNL JupyterLab]的更多信息，请参阅[[!DNL JupyterLab] 用户指南](../../data-science-workspace/jupyterlab/overview.md)。

## 目标 {#destinations}

在[实时客户数据平台](../../rtcdp/overview.md)中，目标是预先构建的与目标平台的集成，这些平台可无缝地向这些合作伙伴激活数据。

**新目标**

您可以在新目标中激活Adobe Experience Platform数据。 有关详细信息，请参阅下文：

| 目标 | 描述 |
|--- | ---|
| [!DNL Google Customer Match] | “Google客户匹配”允许您使用在线和离线数据，通过Google自有资产和运营资产与客户进行联系和重新参与，例如：[!DNL Search]、[!DNL Shopping]、Gmail和YouTube。 <br><br> 有关目 [!DNL Google Customer Match] [](../../destinations/catalog/advertising/google-customer-match.md) 标以及如何在实时CDP中设置目标的更多信息，请访问目标目录中的页面。 |

**新增功能**

| 功能 | 描述 |
|------- | -----------|
| 自定义文件名编辑器 | 更新了电子邮件营销目标和云存储目标的数据激活工作流，以便您编辑导出文件的名称。 有关更多信息，请参阅激活工作流中的[配置步骤](../../destinations/ui/activate-batch-profile-destinations.md) 。 |
| 推荐属性 | 更新了电子邮件营销目标和云存储目标的数据激活工作流程，以显示向导出文件添加的推荐属性。 有关更多信息，请参阅激活工作流中的[选择属性步骤](../../destinations/ui/activate-batch-profile-destinations.md)。 |

## [!DNL Real-time Customer Data Platform] {#rtcdp}

基于Experience Platform的实时客户数据平台([!DNL Real-time CDP])可帮助公司将已知和未知数据汇集在一起，在整个客户历程中通过智能决策激活客户档案。 [!DNL Real-time CDP] 整合多个企业数据源，以实时创建客户配置文件。然后，可以将这些配置文件构建的区段发送到下游目标，以便在所有渠道和设备上提供一对一的个性化客户体验。

**新增功能**

| 功能 | 描述 |
| ------- | ----------- |
| 支持IAB TCF 2.0 | [!DNL Real-time CDP] 现在是2.0版(TCF)的注 [!DNL Transparency & Consent Framework] 册供应商，如(IAB) [!DNL Interactive Advertising Bureau] 所述。您可以将数据操作和配置文件架构配置为接受由CMP生成的客户同意数据，并在将区段激活到下游目标时强制执行客户同意首选项。 |

有关[!DNL Real-time CDP]的更多信息，请参阅[[!DNL Real-time CDP] 概述](../../rtcdp/overview.md)。

## 源 {#sources}

Adobe Experience Platform可以从外部源摄取数据，同时允许您使用[!DNL Platform]服务来构建、标记和增强该数据。 您可以从各种来源摄取数据，如Adobe应用程序、基于云的存储、第三方软件和您的CRM系统。

[!DNL Experience Platform] 提供了RESTful API和交互式UI，让您能够轻松为各种数据提供程序设置源连接。这些源连接允许您验证并连接到外部存储系统和CRM服务，设置摄取运行的时间，以及管理数据摄取吞吐量。

**新增功能**

| 功能 | 描述 |
| ------- | ----------- |
| 流量运行监控 | 用户可以监视所有流运行并查看每个运行的详细视图，包括完成状态、运行持续时间、已处理文件列表、错误和量度。 有关更多信息，请参阅[监控数据流](../../sources/tutorials/ui/monitor.md)文档。 |
| 流运行通知 | 用户可以订阅事件并注册Web挂接，以接收有关流量运行的状态、量度和错误的实时通知。 |
| UI目录改进 | 更新了源目录屏幕，以便更轻松地访问选定对象的主要操作。 |

要了解有关源的更多信息，请参阅[源概述](../../sources/home.md)。
