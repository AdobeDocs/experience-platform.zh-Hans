---
title: 交易台 — CRM连接
description: 激活交易台帐户中的配置文件，以根据CRM数据进行受众定位和抑制。
last-substantial-update: 2025-01-16T00:00:00Z
exl-id: e09eaede-5525-4a51-a0e6-00ed5fdc662b
source-git-commit: 036d784014e7cdb101f39f63f9d6e8bac01fdc97
workflow-type: tm+mt
source-wordcount: '1088'
ht-degree: 5%

---

# [!DNL Trade Desk] - CRM连接

>[!IMPORTANT]
>
>随着 EUID (European Unified ID) 的发布，现在您在[目标目录](/help/destinations/catalog/overview.md)中会看到两个 [!DNL The Trade Desk - CRM] 目标。
>
>* 如果您在欧盟获取数据，请使用 **[!DNL The Trade Desk - CRM (EU)]** 目标。
>* 如果您在 APAC 或 NAMER 地区获取数据，请使用 **[!DNL The Trade Desk - CRM (NAMER & APAC)]** 目标。
>
>此目标连接器和文档页面由&#x200B;*[!DNL Trade Desk]*&#x200B;团队创建和维护。 有关查询或更新请求，请联系您的[!DNL Trade Desk]代表。

## 概述 {#overview}

了解如何根据CRM数据向[!DNL Trade Desk]帐户激活配置文件以进行受众定位和抑制。

此连接器将数据发送到[!DNL The Trade Desk]第一方终结点。 Adobe Experience Platform与[!DNL The Trade Desk]之间的集成不支持将数据导出到[!DNL The Trade Desk]第三方端点。

[!DNL The Trade Desk(TTD)]不会随时直接处理电子邮件地址的上传文件，[!DNL The Trade Desk]也不会存储您的原始（未散列）电子邮件。

>[!TIP]
>
>使用[!DNL The Trade Desk]个CRM目标进行CRM数据映射，如电子邮件或哈希电子邮件地址。 使用Adobe Experience Platform目录中的[其他交易台目标](/help/destinations/catalog/advertising/tradedesk.md)进行Cookie和设备ID映射。

## 先决条件 {#prerequisites}

>[!IMPORTANT]
>
>您必须先联系[!DNL Trade Desk]客户经理以签署CRM载入合同，然后才能将受众激活到交易台。 [!DNL The Trade Desk]将允许使用UID2 / EUID并共享其他详细信息以帮助您配置目标。

## ID匹配要求 {#id-matching-requirements}

根据您摄取到Adobe Experience Platform中的ID类型，您必须遵守其相应的要求。 有关详细信息，请阅读[身份命名空间概述](/help/identity-service/features/namespaces.md)。

## 支持的身份 {#supported-identities}

[!DNL The Trade Desk]支持激活下表中描述的标识。 了解有关[标识](/help/identity-service/features/namespaces.md)的更多信息。

Adobe Experience Platform支持纯文本和SHA256哈希电子邮件地址。 按照ID匹配要求部分中的说明进行操作，并分别将适当的命名空间用于纯文本和经过哈希处理的电子邮件地址。

| 目标身份 | 描述 | 注意事项 |
|---|---|---|
| 电子邮件 | 电子邮件地址（明文） | 当您的源身份是电子邮件命名空间或属性时，输入`email`作为目标身份。 |
| Email_LC_SHA256 | 电子邮件地址需要使用SHA256和小写进行哈希处理。 您以后将无法更改此设置。 | 当源身份是Email_LC_SHA256命名空间或属性时，输入`hashed_email`作为目标身份。 |

{style="table-layout:auto"}

## 电子邮件哈希处理要求 {#hashing-requirements}

您可以在将电子邮件地址摄取到Adobe Experience Platform中之前对其进行哈希处理，或者使用原始电子邮件地址。

要了解如何在Experience Platform中摄取电子邮件地址，请阅读[批次摄取概述](/help/ingestion/batch-ingestion/overview.md)。

如果选择自己对电子邮件地址进行哈希处理，请确保符合以下要求：

* 删除前导空格和尾随空格。
* 将所有ASCII字符转换为小写。
* 在`gmail.com`电子邮件地址中，从电子邮件地址的用户名部分删除以下字符：
   * 句点(. （ASCII代码46）。 例如，将`jane.doe@gmail.com`标准化为`janedoe@gmail.com`。
   * 加号(+ （ASCII代码43）)和所有后续字符。 例如，将`janedoe+home@gmail.com`标准化为`janedoe@gmail.com`。

## 导出类型和频率 {#export-type-frequency}

有关目标导出类型和频率的信息，请参阅下表。

| 项目 | 类型 | 注释 |
|---------|----------|---------|
| 导出类型 | **[!UICONTROL Audience export]** | 您正在导出具有在交易台目标中使用的标识符（电子邮件或哈希电子邮件）的受众的所有成员。 |
| 导出频率 | **[!UICONTROL Daily Batch]** | 由于配置文件是根据受众评估在Experience Platform中进行更新的，因此配置文件（身份）每天会更新一次以流向目标平台。 阅读有关[批处理导出](/help/destinations/destination-types.md#file-based)的详细信息。 |

{style="table-layout:auto"}

## 连接到目标 {#connect}

### 验证目标 {#authenticate}

[!DNL The Trade Desk] CRM目标为每日批处理文件上传，不需要用户身份验证。

### 填写目标详细信息 {#fill-in-details}

在将受众数据发送到或激活到目标之前，您必须先设置与自己的目标平台的连接。 在[设置](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html?lang=zh-Hans)此目标时，必须提供以下信息：

* **[!UICONTROL Account Type]**：请选择&#x200B;**[!UICONTROL Existing Account]**&#x200B;选项。
* **[!UICONTROL Name]**：将来用于识别此目标的名称。
* **[!UICONTROL Description]**：可帮助您将来识别此目标的描述。
* **[!UICONTROL Advertiser ID]**：您的[!DNL Trade Desk Advertiser ID]，可以由您的[!DNL Trade Desk]帐户管理员共享或在[!DNL Advertiser Preferences] UI中的[!DNL Trade Desk]下找到。

![Experience Platform UI屏幕截图显示如何填写目标详细信息。](/help/destinations/assets/catalog/advertising/tradedesk/configuredestination2.png)

连接到目标时，设置数据管理策略是完全可选的。 有关更多详细信息，请查看Experience Platform [数据管理概述](/help/data-governance/policies/overview.md)。

## 激活此目标的受众 {#activate}

>[!IMPORTANT]
> 
>* 若要激活数据，您需要&#x200B;**[!UICONTROL View Destinations]**、**[!UICONTROL Activate Destinations]**、**[!UICONTROL View Profiles]**&#x200B;和&#x200B;**[!UICONTROL View Segments]** [访问控制权限](/help/access-control/home.md#permissions)。 阅读[访问控制概述](/help/access-control/ui/overview.md)或联系您的产品管理员以获取所需的权限。
>* 要导出&#x200B;*标识*，您需要&#x200B;**[!UICONTROL View Identity Graph]** [访问控制权限](/help/access-control/home.md#permissions)。<br> ![选择工作流中突出显示的身份命名空间以将受众激活到目标。](/help/destinations/assets/overview/export-identities-to-destination.png "选择工作流中突出显示的身份命名空间以将受众激活到目标。"){width="100" zoomable="yes"}

有关将受众激活到目标的说明，请阅读[将受众数据激活到批量配置文件导出目标](/help/destinations/ui/activate-batch-profile-destinations.md)。

在&#x200B;**[!UICONTROL Scheduling]**&#x200B;页面中，您可以为要导出的每个受众配置计划和文件名。 配置时间表是强制性的，但配置文件名是可选的。

![Experience Platform UI屏幕截图以安排Audience Activation。](/help/destinations/assets/catalog/advertising/tradedesk/schedulesegment1.png)

>[!NOTE]
>
>激活到[!DNL The Trade Desk] CRM目标的所有受众都会自动设置为每日频率和完整文件导出。

![Experience Platform UI屏幕截图以安排Audience Activation。](/help/destinations/assets/catalog/advertising/tradedesk/schedulesegment2.png)

在&#x200B;**[!UICONTROL Mapping]**&#x200B;页中，必须从源列中选择属性或身份命名空间并映射到目标列。

![用于映射受众激活的Experience Platform UI屏幕截图。](/help/destinations/assets/catalog/advertising/tradedesk/mappingsegment1.png)

以下是激活受众到[!DNL The Trade Desk] CRM目标时正确标识映射的示例。

>[!IMPORTANT]
>
> [!DNL The Trade Desk] CRM目标不接受原始和经过哈希处理的电子邮件地址作为同一激活流中的标识。 为原始电子邮件地址和经过哈希处理的电子邮件地址创建单独的激活流程。

选择源字段：

* 如果在数据摄取时使用原始电子邮件地址，请选择`Email`命名空间或属性作为源标识。
* 如果您在数据摄取到Experience Platform时经过哈希处理的客户电子邮件地址，请选择`Email_LC_SHA256`命名空间或属性作为源身份。

选择目标字段：

* 当源命名空间或属性为`email`时，输入`Email`作为目标标识。
* 当源命名空间或属性为`hashed_email`时，输入`Email_LC_SHA256`作为目标标识。

## 验证数据导出 {#validate}

要验证数据是否已从Experience Platform正确导出到[!DNL The Trade Desk]，请在[!DNL The Trade Desk]数据管理平台(DMP)的Adobe 1PD数据拼贴下找到受众。 以下是在[!DNL Trade Desk] UI中查找相应ID的步骤：

1. 首先，选择&#x200B;**[!UICONTROL Data]**&#x200B;选项卡，并查看&#x200B;**[!UICONTROL First-Party]**&#x200B;部分。
2. 向下滚动该页面，在&#x200B;**[!UICONTROL Imported Data]**&#x200B;下，您会找到&#x200B;**[!UICONTROL Adobe 1PD Tile]**。
3. 单击&#x200B;**[!UICONTROL Adobe 1PD]**&#x200B;图块，它将列出激活到您的广告商的[!DNL Trade Desk]目标的所有受众。 您还可以使用搜索功能。
4. Experience Platform中的区段ID #将显示为[!DNL Trade Desk] UI中的区段名称。

## 数据使用和治理 {#data-usage-governance}

在处理您的数据时，所有[!DNL Adobe Experience Platform]目标都符合数据使用策略。 有关[!DNL Adobe Experience Platform]如何实施数据治理的详细信息，请参阅[数据治理概述](/help/data-governance/home.md)。
