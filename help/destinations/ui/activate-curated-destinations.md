---
title: 根据LiveRamp标识符将受众激活到策划的目标
type: Tutorial
description: 了解如何使用LiveRamp RampID将受众从Adobe Experience Platform激活到连接的电视和音频目标以及其他集成。
source-git-commit: 1eb422572d95426fa8b342dc6aa79fb6125e18a1
workflow-type: tm+mt
source-wordcount: '663'
ht-degree: 0%

---


# 根据LiveRamp标识符将受众激活到策划的目标

将Adobe Real-Time CDP集成用于 [!DNL LiveRamp] 将受众激活到使用的策划的目标列表 [!DNL [LiveRamp RampID]](https://docs.liveramp.com/connect/en/interpreting-rampid,-liveramp-s-people-based-identifier.html) 激活，包括连接的电视和音频目标，如下面列出的目标。

>[!IMPORTANT]
>
>您无需在Experience Platform界面中摄取或以任何方式使用LiveRamp RampID。
>
> 您可以从Real-Time CDP导出身份，例如基于PII的标识符、已知标识符和自定义ID，如官方网站所述 [LiveRamp文档](https://docs.liveramp.com/connect/en/identity-and-identifier-terms-and-concepts.html#known-identifiers). 随后，这些身份将与 [!DNL LiveRamp RampIDs] 在激活过程的下游更进一步。


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

您可以通过两个步骤的过程并使用，将受众激活到连接的电视和音频目标。 [LiveRamp — 入门](../catalog/advertising/liveramp-onboarding.md) 和 [LiveRamp — 分发](../catalog/advertising/liveramp-distribution.md) 目标，如下图所示。

![此图显示了通过LiveRamp将受众从Real-Time CDP激活到策划目标的工作流。](../assets/ui/activate-curated-destinations-liveramp/workflow-diagram.png){width="1920" zoomable="yes"}

首先，将受众从Real-Time CDP导出到 [[!DNL LiveRamp - Onboarding]](../catalog/advertising/liveramp-onboarding.md) 目标，作为CSV文件。

导出受众后，可通过使用 [[!DNL LiveRamp - Distribution]](../catalog/advertising/liveramp-distribution.md) 目标。

>[!TIP]
>
>通过此流程，您可以将受众激活到目标，例如 [[!DNL Roku]](../catalog/advertising/liveramp-distribution.md#roku)， [[!DNL Disney]](../catalog/advertising/liveramp-distribution.md#disney)Real-Time CDP 、等，无需登录到 [!DNL LiveRamp] 帐户激活。

### 视频教程 {#video}

观看以下视频，了解此页面中描述的工作流的端到端说明。

>[!VIDEO](https://video.tv.adobe.com/v/3425367)

### 步骤1：通过，将受众从Experience Platform发送到LiveRamp [!DNL LiveRamp - Onboarding] 目标 {#onboarding}

要将受众激活到基于LiveRamp RampIDs的策划目标，您必须执行的第一个操作是 **将受众从Experience Platform导出到[!DNL LiveRamp]**.

为此，请使用 **[!DNL LiveRamp - Onboarding]** 目标。

![显示LiveRamp — 载入目标卡的Experience PlatformUI图像](../assets/ui/activate-curated-destinations-liveramp/liveramp-onboarding-catalog.png)

要了解如何配置 [!DNL LiveRamp - Onboarding] 从Experience Platform中导出受众，请阅读 [[!DNL LiveRamp - Onboarding]](../catalog/advertising/liveramp-onboarding.md) 目标文档。

>[!IMPORTANT]
>
>将文件导出到 [!DNL LiveRamp - Onboarding] 目标，平台为每个目标生成一个CSV文件 [合并策略Id](../../profile/merge-policies/overview.md). 请参阅 [[!DNL LiveRamp - Onboarding]](../catalog/advertising/liveramp-onboarding.md) 目标文档，以了解有关如何验证数据导出到LiveRamp的详细信息。


成功将受众导出到LiveRamp后，请继续 [步骤2](#distribution).

>[!TIP]
>
>迁移至之前 [步骤2](#distribution)， [验证](../catalog/advertising/liveramp-onboarding.md#exported-data) 受众已成功导出到LiveRamp。 请参阅相关文档 [监视目标数据流](../../dataflows/ui/monitor-destinations.md#dataflow-runs-for-batch-destinations) 并阅读特定的监控详细信息 [[!DNL LiveRamp - Onboarding]](../catalog/advertising/liveramp-onboarding.md#exported-data).

### 步骤2：通过，将已载入的受众激活到连接的电视和音频目标。 [!DNL LiveRamp - Distribution] 目标 {#distribution}

在您拥有 [已验证](../catalog/advertising/liveramp-onboarding.md#exported-data) 您的受众已成功导出到LiveRamp，现在就可以将受众激活到您的首选目标了，例如 [[!DNL Roku]](../catalog/advertising/liveramp-distribution.md#roku)， [[!DNL Disney]](../catalog/advertising/liveramp-distribution.md#disney)，等等。

您可以激活受众（在中导出） [步骤1](#onboarding))，通过使用 **[!DNL LiveRamp - Distribution]** 目标。

![显示LiveRamp — 分发目标卡的Experience PlatformUI图像](../assets/ui/activate-curated-destinations-liveramp/liveramp-distribution-catalog.png)

要了解如何配置 **[!DNL LiveRamp - Distribution]** 目标并激活您在中导出的受众 [步骤1](#onboarding)，阅读 [[!DNL LiveRamp - Distribution]](../catalog/advertising/liveramp-distribution.md) 目标文档。

>[!IMPORTANT]
>
>在 **受众选择** 步骤 **[!DNL LiveRamp - Distribution]** 目标，您必须选择 *完全相同的受众* ，您已将其导出到 [LiveRamp — 入门](../catalog/advertising/liveramp-onboarding.md) 目标位置 [步骤1](#onboarding).

当您配置 **[!DNL LiveRamp - Distribution]** 目标，您必须为要使用的每个下游目标（Roku、Disney等）创建专用连接。

>[!TIP]
>
>在命名目标时，Adobe建议遵循以下格式： `LiveRamp - Downstream Destination Name`. 此命名模式可帮助您快速识别 [浏览](../ui/destinations-workspace.md#browse) 目标工作区的选项卡。
><br>
>示例：`LiveRamp - Roku`。

![显示多个LiveRamp目标的平台UI屏幕截图。](../assets/ui/activate-curated-destinations-liveramp/liveramp-naming.png)

## 导出的数据/验证数据导出 {#exported-data}

验证受众是否成功导出到 [[!DNL LiveRamp - Onboarding]](../catalog/advertising/liveramp-onboarding.md) 目标，请参阅以下文档： [监视目标数据流](../../dataflows/ui/monitor-destinations.md#dataflow-runs-for-batch-destinations) 并阅读特定的监控详细信息 [[!DNL LiveRamp - Onboarding]](../catalog/advertising/liveramp-onboarding.md#exported-data).

要验证受众是否成功激活到您选择的广告平台（例如Roku、Disney等），请登录到您的目标平台帐户并检查激活量度。
