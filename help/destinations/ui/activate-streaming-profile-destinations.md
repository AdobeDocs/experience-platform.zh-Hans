---
keywords: 激活用户档案目标；激活目标；激活数据；激活电子邮件营销目标；激活云存储目标
title: 将受众数据激活到流配置文件导出目标
type: Tutorial
seo-title: 将受众数据激活到流配置文件导出目标
description: 了解如何通过将区段发送到基于用户档案的流目标来激活您在Adobe Experience Platform中拥有的受众数据。
seo-description: 了解如何通过将区段发送到基于用户档案的流目标来激活您在Adobe Experience Platform中拥有的受众数据。
source-git-commit: f0c854e1b6b89d499c720328fa5054611147772f
workflow-type: tm+mt
source-wordcount: '532'
ht-degree: 0%

---


# 将受众数据激活到流配置文件导出目标

## 概述 {#overview}

本文介绍了在Adobe Experience Platform基于用户档案的流式目标(如Amazon Kinesis)中激活受众数据所需的工作流。

## 先决条件 {#prerequisites}

要将数据激活到目标，您必须已成功地[连接到目标](./connect-destination.md)。 如果您尚未执行此操作，请转到[目标目录](../catalog/overview.md)，浏览支持的目标，并配置要使用的目标。

## 选择您的目标 {#select-destination}

1. 转到&#x200B;**[!UICONTROL 连接>目标]**，然后选择&#x200B;**[!UICONTROL 浏览]**&#x200B;选项卡。

   ![“目标浏览”选项卡](../assets/ui/activate-streaming-profile-destinations/browse-tab.png)

1. 选择与要激活区段的目标对应的&#x200B;**[!UICONTROL 添加区段]**&#x200B;按钮，如下图所示。

   ![激活按钮](../assets/ui/activate-streaming-profile-destinations/activate-buttons-browse.png)

1. 移到下一部分，选择[区段](#select-segments)。

## 选择您的区段 {#select-segments}

使用区段名称左侧的复选框选择要激活到目标的区段，然后选择&#x200B;**[!UICONTROL Next]**。

![选择区段](../assets/ui/activate-streaming-profile-destinations/select-segments.png)

## 选择配置文件属性 {#select-attributes}

选择要发送到目标目标的配置文件属性。

>[!NOTE]
>
> Adobe Experience Platform会使用您的架构中四个推荐的常用属性来预填充您的选择：`person.name.firstName`、`person.name.lastName`、`personalEmail.address`、`segmentMembership.status`。

根据是否选择了`segmentMembership.status`，文件导出将按以下方式而有所不同：
* 如果选择了`segmentMembership.status`字段，则导出的文件包括初始完整快照中的&#x200B;**[!UICONTROL 活动]**&#x200B;成员，以及后续增量导出中的&#x200B;**[!UICONTROL 活动]**&#x200B;和&#x200B;**[!UICONTROL 过期]**&#x200B;成员。
* 如果未选择`segmentMembership.status`字段，则导出的文件仅包括初始完整快照和后续增量导出中的&#x200B;**[!UICONTROL Active]**&#x200B;成员。

![推荐属性](../assets/ui/activate-streaming-profile-destinations/attributes-default.png)

1. 在&#x200B;**[!UICONTROL 选择属性]**&#x200B;页面中，选择&#x200B;**[!UICONTROL 添加新字段]**。

   ![添加新映射](../assets/ui/activate-streaming-profile-destinations/add-new-field.png)

1. 选择&#x200B;**[!UICONTROL Schema字段]**&#x200B;条目右侧的箭头。

   ![选择源字段](../assets/ui/activate-streaming-profile-destinations/select-schema-field.png)

1. 在&#x200B;**[!UICONTROL 选择字段]**&#x200B;页面中，选择要发送到目标的XDM属性，然后选择&#x200B;**[!UICONTROL 选择]**。

   ![“选择源字段”页](../assets/ui/activate-streaming-profile-destinations/target-field-page.png)


1. 要添加更多映射，请重复步骤1至3，然后选择&#x200B;**[!UICONTROL Next]**。

## 审阅 {#review}

在&#x200B;**[!UICONTROL Review]**&#x200B;页面上，您可以看到您选择的摘要。 选择&#x200B;**[!UICONTROL 取消]**&#x200B;以划分流程，选择&#x200B;**[!UICONTROL 返回]**&#x200B;以修改设置，或选择&#x200B;**[!UICONTROL 完成]**&#x200B;以确认您的选择并开始向目标发送数据。

>[!IMPORTANT]
>
>在此步骤中，Adobe Experience Platform会检查是否存在数据使用策略违规。 下面显示了违反策略的示例。 在解决违规之前，无法完成区段激活工作流。 有关如何解决策略违规的信息，请参阅数据管理文档一节中的[策略执行](../../rtcdp/privacy/data-governance-overview.md#enforcement)。

![数据策略违规](../assets/common/data-policy-violation.png)

如果未检测到任何违反策略的情况，请选择&#x200B;**[!UICONTROL 完成]**&#x200B;以确认您的选择并开始向目标发送数据。

![审阅](../assets/ui/activate-streaming-profile-destinations/review.png)

## 验证区段激活 {#verify}

导出的[!DNL Experience Platform]数据以JSON格式登陆目标目标。 例如，以下事件包含符合特定区段资格并退出另一个区段的受众的电子邮件地址配置文件属性。 此潜在客户的标识为ECID和电子邮件。

```json
{
  "person": {
    "email": "yourstruly@adobe.con"
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
