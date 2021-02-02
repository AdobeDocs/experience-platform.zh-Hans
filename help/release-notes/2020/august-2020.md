---
title: Adobe Experience Platform 发行说明
description: Experience Platform发行说明2020年8月10日
doc-type: release notes
last-update: August 10, 2020
author: crhoades, ens28527
translation-type: tm+mt
source-git-commit: 49c984a60fd699706eec508ec1d786340df40b57
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

[!DNL Data Science Workspace] 使用机器学习和人工智能从数据中释放洞察。[!DNL Data Science Workspace]集成到Adobe Experience Platform，可帮助您跨Adobe解决方案使用内容和数据资产进行预测。

**新增功能**

| 功能 | 描述 |
| ------- | ----------- |
| [!DNL JupyterLab]中的VM改进 | 改进了长运行[!DNL JupyterLab notebook]虚拟机的稳定性。 |

有关[!DNL JupyterLab]的详细信息，请参见[[!DNL JupyterLab] 用户指南](../../data-science-workspace/jupyterlab/overview.md)。

## 目标 {#destinations}

在[实时客户数据平台](../../rtcdp/overview.md)中，目标是预建的与目标平台集成，这些平台以无缝方式将数据激活给这些合作伙伴。

**新目标**

您可以在新的目的地激活Adobe Experience Platform数据。 有关详细信息，请参阅以下内容：

| 目标 | 描述 |
|--- | ---|
| [!DNL Google Customer Match] | Google客户匹配允许您使用线上和线下数据在Google自有和运营的资产中触及客户并与其重新互动，例如：[!DNL Search]、[!DNL Shopping]、Gmail和YouTube。 <br><br> 有关目 [!DNL Google Customer Match] [](../../destinations/catalog/advertising/google-customer-match.md) 标以及如何在实时CDP中设置目标的详细信息，请访问目标目录中的页。 |

**新增功能**

| 功能 | 描述 |
|------- | -----------|
| 自定义文件名编辑器 | 更新至电子邮件营销目标和云激活目标的存储工作流，以便编辑导出文件的名称。 有关详细信息，请参阅激活工作流中的[配置步骤](../../destinations/ui/activate-destinations.md#configure)。 |
| 推荐属性 | 更新至电子邮件营销目标和云激活目标的存储工作流，以显示您要添加到导出文件的推荐属性。 有关详细信息，请参阅激活工作流中的[选择属性步骤](../../destinations/ui/activate-destinations.md#select-attributes)。 |

## [!DNL Real-time Customer Data Platform] {#rtcdp}

实时客户数据平台([!DNL Real-time CDP])以Experience Platform为构建基础，帮助公司将已知和未知的数据整合在一起，在客户旅程中通过智能决策激活客户用户档案。 [!DNL Real-time CDP] 结合多个企业数据源，实时创建客户用户档案。然后，根据这些用户档案构建的细分可以发送到下游目标，以便在所有渠道和设备上提供一对一的个性化客户体验。

**新增功能**

| 功能 | 描述 |
| ------- | ----------- |
| IAB TCF 2.0支持 | [!DNL Real-time CDP] 如(IAB)所述，现在是2.0版 [!DNL Transparency & Consent Framework] 本(TCF)的注册 [!DNL Interactive Advertising Bureau] 供应商。您可以配置数据操作和用户档案模式，以接受由CMP生成的客户同意数据，并在将区段激活到下游目标时强制执行客户同意偏好。 |

有关[!DNL Real-time CDP]的详细信息，请参阅[[!DNL Real-time CDP] 概述](../../rtcdp/overview.md)。

## 源 {#sources}

Adobe Experience Platform可以从外部源收集数据，同时允许您使用[!DNL Platform]服务来构建、标记和增强该数据。 您可以从各种来源(如Adobe应用程序、基于云的存储、第三方软件和您的CRM系统)收集数据。

[!DNL Experience Platform] 提供REST风格的API和交互式UI，让您可以轻松为各种数据提供者设置源连接。这些源连接允许您验证并连接到外部存储系统和CRM服务，设置获取运行的时间，以及管理数据获取吞吐量。

**新增功能**

| 功能 | 描述 |
| ------- | ----------- |
| 流运行监控 | 用户可以监视所有流运行并查看每个运行的详细视图，包括完成状态、运行持续时间、已处理文件的列表、错误和度量。 有关详细信息，请参阅[监视数据流](../../sources/tutorials/ui/monitor.md)文档。 |
| 流运行通知 | 用户可以订阅事件并注册网络挂接，以接收有关流运行的状态、度量和错误的实时通知。 |
| UI目录改进 | 对源目录屏幕进行更新，以便更轻松地访问选定对象的主要操作。 |

要进一步了解源，请参阅[源概述](../../sources/home.md)。