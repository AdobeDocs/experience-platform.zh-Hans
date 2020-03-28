---
title: 将用户档案和区段激活到目标
seo-title: 将用户档案和区段激活到目标
description: 通过将细分映射到目标，激活您在Adobe实时客户数据平台中拥有的数据。 要完成此操作，请按照以下步骤操作。
seo-description: 通过将细分映射到目标，激活您在Adobe实时客户数据平台中拥有的数据。 要完成此操作，请按照以下步骤操作。
translation-type: tm+mt
source-git-commit: 336aa90cf1e059a92a36dd0ef3222ef6a6f5123b

---


# 将用户档案和区段激活到目标

通过将细分映射到目标，激活您在Adobe实时客户数据平台中拥有的数据。 要完成此操作，请按照以下步骤操作。

## 先决条件 {#prerequisites}

要将数据激活到目标，您必须已成功 [连接目标](/help/rtcdp/destinations/assets/connect-destination.png)。 如果尚未这样做，请转到目标目录 [](/help/rtcdp/destinations/destinations-catalog.md)，浏览支持的目标，然后设置一个或多个目标。

## 激活数据 {#activate-data}

1. 在 **[!UICONTROL Destinations > Browse]**&#x200B;中，选择要激活区段的目标。
2. 单击目标的名称。 此操作将带您进入激活流程。
   ![activate-flow](/help/rtcdp/destinations/assets/activate-flow.png)请注意，如果目标已存在激活流，您可以看到当前发送到目标的区段。 在右 **[!UICONTROL Edit activation]** 边栏中选择，然后按照以下步骤修改激活详细信息。
3. 选择 **[!UICONTROL Activate]**;
4. 在工作 **[!UICONTROL Activate destination]** 流中，在页 **[!UICONTROL Select Segments]** 面上，选择要发送到目标的区段。
   ![细分到目标](/help/rtcdp/destinations/assets/select-segments.png)
5. *视情况而定*. 此步骤仅适用于映射到电子邮件营销目标的区段。 <br> 在页 **[!UICONTROL Destination Attributes]** 面上，选 **[!UICONTROL Add new field]** 择并选择要发送到目标的属性。
我们建议其中一个属性作为合并 [模式的唯一标识符](/help/rtcdp/destinations/email-marketing-destinations.md#identity) 。 有关必选属性的详细信息，请参阅电子邮件营销目标 [文章中的标识](/help/rtcdp/destinations/email-marketing-destinations.md#identity) 。
   ![destination-attributes](/help/rtcdp/destinations/assets/destination-attributes.png)
6. 在该页 **[!UICONTROL Schedule]** 面上，您可以看到向目标发送数据的开始日期以及向目标发送数据的频率。
7. 在页 **[!UICONTROL Review]** 面上，您可以看到所选内容的摘要。 选 **[!UICONTROL Cancel]** 择以分解流、修 **[!UICONTROL Back]** 改设置或确认您的选择 **[!UICONTROL Finish]** 并开始将数据发送到目标。

![确认选择](/help/rtcdp/destinations/assets/confirm-selection.png)

## 编辑激活 {#edit-activation}

请按照以下步骤在实时CDP中编辑现有激活流：

1. 在左 **[!UICONTROL Destinations]** 侧导航栏中选择，然后单击选 **[!UICONTROL Browse]** 项卡，然后单击目标名称。
2. 在右 **[!UICONTROL Edit activation]** 边栏中选择以更改要发送到目标的区段。

## 验证区段激活成功 {#verify-activation}

### 电子邮件营销目标和云存储目标

对于电子邮件营销目标和云存储目标，Adobe实时CDP会在您提供的存储位置创建制表符分 `.txt` 隔 `.csv` 或文件。 期望每天在您的存储位置创建新文件。 The file format is:
`<destination name>id<destination id><timestamp-yyyymmddhhmmss>`

您在连续三天收到的文件可能如下所示：

```
Salesforce_id3544_20191120110000.csv
Salesforce_id3544_20191121123000.csv
Salesforce_id3544_20191122124530.csv
```

这些文件在您的存储位置中的存在是确认激活成功。

### 广告目标

检查您要激活数据的相应广告目标。 如果激活成功，则受众会填充到您的广告平台中。

## 禁用激活 {#disable-activation}

要禁用现有激活流，请执行以下步骤：

1. 在左 **[!UICONTROL Destinations]** 侧导航栏中选择，然后单击选 **[!UICONTROL Browse]** 项卡，然后单击目标名称。
2. 单击右 **[!UICONTROL Enabled]** 边栏中的控件以更改激活流状态。
3. 在“更 **新数据流状态** ”窗口中，选择“ **确认** ”以禁用激活流。

