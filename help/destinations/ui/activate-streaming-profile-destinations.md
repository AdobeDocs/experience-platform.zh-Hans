---
title: 将受众激活到流配置文件导出目标
type: Tutorial
description: 了解如何通过将受众发送到基于个人资料的流目标来激活您在Adobe Experience Platform中的受众数据。
badgeUltimate: label="Ultimate" type="Positive"
exl-id: bc0f781e-60de-44a5-93cb-06b4a3148591
source-git-commit: 3e2dc51e768d6bcfeedbc26e04997dc46c852e4d
workflow-type: tm+mt
source-wordcount: '761'
ht-degree: 0%

---


# 将受众激活到流配置文件导出目标

>[!IMPORTANT]
> 
> * 要激活数据并启用 [映射步骤](#mapping) 的工作流中，您需要 **[!UICONTROL 管理目标]**， **[!UICONTROL 激活目标]**， **[!UICONTROL 查看配置文件]**、和 **[!UICONTROL 查看区段]** [访问控制权限](/help/access-control/home.md#permissions).
> * 要激活数据，而不通过 [映射步骤](#mapping) 的工作流中，您需要 **[!UICONTROL 管理目标]**， **[!UICONTROL 激活没有映射的区段]**， **[!UICONTROL 查看配置文件]**、和 **[!UICONTROL 查看区段]** [访问控制权限](/help/access-control/home.md#permissions).
> 
> 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或与产品管理员联系以获取所需的权限。

## 概述 {#overview}

本文介绍了在Adobe Experience Platform中将受众数据激活到基于个人资料的流目标(也称为 [企业目标](/help/destinations/destination-types.md#streaming-profile-export))。

本文适用于以下三个目标：

* [Amazon Kinesis](/help/destinations/catalog/cloud-storage/amazon-kinesis.md)
* [Azure事件中心](/help/destinations/catalog/cloud-storage/azure-event-hubs.md)
* [HTTP API目标](/help/destinations/catalog/streaming/http-destination.md).

## 先决条件 {#prerequisites}

要将数据激活到目标，您必须已成功完成 [已连接到目标](./connect-destination.md). 如果您尚未这样做，请转到 [目标目录](../catalog/overview.md)，浏览支持的目标，并配置要使用的目标。

## 选择您的目标 {#select-destination}

1. 转到 **[!UICONTROL “连接”>“目标”]**，然后选择 **[!UICONTROL 目录]** 选项卡。

   ![显示目标目录选项卡的图像。](../assets/ui/activate-streaming-profile-destinations/catalog-tab.png)

1. 选择 **[!UICONTROL 激活受众]** ，，如下图所示。

   ![突出显示目标目录选项卡中的激活受众控件的图像。](../assets/ui/activate-streaming-profile-destinations/activate-audiences-button.png)

1. 选择要用于激活受众的目标连接，然后选择 **[!UICONTROL 下一个]**.

   ![该图显示了您可以连接的两个目标选项。](../assets/ui/activate-streaming-profile-destinations/select-destination.png)

1. 移到下一节至 [选择您的受众](#select-audiences).

## 选择您的受众 {#select-audiences}

要选择要激活到目标的受众，请选中受众名称左侧的复选框，然后选择 **[!UICONTROL 下一个]**.

您可以从多种类型的受众中进行选择，具体取决于其来源：

* **[!UICONTROL 分段服务]**：分段服务在Experience Platform中生成的受众。 请参阅 [分段文档](../../segmentation/ui/overview.md) 以了解更多详细信息。
* **[!UICONTROL 自定义上传]**：在Experience Platform之外生成的受众，以CSV文件形式上传到Platform。 要了解有关外部受众的更多信息，请参阅关于以下内容的文档： [导入受众](../../segmentation/ui/overview.md#import-audience).
* 其他类型的受众，源自其他Adobe解决方案，例如 [!DNL Audience Manager].

![突出显示激活工作流选择受众步骤中复选框选择的图像。](../assets/ui/activate-streaming-profile-destinations/select-audiences.png)

## 选择配置文件属性 {#select-attributes}

在 **[!UICONTROL 映射]** 步骤，选择要发送到目标目标的配置文件属性。

1. 在 **[!UICONTROL 选择属性]** 页面，选择 **[!UICONTROL 添加新字段]**.

   ![在映射步骤中突出显示添加新字段控件的图像。](../assets/ui/activate-streaming-profile-destinations/add-new-field.png)

1. 选择右侧的箭头 **[!UICONTROL 架构字段]** 进入。

   ![突出显示映射步骤中如何选择源字段的图像。](../assets/ui/activate-streaming-profile-destinations/select-schema-field.png)

1. 在 **[!UICONTROL 选择字段]** 页面上，选择要发送到目标的XDM属性，然后选择 **[!UICONTROL 选择]**.

   ![显示了一组可选择作为源字段的XDM字段的图像。](../assets/ui/activate-streaming-profile-destinations/target-field-page.png)

1. 要添加更多字段，请重复步骤1至3，然后选择 **[!UICONTROL 下一个]**.

## 请查看 {#review}

在 **[!UICONTROL 审核]** 页面上，您可以看到选择的摘要。 选择 **[!UICONTROL 取消]** 来打破气流， **[!UICONTROL 返回]** 以修改设置，或者 **[!UICONTROL 完成]** 以确认您的选择并开始向目标发送数据。

![审核步骤中的选择摘要。](../assets/ui/activate-streaming-profile-destinations/review.png)

### 同意策略评估 {#consent-policy-evaluation}

[同意政策评估](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) 当前不支持在导出到三个企业目标(Amazon Kinesis、Azure事件中心和HTTP API)时这样做。

这意味着用户档案未同意成为目标 *包括* ，以访问这三个目标。

<!--

If your organization purchased **Adobe Healthcare Shield** or **Adobe Privacy & Security Shield**, select **[!UICONTROL View applicable consent policies]** to see which consent policies are applied and how many profiles are included in the activation as a result of them. Read about [consent policy evaluation](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) for more information.

-->

### 数据使用策略检查 {#data-usage-policy-checks}

在 **[!UICONTROL 审核]** 步骤，Experience Platform还会检查是否存在任何数据使用策略违规。 下面显示了一个违反策略的示例。 在解决该违规之前，您无法完成受众激活工作流。 有关如何解决策略违规的信息，请参阅 [数据使用策略违规](/help/data-governance/enforcement/auto-enforcement.md#data-usage-violation) 数据管理文档一节中。

![数据策略违规](../assets/common/data-policy-violation.png)

### 筛选受众 {#filter-audiences}

此外，在此步骤中，您可以使用页面上的可用过滤器仅显示其计划或映射作为此工作流的一部分而更新的受众。

![显示审核步骤中可用的受众过滤器的屏幕录制。](../assets/ui/activate-streaming-profile-destinations/filter-audiences-review-step.gif)

如果您对您的选择感到满意，并且未检测到任何违反策略的情况，请选择 **[!UICONTROL 完成]** 以确认您的选择并开始向目标发送数据。

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
