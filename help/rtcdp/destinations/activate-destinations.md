---
title: 将配置文件和区段激活到目标
seo-title: 将配置文件和区段激活到目标
description: 通过将细分映射到目标，激活您在Adobe实时客户数据平台中拥有的数据。 要完成此操作，请按照以下步骤操作。
seo-description: 通过将细分映射到目标，激活您在Adobe实时客户数据平台中拥有的数据。 要完成此操作，请按照以下步骤操作。
translation-type: tm+mt
source-git-commit: 73925aa59f9981d8945fb0be6c4924e1831cf902

---


# 将配置文件和区段激活到目标

通过将细分映射到目标，激活您在Adobe实时客户数据平台中拥有的数据。 要完成此操作，请按照以下步骤操作。

## 先决条件 {#prerequisites}

要将数据激活到目标，您必须已成功 [连接目标](/help/rtcdp/destinations/assets/connect-destination.png)。 如果尚未这样做，请转到目标目录 [](/help/rtcdp/destinations/destinations-catalog.md)，浏览支持的目标，然后设置一个或多个目标。

## 激活数据 {#activate-data}

1. 在“ **目标”>“浏览**”中，选择要激活区段的目标。
2. 单击目标的名称。 此操作将带您进入激活流程。
   ![activate-flow](/help/rtcdp/destinations/assets/activate-flow.png)请注意，如果某个目标的激活流程已经存在，您可以看到当前发送到该目标的区段。 在右 **边栏中选择** “编辑激活”，然后按照以下步骤修改激活详细信息。
3. 选择 **激活**;
4. 在激 **活目标向导** ，在选择区段页 **** 面上，选择要发送到目标的区段。
   ![细分到目标](/help/rtcdp/destinations/assets/select-segments.png)
5. *有条件*。 此步骤仅适用于映射到电子邮件营销目标的区段。 <br> 在“目 **标属性** ”页上，选择 **添加新字段** ，然后选择要发送到目标的属性。
我们建议其中一个属性作为您的联合 [架构的唯](/help/rtcdp/destinations/email-marketing-destinations.md#identity) 一标识符。 有关必选属性的详细信息，请参阅电子邮件营销目标 [文章中的标识](/help/rtcdp/destinations/email-marketing-destinations.md#identity) 。
   ![destination-attributes](/help/rtcdp/destinations/assets/destination-attributes.png)
6. 在“ **计划** ”页上，您可以看到向目标发送数据的开始日期以及向目标发送数据的频率。
7. 在“审 **阅** ”页面上，您可以看到所做选择的摘要。 选 **择取消** ，以分解流，选择返回 **，修改设置，或选择完** 成 **** ，以确认选择并开始向目标发送数据。

![确认选择](/help/rtcdp/destinations/assets/confirm-selection.png)

## 编辑激活 {#edit-activation}

请按照以下步骤以实时CDP编辑现有激活流程：

1. 在左 **侧导航栏中** ，选择目标，然后单击浏览选 **项卡** ，然后单击目标名称。
2. 在右 **[!UICONTROL 边栏中选择]** “编辑激活”，以更改要发送到目标的区段。

## 验证区段激活是否成功 {#verify-activation}

### 电子邮件营销目标和云存储目标

对于电子邮件营销目标和云存储目标，Adobe实时CDP会在您提供的存储位置创建制表符 `.txt` 分隔 `.csv` 的或文件。 期望每天在您的存储位置创建一个新文件。 The file format is:
`<destination name>id<destination id><timestamp-yyyymmddhhmmss>`

您在连续三天收到的文件可能如下所示：

```
Salesforce_id3544_20191120110000.csv
Salesforce_id3544_20191121123000.csv
Salesforce_id3544_20191122124530.csv
```

这些文件在您的存储位置中的存在是确认成功激活。

### 广告目标

检查您要激活数据的相应广告目标。 如果激活成功，您的广告平台中会填充受众。

## 禁用激活 {#disable-activation}

要禁用现有激活流程，请执行以下步骤：

1. 在左 **侧导航栏中** ，选择目标，然后单击浏览选 **项卡** ，然后单击目标名称。
2. 单击右 **[!UICONTROL 边栏中]** “已启用”控件以更改激活流程状态。
3. 在“更 **新数据流状态** ”窗口中，选择“ **确认** ”以禁用激活流。

