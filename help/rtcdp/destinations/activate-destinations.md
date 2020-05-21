---
title: 将用户档案和区段激活到目标
seo-title: 将用户档案和区段激活到目标
description: 通过将细分映射到目标，激活您在Adobe实时客户数据平台中的数据。 要完成此操作，请按照以下步骤操作。
seo-description: 通过将细分映射到目标，激活您在Adobe实时客户数据平台中的数据。 要完成此操作，请按照以下步骤操作。
translation-type: tm+mt
source-git-commit: 237ca5fc950b46ae4718850ab1360cdf52b8b112
workflow-type: tm+mt
source-wordcount: '889'
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
5. *视情况而定*. 此步骤因激活区段的目标类型而异。 <br> 对于 *电子邮件营销**目标和云存储目标*，在“选择属 **[!UICONTROL 性”页面上，选]****** 择“添加新字段”并选择要发送到目标的属性。
我们建议将其中一个属性作为合并 [模式的唯](/help/rtcdp/destinations/email-marketing-destinations.md#identity) 一标识符。 有关强制属性的详细信息，请参阅电子邮件营销目 [标文章中的标](/help/rtcdp/destinations/email-marketing-destinations.md#identity) 识。
   ![目标属性](/help/rtcdp/destinations/assets/select-attributes-step.png)

   <br> 

   对于 *社交目标*，在标识 **[!UICONTROL 映射步骤中]** ，您可以选择要映射为目标中的目标标识的源属性。 此步骤为可选或必选，具体取决于您在模式中使用的主要标识。 <br> 

   *电子邮件地址作为主要标识*: 如果您在模式中使用电子邮件地址作为主要标识，则可以跳过标识映射步骤，如下所示：

   ![电子邮件地址作为标识](/help/rtcdp/destinations/assets/email-as-identity.gif)

   <br> 

   *另一个ID作为主标识*: 如果您正在将其他ID( *如奖励ID***&#x200B;或忠诚度ID)用作模式中的主要标识，您需要手动将身份模式中的电子邮件地址映射为社交目标中的目标标识，如下所示：

   ![作为身份的忠诚度ID](/help/rtcdp/destinations/assets/rewardsid-as-identity.gif)


   根据 `Email_LC_SHA256` Facebook电子邮件散列要求，如果您在将目标接收时将客户电子邮件地址哈希化到Adobe Experience Platform，则选择 [身份](/help/rtcdp/destinations/facebook-destination.md#email-hashing-requirements)。 <br> 如果 `Email` 您使用的电子邮件地址没有散列，请选择作为目标标识。 Adobe实时CDP将散列电子邮件地址以符合Facebook要求。

   ![填写字段后的身份映射](/help/rtcdp/destinations/assets/identity-mapping.png)

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

>[!TIP]
>
>Adobe实时CDP与Facebook之间的集成支持历史受众回填。 在将区段激活到目标时，所有历史区段资格都将发送至Facebook。

## 禁用激活 {#disable-activation}

要禁用现有激活流，请执行以下步骤：

1. 在左 **[!UICONTROL 侧导航]** 栏中选择目标，然后单击 **[!UICONTROL 浏览]** 选项卡，然后单击目标名称。
2. 单击右 **[!UICONTROL 边栏]** 中的“已启用”控件以更改激活流状态。
3. 在“更 **新激活流状态** ”窗口中， **选择“确** 认”以禁用流。

在AWS Kinesis中，生成一个访问密钥——秘密访问密钥对，以授予Adobe Real-time CDP对您的AWS Kinesis帐户的访问权限。 在AWS Kinesis文档中 [了解更多信息](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html)。