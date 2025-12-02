---
title: 将帐户受众激活到目标
type: Tutorial
description: 了解如何将帐户受众激活到目标
badgeB2B: label="B2B edition" type="Informative" url=" https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=en#rtcdp-editions newtab=true"
badgeB2P: label="B2P版本" type="Positive" url=" https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=en#rtcdp-editions newtab=true"
exl-id: ad69d0a8-bf5b-42ac-97a3-401eadda62cd
source-git-commit: 9f4ce2a3a8af72342683c859caa270662b161b7d
workflow-type: tm+mt
source-wordcount: '782'
ht-degree: 0%

---

# 激活帐户受众

>[!AVAILABILITY]
>
>向目标激活帐户受众的功能适用于购买[企业对企业](/help/rtcdp/overview.md#rtcdp-b2b)和[企业对个人](/help/rtcdp/overview.md#rtcdp-b2p)版本的Real-Time Customer Data Platform的公司。

本文介绍了将[帐户受众](/help/segmentation/types/account-audiences.md)从Adobe Experience Platform导出到您的首选目标所需的工作流。

## 支持的目标 {#supported-destinations}

转到&#x200B;**[!UICONTROL Connections]** > **[!UICONTROL Destinations]**，然后选择&#x200B;**[!UICONTROL Catalog]**&#x200B;选项卡。 使用&#x200B;**[!UICONTROL Data types]**&#x200B;筛选器并选择&#x200B;**[!UICONTROL Accounts]**&#x200B;查看支持激活帐户受众的目标。 目前，导出帐户受众仅适用于某些云存储目标([Amazon S3](/help/destinations/catalog/cloud-storage/amazon-s3.md)、[ADLS Gen 2](/help/destinations/catalog/cloud-storage/adls-gen2.md)、[Azure Blob Storage](/help/destinations/catalog/cloud-storage/azure-blob.md)、[数据登陆区域](/help/destinations/catalog/cloud-storage/data-landing-zone.md)和[SFTP](/help/destinations/catalog/cloud-storage/sftp.md))以及[Demandbase](/help/destinations/catalog/advertising/demandbase.md)和[（公司）LinkedIn匹配的受众](/help/destinations/catalog/social/linkedin-b2b.md)流目标。

![支持帐户受众的目标。](/help/destinations/assets/ui/activate-account-audiences/data-types-filter.png)

## 视频概述

请观看以下视频，大致了解如何创建和激活帐户受众，以及激活帐户受众时支持的用例。

>[!VIDEO](https://video.tv.adobe.com/v/338252/?learn=on)

## 先决条件 {#prerequisites}

* 必须先摄取[帐户配置文件](/help/rtcdp/accounts/account-profile-overview.md)并创建[帐户受众](/help/segmentation/types/account-audiences.md)，然后才能将其激活到下游目标。
* 要将帐户受众激活到目标，您必须已成功连接到目标。 如果您尚未这样做，请转到[目标目录](../catalog/overview.md)，浏览支持的目标，然后配置要使用的目标。 有关详细信息，请阅读有关[连接到目标](./connect-destination.md)的用户界面教程。

### 所需的权限 {#permissions}

要激活帐户受众，您需要&#x200B;**[!UICONTROL View Destinations]**&#x200B;和&#x200B;**[!UICONTROL Activate Destinations]** [访问控制权限](/help/access-control/home.md#permissions)。 阅读[访问控制概述](/help/access-control/ui/overview.md)或联系您的产品管理员以获取所需的权限。

要确保您具有激活帐户受众的必要权限，请浏览目标目录。 如果目标具有&#x200B;**[!UICONTROL Activate]**&#x200B;控件，则您具有相应的权限。

## 选择您的目标 {#select-destination}

按照相关说明选择一个可导出数据集的目标：

1. 转到&#x200B;**[!UICONTROL Connections > Destinations]**，然后选择&#x200B;**[!UICONTROL Catalog]**&#x200B;选项卡。

   ![目录控件突出显示的目标目录选项卡。](/help/destinations/assets/ui/export-datasets/catalog-tab.png)

1. 在与要将数据集导出到的目标对应的卡片中选择&#x200B;**[!UICONTROL Activate]**。

>[!TIP]
>
>可导出帐户受众的目标在卡片的右上角以图标指示，类似于下面高亮显示的目标，或者，您可以使用数据类型筛选器以仅显示可导出帐户受众的目标，如页面上较高位置显示的[&#128279;](#supported-destinations)。

![可导出突出显示的配置文件受众的Demandbase目标页面。](/help/destinations/assets/ui/activate-account-audiences/demandbase-icon-activate-account-audiences.png)

1. 选择&#x200B;**[!UICONTROL Data type Accounts]**，然后选择要将数据集导出到的目标连接，然后选择&#x200B;**[!UICONTROL Next]**。

>[!TIP]
> 
>如果要设置新目标以激活帐户受众，请选择&#x200B;**[!UICONTROL Configure new destination]**&#x200B;以触发[连接到目标](/help/destinations/ui/connect-destination.md)工作流，并[选择帐户作为数据类型](/help/destinations/ui/connect-destination.md#segment-activation-or-dataset-exports)。

![帐户控件突出显示的目标激活工作流。](/help/destinations/assets/ui/activate-account-audiences/activate-account-audiences-highlighted.png)

1. 继续到[选择帐户受众](#select-profile-audiences)以导出的下一部分。

## 选择您的帐户受众 {#select-account-audiences}

使用帐户受众名称左侧的复选框选择要导出到目标的受众，然后选择&#x200B;**[!UICONTROL Next]**。 请注意，此视图中只显示&#x200B;*帐户受众*，不显示其他受众类型。

![数据集导出工作流显示“选择受众”步骤，您可以在该步骤中选择要导出的帐户受众。](/help/destinations/assets/ui/activate-account-audiences/select-account-audiences.png)

## 计划和后续步骤

有关导入帐户受众的其余激活工作流，请阅读有关将数据激活到基于文件的目标的教程。 从[计划受众导出步骤](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling)继续。 如果要将帐户受众激活到&#x200B;**[!UICONTROL (Companies) LinkedIn Matched Audiences]**&#x200B;目标，请阅读有关激活流目标的教程。 从[映射步骤](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping)继续。

>[!NOTE]
>
>请注意，在将帐户受众导出到云存储目标时的计划步骤中，激活帐户受众的工作流仅允许您按每日计划导出[完整文件](/help/destinations/ui/activate-batch-profile-destinations.md#export-full-files)和[增量文件](/help/destinations/ui/activate-batch-profile-destinations.md#export-incremental-files) _。_&#x200B;不支持每小时导出。 另请注意，**[!UICONTROL After audience evaluation]**&#x200B;是唯一受支持的评估类型。

## 重要标头和已知限制 {#important-callouts-known-limitations}

请注意激活帐户受众功能的正式发布中的以下重要说明和已知限制。

### 将帐户受众激活到&#x200B;**[!UICONTROL (Companies) LinkedIn Matched Audiences]**&#x200B;目标时，映射步骤中需要映射对 {#required-mappings}

将帐户受众激活到&#x200B;**[!UICONTROL (Companies) LinkedIn Matched Audiences]**&#x200B;目标时，请注意，以下两个映射对是成功导出数据所必需的：

![LinkedIn映射必填字段。](/help/destinations/assets/ui/activate-account-audiences/linkedin-mapping-required-fields.png)

| 源字段 | 目标字段 |
|---------|----------|
| `accountName` | `companyName` |
| `accountKey.sourceKey` | `primaryId` （选择&#x200B;**[!UICONTROL Select Identity namespace]**&#x200B;时，在&#x200B;**[!UICONTROL Target Field]**&#x200B;视图中选择此字段）。<br> ![选择工作流中突出显示的身份命名空间以将帐户受众激活到目标。](/help/destinations/assets/ui/activate-account-audiences/identity-namespace-highlighted.png "选择工作流中突出显示的身份命名空间以将帐户受众激活到目标。"){width="100" zoomable="yes"} |

### 数据治理实施 {#data-governance-enforcement}

在&#x200B;*客户和潜在客户受众*&#x200B;的人员或个人资料级别强制同意。 因此，将帐户受众激活到目标时，当前不支持[同意策略评估](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation)。 在激活工作流的审核步骤中，您可以看到&#x200B;**[!UICONTROL View applicable consent policies]**&#x200B;的控件呈灰显状态。

![激活帐户受众工作流的审核步骤，同意强制控制呈灰显状态。](/help/destinations/assets/ui/activate-account-audiences/consent-checks-greyed-out.png)

支持Real-Time CDP中的其他数据治理机制，如[数据使用策略检查](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation)和[基于属性的访问控制](/help/destinations/home.md#attribute-based-access)。
