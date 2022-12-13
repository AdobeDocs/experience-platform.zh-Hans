---
title: （测试版）交易台 — CRM连接
description: 将用户档案激活到交易台帐户，以便根据CRM数据定位和抑制受众。
exl-id: e09eaede-5525-4a51-a0e6-00ed5fdc662b
source-git-commit: 38447348bc96b2f3f330ca363369eb423efea1c8
workflow-type: tm+mt
source-wordcount: '1041'
ht-degree: 2%

---

# （测试版） [!DNL Trade Desk] - CRM连接

>[!IMPORTANT]
>
> [!DNL The Trade Desk - CRM] 平台中的目标当前为测试版。 文档和功能可能会发生更改。

## 概述 {#overview}

>[!IMPORTANT]
>
> 此文档页面由 *[!DNL Trade Desk]* 团队。 如有任何查询或更新请求，请联系 [!DNL Trade Desk] 代表。

本文档旨在帮助您将用户档案激活到 [!DNL Trade Desk] 考虑基于CRM数据的受众定位和抑制。

>[!TIP]
>
>使用 [!DNL The Trade Desk] 用于CRM数据映射的CRM目标，如电子邮件或经过哈希处理的电子邮件地址。 使用 [其他交易台目的地](/help/destinations/catalog/advertising/tradedesk.md) 在Adobe Experience Platform目录中，用于cookie和设备ID映射。

[!DNL The Trade Desk] (TTD)不会随时直接处理电子邮件地址的上传文件，也不会 [!DNL The Trade Desk] 存储原始（未经过哈希处理）电子邮件。

## 先决条件 {#prerequisites}

在将区段激活到 [!DNL The Trade Desk]，您必须联系 [!DNL The Trade Desk] 客户经理来签署CRM载入合同。 [!DNL The Trade Desk] 然后，将授予权限并共享您的广告商ID以配置您的目标。

## ID匹配要求 {#id-matching-requirements}

根据您摄取到Adobe Experience Platform的ID类型，您必须遵循其相应要求。 请阅读 [身份命名空间概述](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=zh-Hans) 以了解更多信息。

## 支持的身份 {#supported-identities}

[!DNL The Trade Desk] 支持激活下表所述的身份。 详细了解 [标识](/help/identity-service/namespaces.md).

Adobe Experience Platform支持纯文本和SHA256哈希电子邮件地址。 按照ID匹配要求部分中的说明，并分别为纯文本和经过哈希处理的电子邮件地址使用相应的命名空间。

| Target标识 | 描述 | 注意事项 |
|---|---|---|
| 电子邮件 | 电子邮件地址（清除文本） | 选择 `Email` 源标识是电子邮件命名空间或属性时的目标标识。 |
| Email_LC_SHA256 | 电子邮件地址需要使用SHA256和小写进行哈希处理。 请务必遵循 [电子邮件标准化](https://github.com/UnifiedID2/uid2docs/tree/main/api#email-address-normalization) 规则。 以后将无法更改此设置。 | 选择 `Email_LC_SHA256` 当源标识是Email_LC_SHA256命名空间或属性时，即表示目标标识。 |

{style=&quot;table-layout:auto&quot;}

## 电子邮件哈希处理要求 {#hashing-requirements}

您可以在将电子邮件地址摄取到Adobe Experience Platform或使用原始电子邮件地址之前对其进行哈希处理。

要了解如何在Experience Platform中摄取电子邮件地址，请参阅 [批量摄取概述](https://experienceleague.adobe.com/docs/experience-platform/ingestion/batch/overview.html?lang=en).

如果您选择自行对电子邮件地址进行哈希处理，请确保符合以下要求：

* 删除前导和尾随空格。
* 将所有ASCII字符转换为小写。
* 在 `gmail.com` 电子邮件地址中，从电子邮件地址的用户名部分删除以下字符：
   * 句点(. （ASCII码46）。 例如，标准化 `jane.doe@gmail.com` to `janedoe@gmail.com`.
   * 加号(+（ASCII代码43）)和所有后续字符。 例如，标准化 `janedoe+home@gmail.com` to `janedoe@gmail.com`.

## 导出类型和频度 {#export-type-frequency}

有关目标导出类型和频率的信息，请参阅下表。

| 项目 | 类型 | 注释 |
---------|----------|---------|
| 导出类型 | **[!UICONTROL 区段导出]** | 您正在导出区段（受众）的所有成员，以及在交易台目标中使用的标识符（电子邮件或哈希电子邮件）。 |
| 导出频度 | **[!UICONTROL 每日批处理]** | 由于用户档案会根据区段评估在Experience Platform中更新，因此该用户档案（身份）每天会在目标平台的下游更新一次。 有关更多信息 [批量上传](https://experienceleague.adobe.com/docs/experience-platform/destinations/destination-types.html?lang=en#file-based). |

{style=&quot;table-layout:auto&quot;}

## 连接到目标 {#connect}

### 目标身份验证 {#authenticate}

[!DNL The Trade Desk] CRM目标是每日上传批处理文件，不需要用户进行身份验证。

### 填写目标详细信息 {#fill-in-details}

在向目标发送或激活受众数据之前，您必须设置与您自己的目标平台的连接。 While [设置](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html?lang=en) 此目标中，您必须提供以下信息：

* **[!UICONTROL 帐户类型]**:请选择 **[!UICONTROL 现有帐户]** 选项。
* **[!UICONTROL 名称]**:将来用于识别此目标的名称。
* **[!UICONTROL 描述]**:此描述将帮助您在将来确定此目标。
* **[!UICONTROL 广告商ID]**:您的 [!DNL Trade Desk Advertiser ID]，可由 [!DNL Trade Desk] 客户经理或可在 [!DNL Advertiser Preferences] 在 [!DNL Trade Desk] UI。

连接到目标时，设置数据管理策略是完全可选的。 请查看Experience Platform [数据管理概述](https://experienceleague.adobe.com/docs/experience-platform/data-governance/policies/overview.html?lang=en) 以了解更多详细信息。

## 将区段激活到此目标 {#activate}

请参阅 [将受众数据激活为批量配置文件导出目标](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations.html?lang=en) 有关将受众区段激活到目标的说明。

在 **[!UICONTROL 计划]** 页面，您可以配置要导出的每个区段的计划和文件名。 必须配置计划，但配置文件名是可选的。

>[!NOTE]
>
>激活到的所有区段 [!DNL The Trade Desk] CRM目标会自动设置为每日频率和完整文件导出。

在 **[!UICONTROL 映射]** 页面，则必须从源列中选择属性或身份命名空间，然后映射到目标列。

以下是将区段激活到 [!DNL The Trade Desk] CRM目标。

>[!IMPORTANT]
>
> [!DNL The Trade Desk] CRM目标不接受在同一激活流程中将原始电子邮件地址和经过哈希处理的电子邮件地址作为标识。 为原始电子邮件地址和经过哈希处理的电子邮件地址创建单独的激活流程。

选择源字段：

* 选择 `Email` 命名空间或属性作为源标识（如果在数据摄取中使用原始电子邮件地址）。
* 选择 `Email_LC_SHA256` 命名空间或属性作为源标识（如果您在将数据摄取到平台时对客户电子邮件地址进行哈希处理）。

选择目标字段：

* 选择 `Email` 命名空间作为目标标识（如果源命名空间或属性为） `Email`.
* 选择 `Email_LC_SHA256` 命名空间作为目标标识（如果源命名空间或属性为） `Email_LC_SHA256`.

## 验证数据导出 {#validate}

验证数据是否正确导出为Experience Platform外和 [!DNL The Trade Desk]，请在的Adobe1PD数据区块下找到区段 [!DNL The Trade Desk] 数据管理平台(DMP)。 以下是在 [!DNL Trade Desk] UI:

1. 首先，单击 **[!UICONTROL 数据]** 选项卡，并查看 **[!UICONTROL 第一方]**.
2. 向下滚动页面，在 **[!UICONTROL 导入的数据]**，您将找到 **[!UICONTROL Adobe1PD磁贴]**.
3. 单击**[!UICONTROL Adobe1PD]**拼贴，它会列出激活到的所有区段 [!DNL Trade Desk] 广告商的目标。 您还可以使用搜索函数。
4. Experience Platform中的区段ID #将在 [!DNL Trade Desk] UI。

## 数据使用和管理 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 目标在处理数据时与数据使用策略相兼容。 有关如何 [!DNL Adobe Experience Platform] 实施数据管理，请查看 [数据管理概述](/help/data-governance/home.md).
