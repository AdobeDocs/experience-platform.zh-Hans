---
title: 将受众激活到流配置文件导出目标
type: Tutorial
description: 了解如何通过将受众发送到基于个人资料的流目标来激活您在Adobe Experience Platform中的受众数据。
badgeUltimate: label="Ultimate" type="Positive"
exl-id: bc0f781e-60de-44a5-93cb-06b4a3148591
source-git-commit: 99bac2ea71003b678a25b3afc10a68d36472bfbc
workflow-type: tm+mt
source-wordcount: '762'
ht-degree: 1%

---


# 将受众激活到流配置文件导出目标

>[!IMPORTANT]
> 
> * 要激活数据并启用工作流的[映射步骤](#mapping)，您需要&#x200B;**[!UICONTROL View Destinations]**、**[!UICONTROL Activate Destinations]**、**[!UICONTROL View Profiles]**&#x200B;和&#x200B;**[!UICONTROL View Segments]** [访问控制权限](/help/access-control/home.md#permissions)。
> * 若要在不执行工作流的[映射步骤](#mapping)的情况下激活数据，您需要&#x200B;**[!UICONTROL View Destinations]**、**[!UICONTROL Activate Segment without Mapping]**、**[!UICONTROL View Profiles]**&#x200B;和&#x200B;**[!UICONTROL View Segments]** [访问控制权限](/help/access-control/home.md#permissions)。
> 
> 阅读[访问控制概述](/help/access-control/ui/overview.md)或联系您的产品管理员以获取所需的权限。

## 概述 {#overview}

本文介绍了在Adobe Experience Platform中将受众数据激活到基于配置文件的流式目标（也称为[企业目标](/help/destinations/destination-types.md#advanced-enterprise-destinations)）所需的工作流。

本文适用于以下三个目标：

* [Amazon Kinesis](/help/destinations/catalog/cloud-storage/amazon-kinesis.md)
* [Azure 事件中心](/help/destinations/catalog/cloud-storage/azure-event-hubs.md)
* [HTTP API目标](/help/destinations/catalog/streaming/http-destination.md)。

## 先决条件 {#prerequisites}

若要将数据激活到目标，您必须已成功[连接到目标](./connect-destination.md)。 如果您尚未这样做，请转到[目标目录](../catalog/overview.md)，浏览支持的目标，然后配置要使用的目标。

## 选择您的目标 {#select-destination}

1. 转到&#x200B;**[!UICONTROL Connections > Destinations]**，然后选择&#x200B;**[!UICONTROL Catalog]**&#x200B;选项卡。

   ![显示目标目录选项卡的图像。](../assets/ui/activate-streaming-profile-destinations/catalog-tab.png)

1. 在与您要激活受众的目标对应的卡片中选择&#x200B;**[!UICONTROL Activate audiences]**，如下图所示。

   ![在目标目录选项卡中突出显示“激活受众”控件的图像。](../assets/ui/activate-streaming-profile-destinations/activate-audiences-button.png)

1. 选择要用于激活受众的目标连接，然后选择&#x200B;**[!UICONTROL Next]**。

   ![显示所选两个目标的图像，您可以连接到这些目标。](../assets/ui/activate-streaming-profile-destinations/select-destination.png)

1. 移到下一部分以[选择您的受众](#select-audiences)。

## 选择您的受众 {#select-audiences}

要选择要激活到目标的受众，请使用受众名称左侧的复选框，然后选择&#x200B;**[!UICONTROL Next]**。

您可以从多种类型的受众中进行选择，具体取决于其来源：

* **[!UICONTROL Segmentation Service]**：分段服务在Experience Platform中生成的受众。 有关更多详细信息，请参阅[受众门户文档](../../segmentation/ui/audience-portal.md)。
* **[!UICONTROL Custom upload]**：受众在Experience Platform之外生成，并以CSV文件形式上传到Experience Platform。 要了解有关外部受众的更多信息，请参阅有关[导入受众](../../segmentation/ui/audience-portal.md#import-audience)的文档。
* 其他类型的受众，来自其他Adobe解决方案，如[!DNL Audience Manager]。

![在激活工作流的“选择受众”步骤中，突出显示复选框选择的图像。](../assets/ui/activate-streaming-profile-destinations/select-audiences.png)

## 选择配置文件属性 {#select-attributes}

在&#x200B;**[!UICONTROL Mapping]**&#x200B;步骤中，选择要发送到目标目标的配置文件属性。

1. 在&#x200B;**[!UICONTROL Select attributes]**&#x200B;页面中，选择&#x200B;**[!UICONTROL Add new field]**。

   ![在映射步骤中突出显示“添加新字段控件”的图像。](../assets/ui/activate-streaming-profile-destinations/add-new-field.png)

1. 选择&#x200B;**[!UICONTROL Schema field]**&#x200B;条目右侧的箭头。

   ![突出显示映射步骤中如何选择源字段的图像。](../assets/ui/activate-streaming-profile-destinations/select-schema-field.png)

1. 在&#x200B;**[!UICONTROL Select source field]**&#x200B;页面中，选择要发送到目标的XDM属性，然后选择&#x200B;**[!UICONTROL Save]**。

   ![该图像显示了一组您可以选择作为源字段的XDM字段。](../assets/ui/activate-streaming-profile-destinations/select-source-field-modal.png)

   使用&#x200B;**[!UICONTROL Show only fields with data]**&#x200B;切换可仅显示用值填充的架构字段。 默认情况下，仅显示填充的架构字段。

   使用&#x200B;**[!UICONTROL Show display names for fields]**&#x200B;切换显示字段的友好名称，而不是架构字段名称。

   ![显示显示显示名称切换的源字段页。](../assets/ui/activate-batch-profile-destinations/show-display-names.gif)

1. 要添加更多字段，请重复步骤1至3，然后选择&#x200B;**[!UICONTROL Next]**。

## 审阅 {#review}

在&#x200B;**[!UICONTROL Review]**&#x200B;页面上，您可以看到所选内容的摘要。 选择&#x200B;**[!UICONTROL Cancel]**&#x200B;以中断流，**[!UICONTROL Back]**&#x200B;以修改您的设置，或&#x200B;**[!UICONTROL Finish]**&#x200B;以确认您的选择并开始将数据发送到目标。

![审核步骤中的选择摘要。](../assets/ui/activate-streaming-profile-destinations/review.png)

### 同意策略评估 {#consent-policy-evaluation}

向三个企业目标(Amazon Kinesis、Azure事件中心和HTTP API)的导出当前不支持同意策略评估[。](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation)

这意味着未同意成为目标&#x200B;*的用户档案包括在导出到这三个目标的*&#x200B;中。

<!--

If your organization purchased **Adobe Healthcare Shield** or **Adobe Privacy & Security Shield**, select **[!UICONTROL View applicable consent policies]** to see which consent policies are applied and how many profiles are included in the activation as a result of them. Read about [consent policy evaluation](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) for more information.

-->

### 数据使用策略检查 {#data-usage-policy-checks}

在&#x200B;**[!UICONTROL Review]**&#x200B;步骤中，Experience Platform还会检查是否存在任何数据使用策略违规。 下面显示了一个违反策略的示例。 在解决该违规之前，您无法完成受众激活工作流。 有关如何解决策略违规的信息，请参阅数据治理文档部分中的[数据使用策略违规](/help/data-governance/enforcement/auto-enforcement.md#data-usage-violation)。

![数据策略违规](../assets/common/data-policy-violation.png)

### 筛选受众 {#filter-audiences}

此外，在此步骤中，您可以使用页面上的可用过滤器仅显示其计划或映射作为此工作流的一部分而更新的受众。

![显示审核步骤中可用的受众过滤器的屏幕录制。](../assets/ui/activate-streaming-profile-destinations/filter-audiences-review-step.gif)

如果您对您的选择感到满意，并且未检测到任何违反策略的情况，请选择&#x200B;**[!UICONTROL Finish]**&#x200B;以确认您的选择并开始将数据发送到目标。

## 验证受众激活 {#verify}

导出的[!DNL Experience Platform]数据以JSON格式登陆目标目标。 例如，以下事件包含符合特定受众资格并退出其他受众的个人资料的电子邮件地址属性。 此潜在客户的身份是`ECID`和`email_lc_sha256`。

```json
{
  "person": {
    "email": "yourstruly@adobe.com"
  },
  "segmentMembership": {
    "ups": {
      "7841ba61-23c1-4bb3-a495-00d3g5fe1e93": {
        "lastQualificationTime": "2020-05-25T21:24:39Z",
        "status": "exited"
      },
      "59bd2fkd-3c48-4b18-bf56-4f5c5e6967ae": {
        "lastQualificationTime": "2020-05-25T23:37:33Z",
        "status": "realized"
      }
    }
  },
  "identityMap": {
    "ecid": [
      {
        "id": "14575006536349286404619648085736425115"
      },
      {
        "id": "66478888669296734530114754794777368480"
      }
    ],
    "email_lc_sha256": [
      {
        "id": "655332b5fa2aea4498bf7a290cff017cb4"
      },
      {
        "id": "66baf76ef9de8b42df8903f00e0e3dc0b7"
      }
    ]
  }
}
```
