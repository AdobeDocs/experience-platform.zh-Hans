---
title: 将用户档案和区段激活到目标
seo-title: 将用户档案和区段激活到目标
description: 通过将细分映射到目标，激活您在Adobe实时客户数据平台中的数据。 要完成此操作，请按照以下步骤操作。
seo-description: 通过将细分映射到目标，激活您在Adobe实时客户数据平台中的数据。 要完成此操作，请按照以下步骤操作。
translation-type: tm+mt
source-git-commit: 7dafdf0dd1ad3af2defab3bf6b784fd37e777062
workflow-type: tm+mt
source-wordcount: '639'
ht-degree: 0%

---


# 将用户档案和区段激活到目标

通过将细分映射到目标，激活您在Adobe实时客户数据平台中的数据。 要完成此操作，请按照以下步骤操作。

## 先决条件 {#prerequisites}

要将数据激活到目标，您必须已成 [功连接目标](/help/rtcdp/destinations/assets/connect-destination.png)。 如果尚未这样做，请转到目标目 [录](/help/rtcdp/destinations/destinations-catalog.md)，浏览支持的目标，然后设置一个或多个目标。

## 激活数据 {#activate-data}

1. 在 **[!UICONTROL 目标>浏览]**，选择要激活区段的目标。
2. 单击目标的名称。 此操作将带您进入激活流程。
   ![activate-flow](/help/rtcdp/destinations/assets/activate-flow.png)请注意，如果目标激活流已存在，您可以看到当前发送到目标的区段。 选 **[!UICONTROL 择右边栏]** 中的编辑激活，然后按照以下步骤修改激活详细信息。
3. 选择 **[!UICONTROL 激活]**;
4. 在激活 **[!UICONTROL 目标工作流]** ，在选择 **[!UICONTROL 区段页面上]** ，选择要发送到目标的区段。
   ![细分到目标](/help/rtcdp/destinations/assets/select-segments.png)
5. *视情况而定*. 此步骤仅适用于映射到云存储目标和电子邮件营销目标的细分。 <br> 在“目 **[!UICONTROL 标属性]** ”页上，选 **[!UICONTROL 择“添加新字段]** ”，然后选择要发送到目标的属性。
我们建议将其中一个属性作为合并 [模式的唯](/help/rtcdp/destinations/email-marketing-destinations.md#identity) 一标识符。 有关强制属性的详细信息，请参阅电子邮件营销目 [标文章中的标](/help/rtcdp/destinations/email-marketing-destinations.md#identity) 识。
   ![目标属性](/help/rtcdp/destinations/assets/destination-attributes.png)
6. 在“ **[!UICONTROL 区段计划]** ”页上，您可以看到向目标发送数据的开始日期以及向目标发送数据的频率。

   >[!IMPORTANT]
   >
   >对于社交目标，您必须在此步骤中选择受众的来源。 只有在选择下图中的某个选项后，才能继续执行下一步。

   ![选择数据来源](/help/rtcdp/destinations/assets/choose-data-origin.png)

7. 在“审 **[!UICONTROL 阅]** ”页面上，您可以看到所选内容的摘要。 选 **[!UICONTROL 择取消]** (Cancel **[!UICONTROL )以分解流，选择]** 返回 **[!UICONTROL (Back)以修改设置，或选择]** 完成(Finish)以确认选择并开始将数据发送到目标。

![确认选择](/help/rtcdp/destinations/assets/confirm-selection.png)

## 编辑激活 {#edit-activation}

请按照以下步骤以实时CDP编辑现有激活流：

1. 在左 **[!UICONTROL 侧导航]** 栏中选择目标，然后单击 **[!UICONTROL 浏览]** 选项卡，然后单击目标名称。
2. 选 **[!UICONTROL 择右边栏]** 中的编辑激活，以更改要发送到目标的区段。

## 验证区段激活成功 {#verify-activation}

### 电子邮件营销目标和云存储目标

对于电子邮件营销目标和云存储目标，Adobe实时CDP会在您提供的存储位 `.txt` 置 `.csv` 创建制表符分隔或文件。 希望每天在存储位置创建新文件。 The file format is:
`<destination name>id<destination id><timestamp-yyyymmddhhmmss>`

您连续三天收到的文件可能如下所示：

```
Salesforce_id3544_20191120110000.csv
Salesforce_id3544_20191121123000.csv
Salesforce_id3544_20191122124530.csv
```

这些文件在您的存储位置是确认成功激活。

### 广告目标

检查要激活数据的各个广告目标。 如果激活成功，则受众将填充到您的广告平台中。

### 社交网络目标

对于Facebook，成功的激活意味着将在Facebook Ads Manager中有计划地创建 [Facebook自定义受众](https://www.facebook.com/adsmanager/manage/)。 由于用户对已激活的区段具有资格或取消资格，因此将添加和删除该受众的区段成员资格。

## 禁用激活 {#disable-activation}

要禁用现有激活流，请执行以下步骤：

1. 在左 **[!UICONTROL 侧导航]** 栏中选择目标，然后单击 **[!UICONTROL 浏览]** 选项卡，然后单击目标名称。
2. 单击右 **[!UICONTROL 边栏]** 中的“已启用”控件以更改激活流状态。
3. 在“更 **新激活流状态** ”窗口中， **选择“确** 认”以禁用流。

