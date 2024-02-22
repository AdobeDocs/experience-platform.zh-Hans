---
title: 将帐户受众激活到目标
type: Tutorial
description: 了解如何将帐户受众激活到目标
badgeB2B: label="B2B版本" type="Informative" url=" https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=en#rtcdp-editions newtab=true"
badgeB2P: label="B2P版本" type="Positive" url=" https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=en#rtcdp-editions newtab=true"
exl-id: ad69d0a8-bf5b-42ac-97a3-401eadda62cd
source-git-commit: 3c0b7c4eee7c790a8ffae95c05a8db6ba7c3b285
workflow-type: tm+mt
source-wordcount: '810'
ht-degree: 0%

---

# 激活帐户受众

>[!AVAILABILITY]
>
>公司可以使用此功能将帐户受众激活到目标。 [企业对企业](/help/rtcdp/overview.md#rtcdp-b2b) 和 [企业对个人](/help/rtcdp/overview.md#rtcdp-b2p) Real-time Customer Data Platform各版。

本文介绍了导出所需的工作流 [帐户受众](/help/segmentation/ui/account-audiences.md) 从Adobe Experience Platform到您的首选目标。

## 支持的目标 {#supported-destinations}

转到 **[!UICONTROL 连接]** > **[!UICONTROL 目标]**，然后选择 **[!UICONTROL 目录]** 选项卡。 使用 **[!UICONTROL 数据类型]** 筛选并选择 **[!UICONTROL 帐户]** 查看支持激活帐户受众的目标。 目前，导出帐户受众仅适用于某些云存储目标([Amazon S3](/help/destinations/catalog/cloud-storage/amazon-s3.md)， [ADLS Gen 2](/help/destinations/catalog/cloud-storage/adls-gen2.md)， [Azure Blob存储](/help/destinations/catalog/cloud-storage/azure-blob.md)， [数据登陆区](/help/destinations/catalog/cloud-storage/data-landing-zone.md)、和 [SFTP](/help/destinations/catalog/cloud-storage/sftp.md))和 [（公司） LinkedIn匹配的受众](/help/destinations/catalog/social/linkedin.md) 目标。

![支持帐户受众的目标。](/help/destinations/assets/ui/activate-account-audiences/data-types-filter.png)

## 先决条件 {#prerequisites}

* 您必须先摄取 [帐户配置文件](/help/rtcdp/accounts/account-profile-overview.md) 和创建 [帐户受众](/help/segmentation/ui/account-audiences.md) 才能将其激活到下游目标。
* 要将帐户受众激活到目标，您必须已成功连接到目标。 如果您尚未这样做，请转到 [目标目录](../catalog/overview.md)，浏览支持的目标，并配置要使用的目标。 阅读有关的UI教程 [连接到目标](./connect-destination.md) 以了解更多信息。

### 所需权限 {#permissions}

要激活帐户受众，您需要 **[!UICONTROL 查看目标]** 和 **[!UICONTROL 激活目标]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或与产品管理员联系以获取所需的权限。

要确保您具有激活帐户受众的必要权限，请浏览目标目录。 如果目标具有 **[!UICONTROL 激活]** 则您具有相应的权限。

## 选择您的目标 {#select-destination}

按照相关说明选择一个可导出数据集的目标：

1. 转到 **[!UICONTROL “连接”>“目标”]**，然后选择 **[!UICONTROL 目录]** 选项卡。

   ![突出显示目录控件的目标目录选项卡。](/help/destinations/assets/ui/export-datasets/catalog-tab.png)

1. 选择 **[!UICONTROL 激活]** 在与要将数据集导出到的目标对应的卡上。

>[!TIP]
>
>可导出帐户受众的目标在卡片的右上角有一个图标来指示，类似于下面高亮显示的目标，或者，您可以使用数据类型过滤器仅显示可导出帐户受众的目标，如 [显示在页面上的较高位置](#supported-destinations).

![可导出突出显示的配置文件受众的Amazon S3目标页面。](/help/destinations/assets/ui/activate-account-audiences/amazon-s3-icon-activate-account-audiences.png)

1. 选择 **[!UICONTROL 数据类型帐户]**，然后选择要将数据集导出到的目标连接，然后选择 **[!UICONTROL 下一个]**.

>[!TIP]
> 
>如果要设置新目标以激活帐户受众，请选择 **[!UICONTROL 配置新目标]** 以触发 [连接到目标](/help/destinations/ui/connect-destination.md) 工作流和 [选择帐户作为数据类型](/help/destinations/ui/connect-destination.md#segment-activation-or-dataset-exports).

![突出显示帐户控制的目标激活工作流。](/help/destinations/assets/ui/activate-account-audiences/activate-account-audiences-highlighted.png)

1. 继续下一节以 [选择您的帐户受众](#select-profile-audiences) 以导出。

## 选择您的帐户受众 {#select-account-audiences}

使用帐户受众名称左侧的复选框选择要导出到目标的受众，然后选择 **[!UICONTROL 下一个]**. 请注意，仅 *帐户受众* 将显示在此视图中，但不显示其他受众类型。

![数据集导出工作流显示了选择受众步骤，您可以在其中选择要导出的帐户受众。](/help/destinations/assets/ui/activate-account-audiences/select-account-audiences.png)

## 计划和后续步骤

有关导入帐户受众的其余激活工作流，请阅读有关将数据激活到基于文件的目标的教程。 继续从 [计划受众导出步骤](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling). 如果您要将帐户受众激活到 **[!UICONTROL （公司） LinkedIn匹配的受众]** 目标，请阅读有关激活流目标的教程。 继续从 [映射步骤](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping).

>[!NOTE]
>
>请注意，在将帐户受众导出到云存储目标时的计划步骤中，激活帐户受众的工作流仅允许您导出 [完整文件](/help/destinations/ui/activate-batch-profile-destinations.md#export-full-files) 和 [增量文件](/help/destinations/ui/activate-batch-profile-destinations.md#export-incremental-files) _按每日计划_. 不支持每小时导出。 另请注意 **[!UICONTROL 受众评估后]** 是唯一支持的评估类型。

## 重要标头和已知限制 {#important-callouts-known-limitations}

请注意激活帐户受众功能的正式发布中的以下重要说明和已知限制。

### 将帐户受众激活到时，映射步骤中所需的映射对 **[!UICONTROL （公司） LinkedIn匹配的受众]** 目标 {#required-mappings}

将帐户受众激活到时 **[!UICONTROL （公司） LinkedIn匹配的受众]** 请注意，要成功导出数据，必须具有以下两个映射对：

![linkedIn映射必填字段。](/help/destinations/assets/ui/activate-account-audiences/linkedin-mapping-required-fields.png)

| 源字段 | 目标字段 |
|---------|----------|
| `accountName` | `companyName` |
| `accountKey.sourceKey` | `primaryId` (在 **[!UICONTROL 选择身份命名空间]** 视图，当选择 **[!UICONTROL 目标字段]**)。 <br> ![选择工作流中突出显示的身份命名空间以将帐户受众激活到目标。](/help/destinations/assets/ui/activate-account-audiences/identity-namespace-highlighted.png "选择工作流中突出显示的身份命名空间以将帐户受众激活到目标。"){width="100" zoomable="yes"} |

### 数据治理实施 {#data-governance-enforcement}

在人员或个人资料级别强制同意 *客户和潜在客户受众*. 因此，  [同意政策评估](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) 当前不支持将帐户受众激活到目标。 在激活工作流的审核步骤中，您可以看到的控件显示为灰色 **[!UICONTROL 查看适用的同意政策]**.

![激活帐户受众工作流的审核步骤，同意实施控制呈灰显状态。](/help/destinations/assets/ui/activate-account-audiences/consent-checks-greyed-out.png)

Real-Time CDP中的其他数据治理机制，例如 [数据使用策略检查](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) 和 [基于属性的访问控制](/help/destinations/home.md#attribute-based-access) 受支持。
