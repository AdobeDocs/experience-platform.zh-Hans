---
title: 在新的测试版云存储目标中使用XDM属性的上一个鉴别时间
description: 了解如何在新的测试版云存储目标中使用XDM属性的上一个鉴别时间
hidefromtoc: y
hide: y
source-git-commit: 7dd525d8c71cdfb9fb2393181faa3270ad1dc4cc
workflow-type: tm+mt
source-wordcount: '332'
ht-degree: 0%

---

# 在新的测试版云存储目标中使用XDM属性的上一个鉴别时间 {#last-qualification-time}

>[!IMPORTANT]
> 
>本页介绍测试版中的功能。 功能和文档可能会发生更改。 如果您希望访问此测试版计划，请联系您的Adobe代表或客户关怀团队。

## 先决条件 {#prerequisites}

使用上次资格鉴定时间(`lastQualificationTime`)XDM属性，您必须在 [测试版计划](/help/release-notes/2022/october-2022.md#destinations) 使用改进的文件导出功能，并将数据导出到 [beta云存储目标](/help/release-notes/2022/october-2022.md#destinations) ([[!DNL ADLS Gen 2]](/help/destinations/catalog/cloud-storage/adls-gen2.md), [[!DNL Amazon S3]](/help/destinations/catalog/cloud-storage/amazon-s3.md), [[!DNL Azure Blob]](/help/destinations/catalog/cloud-storage/azure-blob.md), [[!DNL Data Landing Zon]e](/help/destinations/catalog/cloud-storage/data-landing-zone.md), [[!DNL Google Cloud Storage]](/help/destinations/catalog/cloud-storage/google-cloud-storage.md), [SFTP](/help/destinations/catalog/cloud-storage/sftp.md))。 如果您在目录中看到云存储目标的新测试版卡，则您已注册，如下所示 [!DNL Amazon S3].

![显示新的Amazon S3测试版卡的图像](/help/destinations/assets/ui/activate-destinations/new-amazon-s3-beta-card.png)

## 如何使用上次鉴别时间XDM属性 {#how-to-use}

如果您使用六个新的云存储测试版连接器之一，则可以使用 [映射步骤](//help/destinations/ui/activate-batch-profile-destinations.md#mapping) ，用于在导出文件中创建列，且最新时间戳为用户档案符合区段条件时。 这可以帮助您了解某些测量或分析用例，并更好地了解何时激活特定受众。

请注意，要添加 `lastQualificationTime` 要导出文件，您当前需要手动插入值 `xdm: segmentMembership.ups.seg_id.lastQualificationTime` ，如下所示。 您还可以将目标字段编辑为 `lastQualificationTime` 或要命名此列的任何其他值。 请注意，由于这是测试版功能，因此 `xdm: segmentMembership.ups.seg_id.lastQualificationTime` 值可能会在将来发生更改。

![显示XDM属性粘贴到映射步骤中的上次鉴别时间的屏幕记录](/help/destinations/ui/last-qualification-time.gif)

## 更多信息 {#more-information}

有关将数据激活到基于文件的目标（包括工作流中的所有步骤和必要的权限）的广泛信息，请阅读 [激活基于文件的目标教程](/help/destinations/ui/activate-batch-profile-destinations.md).