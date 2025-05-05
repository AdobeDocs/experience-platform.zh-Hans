---
title: 根据LiveRamp标识符将受众激活到策划的目标
type: Tutorial
description: 了解如何使用LiveRamp RampID将受众从Adobe Experience Platform激活到连接的电视和音频目标以及其他集成。
exl-id: 37e5bab9-588f-40b3-b65b-68f1a4b868f1
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '662'
ht-degree: 0%

---

# 根据LiveRamp标识符将受众激活到策划的目标

使用与[!DNL LiveRamp]的Adobe Real-Time CDP集成将受众激活到使用[[!DNL [LiveRamp RampID]]](https://docs.liveramp.com/connect/en/interpreting-rampid,-liveramp-s-people-based-identifier.html)进行激活的策划的目标列表，包括连接的电视和音频目标，如下面列出的目标。

>[!IMPORTANT]
>
>您无需在Experience Platform界面中摄取或以任何方式使用LiveRamp RampID。
>
> 您可以从Real-Time CDP导出身份，如基于PII的标识符、已知标识符和自定义ID，如官方[LiveRamp文档](https://docs.liveramp.com/connect/en/identity-and-identifier-terms-and-concepts.html#known-identifiers)中所述。 然后，这些标识与激活过程中下游的[!DNL LiveRamp RampIDs]匹配。


* [[!DNL 4C Insights]](#insights)
* [[!DNL Acast]](#acast)
* [[!DNL Ampersand.tv]](#ampersand-tv)
* [[!DNL Captify]](#captify)
* [[!DNL Cardlytics]](#cardlytics)
* [[!DNL Disney (Hulu/ESPN/ABC)]](#disney)
* [[!DNL iHeartMedia]](#iheartmedia)
* [[!DNL Index Exchange]](#index-exchange)
* [[!DNL Magnite CTV Platform]](#magnite)
* [[!DNL Magnite DV+ (Rubicon Project)]](#magnite-dv)
* [[!DNL Nexxen]](#nexxen)
* [[!DNL One Fox]](#fox)
* [[!DNL Pandora]](#pandora)
* [[!DNL Reddit]](#reddit)
* [[!DNL Roku]](#roku)
* [[!DNL Spotify]](#spotify)
* [[!DNL Taboola]](#taboola)
* [[!DNL TargetSpot]](#targetspot)
* [[!DNL Teads]](#teads)
* [[!DNL WB Discovery]](#wb-discovery)

本文介绍了直接从Real-Time CDP UI将受众从Real-Time CDP激活到上面列出的目标所需的工作流。

## 激活工作流 {#workflow}

您可以通过两个步骤的流程，并使用[LiveRamp — 入门](../catalog/advertising/liveramp-onboarding.md)和[LiveRamp — 分发](../catalog/advertising/liveramp-distribution.md)目标，将受众激活到连接的电视和音频目标，如下图所示。

![显示通过LiveRamp将受众从Real-Time CDP激活到策划目标的工作流的图表。](../assets/ui/activate-curated-destinations-liveramp/workflow-diagram.png){width="1920" zoomable="yes"}

首先，将受众以CSV文件形式从Real-Time CDP导出到[[!DNL LiveRamp - Onboarding]](../catalog/advertising/liveramp-onboarding.md)目标。

导出受众后，可使用[[!DNL LiveRamp - Distribution]](../catalog/advertising/liveramp-distribution.md)目标激活它们。

>[!TIP]
>
>通过此流程，您可以直接从Real-Time CDP UI将受众激活到目标，例如[[!DNL Roku]](../catalog/advertising/liveramp-distribution.md#roku)、[[!DNL Disney]](../catalog/advertising/liveramp-distribution.md#disney)等，而无需登录到您的[!DNL LiveRamp]帐户进行激活。

### 视频教程 {#video}

观看以下视频，了解此页面中描述的工作流的端到端说明。

>[!VIDEO](https://video.tv.adobe.com/v/3425367)

### 步骤1：通过[!DNL LiveRamp - Onboarding]目标将受众从Experience Platform发送到LiveRamp {#onboarding}

要将受众激活到基于LiveRamp RampIDs的策划目标，您必须执行的第一个操作是&#x200B;**将受众从Experience Platform导出到[!DNL LiveRamp]**。

可使用&#x200B;**[!DNL LiveRamp - Onboarding]**&#x200B;目标执行此操作。

![显示LiveRamp — 登录目标卡的Experience Platform UI图像](../assets/ui/activate-curated-destinations-liveramp/liveramp-onboarding-catalog.png)

要了解如何配置[!DNL LiveRamp - Onboarding]目标并从Experience Platform导出受众，请阅读[[!DNL LiveRamp - Onboarding]](../catalog/advertising/liveramp-onboarding.md)目标文档。

>[!IMPORTANT]
>
>将文件导出到[!DNL LiveRamp - Onboarding]目标时，Experience Platform为每个[合并策略ID](../../profile/merge-policies/overview.md)生成一个CSV文件。 有关如何验证数据导出到LiveRamp的详细信息，请参阅[[!DNL LiveRamp - Onboarding]](../catalog/advertising/liveramp-onboarding.md)目标文档。


成功将受众导出到LiveRamp后，请继续[步骤2](#distribution)。

>[!TIP]
>
>在迁移到[步骤2](#distribution)之前，[验证](../catalog/advertising/liveramp-onboarding.md#exported-data)您的受众已成功导出到LiveRamp。 请参阅有关[监视目标数据流](../../dataflows/ui/monitor-destinations.md#dataflow-runs-for-batch-destinations)的文档并阅读[[!DNL LiveRamp - Onboarding]](../catalog/advertising/liveramp-onboarding.md#exported-data)的特定监视详细信息。

### 步骤2：通过[!DNL LiveRamp - Distribution]目标将已载入受众激活到连接的电视和音频目标 {#distribution}

在您[验证](../catalog/advertising/liveramp-onboarding.md#exported-data)您的受众已成功导出到LiveRamp之后，就可以将受众激活到您的首选目标，如[[!DNL Roku]](../catalog/advertising/liveramp-distribution.md#roku)、[[!DNL Disney]](../catalog/advertising/liveramp-distribution.md#disney)等。

使用&#x200B;**[!DNL LiveRamp - Distribution]**&#x200B;目标激活受众（在[步骤1](#onboarding)中导出）。

显示LiveRamp — 分发目标卡的![Experience Platform UI图像](../assets/ui/activate-curated-destinations-liveramp/liveramp-distribution-catalog.png)

要了解如何配置&#x200B;**[!DNL LiveRamp - Distribution]**&#x200B;目标并激活您在[步骤1](#onboarding)中导出的受众，请阅读[[!DNL LiveRamp - Distribution]](../catalog/advertising/liveramp-distribution.md)目标文档。

>[!IMPORTANT]
>
>在&#x200B;**[!DNL LiveRamp - Distribution]**&#x200B;目标的&#x200B;**受众选择**&#x200B;步骤中，您必须在[步骤1](#onboarding)中选择已导出到[LiveRamp — 载入](../catalog/advertising/liveramp-onboarding.md)目标的&#x200B;*完全相同的受众*。

在配置&#x200B;**[!DNL LiveRamp - Distribution]**&#x200B;目标时，必须为要使用的每个下游目标（Roku、Disney等）创建专用连接。

>[!TIP]
>
>在命名目标时，Adobe建议遵循以下格式： `LiveRamp - Downstream Destination Name`。 此命名模式可帮助您在目标工作区的[浏览](../ui/destinations-workspace.md#browse)选项卡中快速识别目标。
><br>
>示例：`LiveRamp - Roku`。

![Experience Platform UI屏幕截图显示多个LiveRamp目标。](../assets/ui/activate-curated-destinations-liveramp/liveramp-naming.png)

## 导出的数据/验证数据导出 {#exported-data}

要验证如何将受众成功导出到[[!DNL LiveRamp - Onboarding]](../catalog/advertising/liveramp-onboarding.md)目标，请参阅有关[监视目标数据流](../../dataflows/ui/monitor-destinations.md#dataflow-runs-for-batch-destinations)的文档并阅读[[!DNL LiveRamp - Onboarding]](../catalog/advertising/liveramp-onboarding.md#exported-data)的特定监视详细信息。

要验证受众是否成功激活到您选择的广告平台（例如Roku、Disney等），请登录到您的目标平台帐户并检查激活量度。
