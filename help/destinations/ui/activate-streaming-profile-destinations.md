---
keywords: 激活用户档案目标；激活目标；激活数据；激活电子邮件营销目标；激活云存储目标
title: 将受众数据激活到流配置文件导出目标
type: Tutorial
seo-title: Activate audience data to streaming profile export destinations
description: 了解如何通过将区段发送到基于用户档案的流目标来激活您在Adobe Experience Platform中拥有的受众数据。
seo-description: Learn how to activate the audience data you have in Adobe Experience Platform by sending segments to streaming profile-based destinations.
exl-id: bc0f781e-60de-44a5-93cb-06b4a3148591
source-git-commit: 0b094e635e6d22e58e5aa79a374df0879167a833
workflow-type: tm+mt
source-wordcount: '557'
ht-degree: 0%

---

# 将受众数据激活到流配置文件导出目标

>[!IMPORTANT]
> 
>要激活数据，您需要 **[!UICONTROL 管理目标]**, **[!UICONTROL 激活目标]**, **[!UICONTROL 查看配置文件]**&#x200B;和 **[!UICONTROL 查看区段]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或联系您的产品管理员以获取所需的权限。

## 概述 {#overview}

本文介绍了在Adobe Experience Platform基于用户档案的流式目标(如Amazon Kinesis)中激活受众数据所需的工作流。

## 先决条件 {#prerequisites}

要将数据激活到目标，您必须成功 [连接到目标](./connect-destination.md). 如果您尚未执行此操作，请转到 [目标目录](../catalog/overview.md)，浏览支持的目标，并配置要使用的目标。

## 选择您的目标 {#select-destination}

1. 转到 **[!UICONTROL 连接>目标]**，然后选择 **[!UICONTROL 目录]** 选项卡。

   ![“目标目录”选项卡](../assets/ui/activate-streaming-profile-destinations/catalog-tab.png)

1. 选择 **[!UICONTROL 激活区段]** 在与要激活区段的目标对应的卡上，如下图所示。

   ![“激活区段”按钮](../assets/ui/activate-streaming-profile-destinations/activate-segments-button.png)

1. 选择要用于激活区段的目标连接，然后选择 **[!UICONTROL 下一个]**.

   ![选择目标](../assets/ui/activate-streaming-profile-destinations/select-destination.png)

1. 移到下一个部分 [选择区段](#select-segments).

## 选择您的区段 {#select-segments}

使用区段名称左侧的复选框选择要激活到目标的区段，然后选择 **[!UICONTROL 下一个]**.

![选择区段](../assets/ui/activate-streaming-profile-destinations/select-segments.png)

## 选择配置文件属性 {#select-attributes}

选择要发送到目标目标的配置文件属性。

>[!NOTE]
>
> Adobe Experience Platform会使用您的架构中四个推荐的常用属性来预填充您的选择： `person.name.firstName`, `person.name.lastName`, `personalEmail.address`, `segmentMembership.status`.

文件导出将按以下方式有所不同，具体取决于 `segmentMembership.status` 已选中：
* 如果 `segmentMembership.status` 字段，导出的文件包括 **[!UICONTROL 活动]** 初始完整快照中的成员和 **[!UICONTROL 活动]** 和 **[!UICONTROL 过期]** 成员。
* 如果 `segmentMembership.status` 字段，导出的文件仅包含 **[!UICONTROL 活动]** 初始完整快照和后续增量导出中的成员。

![推荐属性](../assets/ui/activate-streaming-profile-destinations/attributes-default.png)

1. 在 **[!UICONTROL 选择属性]** 页面，选择 **[!UICONTROL 添加新字段]**.

   ![添加新映射](../assets/ui/activate-streaming-profile-destinations/add-new-field.png)

1. 选择 **[!UICONTROL 架构字段]** 中。

   ![选择源字段](../assets/ui/activate-streaming-profile-destinations/select-schema-field.png)

1. 在 **[!UICONTROL 选择字段]** ，选择要发送到目标的XDM属性，然后选择 **[!UICONTROL 选择]**.

   ![“选择源字段”页](../assets/ui/activate-streaming-profile-destinations/target-field-page.png)


1. 要添加更多映射，请重复步骤1至3，然后选择 **[!UICONTROL 下一个]**.

## 审阅 {#review}

在 **[!UICONTROL 审阅]** 页面，则可以查看所选内容的摘要。 选择 **[!UICONTROL 取消]** 来分解流量， **[!UICONTROL 返回]** 修改设置，或 **[!UICONTROL 完成]** 以确认您的选择并开始向目标发送数据。

>[!IMPORTANT]
>
>在此步骤中，Adobe Experience Platform会检查是否存在数据使用策略违规。 下面显示了违反策略的示例。 在解决违规之前，无法完成区段激活工作流。 有关如何解决策略违规的信息，请参阅 [策略执行](../../rtcdp/privacy/data-governance-overview.md#enforcement) 在“数据管理文档”一节中。

![数据策略违规](../assets/common/data-policy-violation.png)

如果未检测到任何策略违规，请选择 **[!UICONTROL 完成]** 以确认您的选择并开始向目标发送数据。

![审阅](../assets/ui/activate-streaming-profile-destinations/review.png)

## 验证区段激活 {#verify}

导出的 [!DNL Experience Platform] 数据以JSON格式登陆您的目标目标。 例如，以下事件包含符合特定区段资格并退出另一个区段的受众的电子邮件地址配置文件属性。 此潜在客户的标识为ECID和电子邮件。

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
        "status": "existing"
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
