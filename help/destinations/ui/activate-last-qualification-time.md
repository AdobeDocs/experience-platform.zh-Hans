---
title: 在新的Beta版云存储目标中使用最后限定时间XDM属性
description: 了解如何在新的测试版云存储目标中使用上次资格授予时间XDM属性
badgeBeta: label="Beta 版" type="Informative"
exl-id: d077ea10-5ff2-4acc-8ee6-78ea6cd752d1
source-git-commit: 35429ec2dffacb9c0f2c60b608561988ea487606
workflow-type: tm+mt
source-wordcount: '289'
ht-degree: 1%

---

# 在新的Beta版云存储目标中使用最后限定时间XDM属性 {#last-qualification-time}

>[!IMPORTANT]
> 
>本页介绍了测试版中的功能。 功能和文档可能会发生更改。 如果您希望访问此测试版计划，请联系您的Adobe代表或客户关怀。

## 先决条件 {#prerequisites}

要使用最后限定时间(`lastQualificationTime`) XDM属性，您必须将数据导出到下面列出的六个云存储目标之一：

* [[!DNL ADLS Gen 2]](/help/destinations/catalog/cloud-storage/adls-gen2.md)
* [[!DNL Amazon S3]](/help/destinations/catalog/cloud-storage/amazon-s3.md)
* [[!DNL Azure Blob]](/help/destinations/catalog/cloud-storage/azure-blob.md)
* [[!DNL Data Landing Zone]](/help/destinations/catalog/cloud-storage/data-landing-zone.md)
* [[!DNL Google Cloud Storage]](/help/destinations/catalog/cloud-storage/google-cloud-storage.md)
* [SFTP](/help/destinations/catalog/cloud-storage/sftp.md)

## 如何使用最后限定时间XDM属性 {#how-to-use}

如果您使用上面列出的六个云存储连接器之一，则可以使用激活工作流的[映射步骤](/help/destinations/ui/activate-batch-profile-destinations.md#mapping)中的上次资格取得时间XDM属性，在导出文件中创建一个列，其最新时间戳为配置文件符合区段资格取得时间。 这可以帮助您处理某些测量或分析用例，并让您更好地了解何时激活某些受众。

请注意，要将`lastQualificationTime`添加到您的文件导出，您当前需要手动将值`xdm: segmentMembership.ups.seg_id.lastQualificationTime`插入源字段，如下所示。 您还可以将目标字段编辑为`lastQualificationTime`或要为此列命名的任何其他值。 请注意，由于这是测试版功能，因此`xdm: segmentMembership.ups.seg_id.lastQualificationTime`值的语法将来可能会更改。

![显示上次将XDM属性粘贴到映射步骤中的资格时间的屏幕录制](/help/destinations/ui/last-qualification-time.gif)

## 更多信息 {#more-information}

有关将数据激活到基于文件的目标的详细信息（包括工作流中的所有步骤和必要的权限），请阅读[激活基于文件的目标教程](/help/destinations/ui/activate-batch-profile-destinations.md)。
