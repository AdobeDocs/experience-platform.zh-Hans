---
title: 将用户档案和区段激活到目标
seo-title: 将用户档案和区段激活到目标
description: 通过将细分映射到目标，激活您在Adobe实时客户数据平台中拥有的数据。 要完成此操作，请按照以下步骤操作。
seo-description: 通过将细分映射到目标，激活您在Adobe实时客户数据平台中拥有的数据。 要完成此操作，请按照以下步骤操作。
translation-type: tm+mt
source-git-commit: 08b6fd2d43e8ca9d0208ac1bfadc2db15e3f2e90
workflow-type: tm+mt
source-wordcount: '1039'
ht-degree: 0%

---


# 将用户档案和区段激活到目标

通过将细分映射到目标，激活您在Adobe实时客户数据平台中拥有的数据。 要完成此操作，请按照以下步骤操作。

## 先决条件 {#prerequisites}

要将数据激活到目标，您必须已成 [功连接目标](/help/rtcdp/destinations/connect-destination.md)。 如果尚未这样做，请转到目标目 [录](/help/rtcdp/destinations/destinations-catalog.md)，浏览支持的目标，然后设置一个或多个目标。

## 激活数据 {#activate-data}

1. 在 **[!UICONTROL 目标>浏览]**，选择要激活区段的目标。
2. 单击目标的名称。 此操作将带您进入激活流程。
   ![activate-flow](/help/rtcdp/destinations/assets/activate-flow.png)请注意，如果目标激活流已存在，您可以看到当前发送到目标的区段。 选 **[!UICONTROL 择右边栏]** 中的编辑激活，然后按照以下步骤修改激活详细信息。
3. 选择 **[!UICONTROL 激活]**;
4. 在激活 **[!UICONTROL 目标工作流]** ，在选择 **[!UICONTROL 区段页面上]** ，选择要发送到目标的区段。
   ![细分到目标](/help/rtcdp/destinations/assets/email-select-segments.png)
5. *视情况而定*. 此步骤因激活区段的目标类型而异。 <br> 对于 *电子邮件营销**目标和云存储目标*，在“选择属 **[!UICONTROL 性”页面上，选]****** 择“添加新字段”并选择要发送到目标的属性。
我们建议将其中一个属性作为合并 [模式的唯](/help/rtcdp/destinations/email-marketing-destinations.md#identity) 一标识符。 有关强制属性的详细信息，请参阅电子邮件营销目 [标文章中的标](/help/rtcdp/destinations/email-marketing-destinations.md#identity) 识。

   >[!NOTE]
   > 
   >如果任何激活使用标签已应用于数据集（而非整个数据集）中的某些字段，则在以下条件下将执行这些字段级别标签：
   >* 这些字段用在段定义中。
   >* 字段将配置为目标目标的预计属性。

   >
   > 请考虑以下屏幕截图。 例如，如果字段具有与目 `person.name.first.Name` 标的营销用例冲突的特定数据使用标签，则在审核步骤（第7步）中将显示数据使用策略违规。 有关详细信息，请参 [阅实时CDP中的数据管理](/help/rtcdp/privacy/data-governance-overview.md#destinations)

   ![目标属性](/help/rtcdp/destinations/assets/select-attributes-step.png)

   <br> 

   对于 *社交目标*，在标识 **[!UICONTROL 映射步骤中]** ，您可以选择要映射为目标中的目标标识的源属性。 此步骤为可选或必选，具体取决于您在模式中使用的主要标识。 <br> 

   *电子邮件地址作为主要标识*: 如果您在模式中使用电子邮件地址作为主要标识，则可以跳过标识映射步骤，如下所示：

   ![电子邮件地址作为标识](/help/rtcdp/destinations/assets/email-as-identity.gif)

   <br> 

   *另一个ID作为主标识*: 如果您正在将其他ID( *如奖励ID***&#x200B;或忠诚度ID)用作模式中的主要标识，您需要手动将身份模式中的电子邮件地址映射为社交目标中的目标标识，如下所示：

   ![作为身份的忠诚度ID](/help/rtcdp/destinations/assets/rewardsid-as-identity.gif)


   如果 `Email_LC_SHA256` 您根据电子邮件散列法要求将目标接收时的客户电子邮件地址哈希化为Adobe Experience Platform，则 [!DNL Facebook] 选择 [作为身份](/help/rtcdp/destinations/facebook-destination.md#email-hashing-requirements)。 <br> 如果 `Email` 您使用的电子邮件地址没有散列，请选择作为目标标识。 Adobe实时CDP将散列电子邮件地址以符合要 [!DNL Facebook] 求。

   ![填写字段后的身份映射](/help/rtcdp/destinations/assets/identity-mapping.png)

6. 在“ **[!UICONTROL 区段计划]** ”页上，您可以看到向目标发送数据的开始日期以及向目标发送数据的频率。

   >[!IMPORTANT]
   >
   >对于社交目标，您必须在此步骤中选择受众的来源。 只有在选择下图中的某个选项后，才能继续执行下一步。

   ![选择数据来源](/help/rtcdp/destinations/assets/choose-data-origin.png)

7. 在“审 **[!UICONTROL 阅]** ”页面上，您可以看到所选内容的摘要。 选 **[!UICONTROL 择取消]** (Cancel **[!UICONTROL )以分解流，选择]** 返回 **[!UICONTROL (Back)以修改设置，或选择]** 完成(Finish)以确认选择并开始将数据发送到目标。

   >[!IMPORTANT]
   >
   >在此步骤中，实时CDP会检查数据使用策略违规。 下面显示了违反策略的示例。 在解决违规之前，您无法完成区段激活工作流。 有关如何解决违反策略的信息，请参 [阅数据管理](/help/rtcdp/privacy/data-governance-overview.md#enforcement) 文档部分中的策略实施。

![确认选择](/help/rtcdp/destinations/assets/data-policy-violation.png)

如果未检测到任何违反策略的情况，请选 **[!UICONTROL 择“完成]** ”以确认您的选择，并让开始将数据发送到目标。

![确认选择](/help/rtcdp/destinations/assets/confirm-selection.png)



## 编辑激活 {#edit-activation}

请按照以下步骤以实时CDP编辑现有激活流：

1. 在左 **[!UICONTROL 侧导航]** 栏中选择目标，然后单击 **[!UICONTROL 浏览]** 选项卡，然后单击目标名称。
2. 选 **[!UICONTROL 择右边栏]** 中的编辑激活，以更改要发送到目标的区段。

## 验证区段激活成功 {#verify-activation}

### 电子邮件营销目标和云存储目标 {#esp-and-cloud-storage}

对于电子邮件营销目标和云存储目标，Adobe实时CDP会在您提供的存储位 `.csv` 置 `.txt` 创建制表符分隔或文件。 希望每天在存储位置创建新文件。 The file format is:
`<destinationName>_segment<segmentID>_<timestamp-yyyymmddhhmmss>.csv|txt`

您连续三天收到的文件可能如下所示：

```
Salesforce_Marketing_Cloud_segment12341e18-abcd-49c2-836d-123c88e76c39_20200408061804.csv
Salesforce_Marketing_Cloud_segment12341e18-abcd-49c2-836d-123c88e76c39_20200409052200.csv
Salesforce_Marketing_Cloud_segment12341e18-abcd-49c2-836d-123c88e76c39_20200410061130.csv
```

这些文件在您的存储位置是确认成功激活。 要了解导出的文件的结构，您可 [以下载示例。csv文件](/help/rtcdp/destinations/assets/sample_export_file_segment12341e18-abcd-49c2-836d-123c88e76c39_20200408061804.csv)。 此示例文件包括用户档案 `person.firstname`属性 `person.lastname`、 `person.gender`、 `person.birthyear`和 `personalEmail.address`。

### 广告目标

在要激活数据的相应广告目标中检查您的帐户。 如果激活成功，则受众将填充到您的广告平台中。

### 社交网络目标

例 [!DNL Facebook]如，成功的激活意味着 [!DNL Facebook] 将在Facebook Ads Manager中有计划地 [[!UICONTROL 创建自定义受众]](https://www.facebook.com/adsmanager/manage/)。 由于用户对已激活的区段具有资格或取消资格，因此将添加和删除该受众的区段成员资格。

>[!TIP]
>
>Adobe实时CDP与历史受众回填之 [!DNL Facebook] 间的集成。 在将区段激活到目标时， [!DNL Facebook] 所有历史区段资格都将发送至。

## 禁用激活 {#disable-activation}

要禁用现有激活流，请执行以下步骤：

1. 在左 **[!UICONTROL 侧导航]** 栏中选择目标，然后单击 **[!UICONTROL 浏览]** 选项卡，然后单击目标名称。
2. 单击右 **[!UICONTROL 边栏]** 中的“已启用”控件以更改激活流状态。
3. 在“更 **新激活流状态** ”窗口中， **选择“确** 认”以禁用流。
