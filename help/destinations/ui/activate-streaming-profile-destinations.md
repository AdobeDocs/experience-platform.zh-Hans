---
keywords: 激活配置文件目标；激活目标；激活数据；激活电子邮件营销目标；激活云存储目标
title: 将受众激活到流配置文件导出目标
type: Tutorial
description: 了解如何通过将受众发送到基于用户档案的流目标，激活您在Adobe Experience Platform中的受众数据。
exl-id: bc0f781e-60de-44a5-93cb-06b4a3148591
source-git-commit: 37819b5a6480923686d327e30b1111ea29ae71da
workflow-type: tm+mt
source-wordcount: '760'
ht-degree: 5%

---


# 将受众激活到流配置文件导出目标

>[!IMPORTANT]
> 
> * 要激活数据并启用 [映射步骤](#mapping) 的工作流，您需要 **[!UICONTROL 管理目标]**， **[!UICONTROL 激活目标]**， **[!UICONTROL 查看配置文件]**、和 **[!UICONTROL 查看区段]** [访问控制权限](/help/access-control/home.md#permissions).
> * 要激活数据，而不通过 [映射步骤](#mapping) 的工作流，您需要 **[!UICONTROL 管理目标]**， **[!UICONTROL 激活没有映射的区段]**， **[!UICONTROL 查看配置文件]**、和 **[!UICONTROL 查看区段]** [访问控制权限](/help/access-control/home.md#permissions).
> 
> 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或与产品管理员联系以获取所需的权限。

## 概述 {#overview}

本文介绍了在基于用户档案的Adobe Experience Platform流式目标(如Amazon Kinesis)中激活受众数据所需的工作流。

## 先决条件 {#prerequisites}

要将数据激活到目标，您必须已成功 [已连接到目标](./connect-destination.md). 如果您尚未这样做，请转到 [目标目录](../catalog/overview.md)，浏览支持的目标，并配置要使用的目标。

## 选择您的目标 {#select-destination}

1. 转到 **[!UICONTROL 连接>目标]**，并选择 **[!UICONTROL 目录]** 选项卡。

   ![显示目标目录选项卡的图像。](../assets/ui/activate-streaming-profile-destinations/catalog-tab.png)

1. 选择 **[!UICONTROL 激活受众]** ，该页面位于要激活受众的目标对应的信息卡上，如下图所示。

   ![在目标目录选项卡中突出显示“激活受众”控件的图像。](../assets/ui/activate-streaming-profile-destinations/activate-audiences-button.png)

1. 选择要用于激活受众的目标连接，然后选择 **[!UICONTROL 下一个]**.

   ![该图显示了您可以连接的两个目标选项。](../assets/ui/activate-streaming-profile-destinations/select-destination.png)

1. 移到下一部分以 [选择您的受众](#select-audiences).

## 选择您的受众 {#select-audiences}

要选择要激活到目标的受众，请选中受众名称左侧的复选框，然后选择 **[!UICONTROL 下一个]**.

您可以根据受众的来源，从多种类型的受众中进行选择：

* **[!UICONTROL 分段服务]**：分段服务在Experience Platform中生成的受众。 请参阅 [分段文档](../../segmentation/ui/overview.md) 了解更多详细信息。
* **[!UICONTROL 自定义上传]**：受众在Experience Platform之外生成，并以CSV文件形式上传到Platform。 要了解有关外部受众的更多信息，请参阅有关以下内容的文档 [导入受众](../../segmentation/ui/overview.md#import-audience).
* 其他类型的受众，源自其他Adobe解决方案，例如 [!DNL Audience Manager].

![突出显示激活工作流选择受众步骤中的复选框选择的图像。](../assets/ui/activate-streaming-profile-destinations/select-audiences.png)

## 选择配置文件属性 {#select-attributes}

在 **[!UICONTROL 映射]** 步骤，选择要发送到目标目标的配置文件属性。

1. 在 **[!UICONTROL 选择属性]** 页面，选择 **[!UICONTROL 添加新字段]**.

   ![在映射步骤中突出显示“添加新字段”控件的图像。](../assets/ui/activate-streaming-profile-destinations/add-new-field.png)

1. 选择右侧的箭头 **[!UICONTROL 架构字段]** 登入。

   ![突出显示映射步骤中如何选择源字段的图像。](../assets/ui/activate-streaming-profile-destinations/select-schema-field.png)

1. 在 **[!UICONTROL 选择字段]** 页面上，选择要发送到目标的XDM属性，然后选择 **[!UICONTROL 选择]**.

   ![该图像显示了可选择作为源字段的一系列XDM字段。](../assets/ui/activate-streaming-profile-destinations/target-field-page.png)

1. 要添加更多字段，请重复步骤1至3，然后选择 **[!UICONTROL 下一个]**.

## 请查看 {#review}

在 **[!UICONTROL 审核]** 页面时，您可以看到所选内容的摘要。 选择 **[!UICONTROL 取消]** 来打破气流， **[!UICONTROL 返回]** 修改设置，或者 **[!UICONTROL 完成]** 以确认您的选择并开始向目标发送数据。

![审核步骤中的选择摘要。](../assets/ui/activate-streaming-profile-destinations/review.png)

### 同意政策评估 {#consent-policy-evaluation}

如果您的组织购买了 **Adobe Healthcare Shield** 或 **Adobe Privacy &amp; Security Shield**，请选择&#x200B;**[!UICONTROL 查看适用的同意策略]**&#x200B;以查看应用了哪些同意策略以及作为其结果包含在激活中的配置文件数量。阅读关于 [同意政策评估](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) 了解更多信息。

### 数据使用策略检查 {#data-usage-policy-checks}

在 **[!UICONTROL 审核]** 步骤，Experience Platform还会检查是否存在任何数据使用策略违规。 下面显示了一个违反策略的示例。 在解决该违规之前，您无法完成受众激活工作流。 有关如何解决策略违规的信息，请参阅 [数据使用策略违规](/help/data-governance/enforcement/auto-enforcement.md#data-usage-violation) 在数据治理文档部分中。

![数据策略违规](../assets/common/data-policy-violation.png)

### 筛选受众 {#filter-audiences}

此外，在此步骤中，您可以使用页面上的可用过滤器仅显示其计划或映射已作为此工作流的一部分更新的受众。

![屏幕录制，其中显示审核步骤中的可用受众筛选器。](../assets/ui/activate-streaming-profile-destinations/filter-audiences-review-step.gif)

如果您对您的选择感到满意，并且未检测到违反策略的情况，请选择 **[!UICONTROL 完成]** 以确认您的选择并开始向目标发送数据。

## 验证受众激活 {#verify}

已导出 [!DNL Experience Platform] 数据以JSON格式登陆到您的目标目标。 例如，以下事件包含符合特定受众资格并退出其他受众的个人资料的电子邮件地址属性。 此潜在客户的身份为 `ECID` 和 `email_lc_sha256`.

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
