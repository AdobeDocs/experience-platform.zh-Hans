---
title: Adobe Experience Platform 发行说明（2020 年 8 月）
description: Adobe Experience Platform 的 2020 年 8 月发行说明。
doc-type: release notes
last-update: August 10, 2020
author: crhoades, ens28527
exl-id: 9347147f-e830-4487-aa12-f56723abb3c8
source-git-commit: be2ad7a02d4bdf5a26a0847c8ee7a9a93746c2ad
workflow-type: tm+mt
source-wordcount: '576'
ht-degree: 25%

---

# Adobe Experience Platform 发行说明

**发行日期： 2020年8月12日**

Adobe Experience Platform 中现有功能的更新：

- [[!DNL Data Science Workspace]](#dsw)
- [[!DNL Destinations]](#destinations)
- [[!DNL Real-Time Customer Data Platform]](#rtcdp)
- [[!DNL Sources]](#sources)

## [!DNL Data Science Workspace] {#dsw}

[!DNL Data Science Workspace]使用机器学习和人工智能从您的数据中释放见解。 [!DNL Data Science Workspace]已集成到Adobe Experience Platform中，可帮助您跨Adobe解决方案使用您的内容和数据资源做出预测。

**新增功能**

| 功能 | 描述 |
| ------- | ----------- |
| [!DNL JupyterLab]中的VM改进 | 已改进长时间运行的[!DNL JupyterLab notebook]虚拟机的稳定性。 |

有关[!DNL JupyterLab]的详细信息，请参阅[[!DNL JupyterLab] 用户指南](../../data-science-workspace/jupyterlab/overview.md)。

## 目标 {#destinations}

在[Real-Time Customer Data Platform](../../rtcdp/overview.md)中，目标是与目标平台预先构建的集成，这些平台以无缝方式向这些合作伙伴激活数据。

**新目标**

提供了一些新目标，您可以在其中激活Adobe Experience Platform数据。 有关详细信息，请参阅下文：

| 目标 | 描述 |
|--- | ---|
| [!DNL Google Customer Match] | Google Customer Match允许您使用在线和离线数据，通过Google拥有和运营的资产(如： [!DNL Search]、[!DNL Shopping]、Gmail和YouTube)与客户联系并重新互动。 <br><br>访问目标目录中的[!DNL Google Customer Match] [页面](../../destinations/catalog/advertising/google-customer-match.md)，了解有关目标以及如何在Real-Time CDP中设置目标的更多信息。 |

**新增功能**

| 功能 | 描述 |
|------- | -----------|
| 自定义文件名编辑器 | 更新至电子邮件营销目标和云存储目标的数据激活工作流，允许您编辑导出文件的名称。 有关详细信息，请参阅激活工作流中的[配置步骤](../../destinations/ui/activate-batch-profile-destinations.md)。 |
| 建议的属性 | 更新了电子邮件营销目标和云存储目标的数据激活工作流，该工作流可显示建议您添加到导出文件的属性。 有关详细信息，请参阅激活工作流中的[选择属性步骤](../../destinations/ui/activate-batch-profile-destinations.md)。 |

## [!DNL Real-Time Customer Data Platform] {#rtcdp}

建立在 Experience Platform 上的 Real-Time Customer Data Platform ([!DNL Real-Time CDP]) 可以帮助公司汇集已知和未知数据，通过整个客户历程中通过智能决策激活客户轮廓。[!DNL Real-Time CDP] 结合多个企业数据源来实时创建客户轮廓。然后，根据这些轮廓构建的区段可以发送到下游目标，以便跨所有渠道和设备提供一对一的个性化客户体验。

**新增功能**

| 功能 | 描述 |
| ------- | ----------- |
| IAB TCF 2.0支持 | [!DNL Real-Time CDP]现在是[!DNL Transparency & Consent Framework] (TCF)的2.0版本的注册供应商，如[!DNL Interactive Advertising Bureau] (IAB)所述。 您可以配置数据操作和配置文件架构以接受CMP生成的客户同意数据，并在将区段激活到下游目标时强制实施客户的同意偏好设置。 |

有关 [!DNL Real-Time CDP] 的详细信息，请参阅 [[!DNL Real-Time CDP] 概述](../../rtcdp/overview.md)。

## 源 {#sources}

Adobe Experience Platform可以从外部源摄取数据，同时允许您使用[!DNL Experience Platform]服务来构建、标记和增强该数据。 您可以从各种源摄取数据，如Adobe应用程序、基于云的存储、第三方软件和您的CRM系统。

[!DNL Experience Platform]提供了一个RESTful API和一个交互式UI，可让您轻松为各种数据提供程序设置源连接。 这些源连接允许您验证并连接到外部存储系统和 CRM 服务、设置运行摄取操作的时间以及管理数据摄取吞吐量。

**新增功能**

| 功能 | 描述 |
| ------- | ----------- |
| 流量运行监控 | 用户可以监视所有流运行并查看每次运行的详细视图，包括完成状态、运行持续时间、已处理文件的列表、错误和量度。 有关详细信息，请参阅[监视数据流](../../sources/tutorials/ui/monitor.md)文档。 |
| 流量运行通知 | 用户可以订阅事件并注册Webhook，以接收有关流运行的状态、量度和错误的实时通知。 |
| UI目录改进 | 更新了源目录屏幕，以便更轻松地访问所选对象的主要操作。 |

要了解有关源的更多信息，请参阅[源概述](../../sources/home.md)。
