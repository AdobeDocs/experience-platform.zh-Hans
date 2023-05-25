---
title: (Beta)交易台 — CRM连接
description: 将配置文件激活到您的交易台帐户，以便根据CRM数据进行受众定位和抑制。
last-substantial-update: 2023-01-25T00:00:00Z
exl-id: e09eaede-5525-4a51-a0e6-00ed5fdc662b
source-git-commit: 83778bc5d643f69e0393c0a7767fef8a4e8f66e9
workflow-type: tm+mt
source-wordcount: '1078'
ht-degree: 0%

---

# (Beta) [!DNL Trade Desk] - CRM连接

>[!IMPORTANT]
>
>[!DNL The Trade Desk - CRM] Platform中的目标当前为测试版。 文档和功能可能会发生更改。
>
>随着EUID (European Unified ID)的发布，您现在可以看到两个 [!DNL The Trade Desk - CRM] 中的目标 [目标目录](/help/destinations/catalog/overview.md).
>* 如果您从欧盟地区获取数据，请使用 **[!DNL The Trade Desk - CRM (EU)]** 目标。
>* 如果您在APAC或NAMER地区获取数据，请使用 **[!DNL The Trade Desk - CRM (NAMER & APAC)]** 目标。
>
>Experience Platform中的两个目标当前均处于测试阶段。 此文档页面由创建 *[!DNL Trade Desk]* 团队。 如有任何查询或更新请求，请联系 [!DNL Trade Desk] 代表，文档和功能可能会发生更改。

## 概述 {#overview}

本文档旨在帮助您将配置文件激活到 [!DNL Trade Desk] 用于基于CRM数据的受众定位和禁止的帐户。

[!DNL The Trade Desk(TTD)] 不会随时直接处理电子邮件地址的上传文件，也不会 [!DNL The Trade Desk] 存储原始（未哈希处理的）电子邮件。

>[!TIP]
>
>使用 [!DNL The Trade Desk] CRM数据映射的CRM目标，如电子邮件或哈希电子邮件地址。 使用 [其他交易台目标](/help/destinations/catalog/advertising/tradedesk.md) 用于Cookie和设备ID映射的Adobe Experience Platform目录中。

## 先决条件 {#prerequisites}

在将区段激活到之前 [!DNL The Trade Desk]，您必须联系 [!DNL The Trade Desk] 客户经理签署CRM入门培训合同。 [!DNL The Trade Desk] 将授予权限并共享您的广告商ID以配置您的目标。

## ID匹配要求 {#id-matching-requirements}

根据您摄取到Adobe Experience Platform中的ID类型，您必须遵守其相应的要求。 请阅读 [身份命名空间概述](/help/identity-service/namespaces.md) 了解更多信息。

## 支持的身份 {#supported-identities}

[!DNL The Trade Desk] 支持激活下表中描述的标识。 详细了解 [身份](/help/identity-service/namespaces.md).

Adobe Experience Platform支持纯文本和SHA256哈希电子邮件地址。 按照ID匹配要求部分中的说明进行操作，并分别将适当的命名空间用于纯文本和经过哈希处理的电子邮件地址。

| 目标身份 | 描述 | 注意事项 |
|---|---|---|
| 电子邮件 | 电子邮件地址（纯文本） | 输入 `email` 当源身份是电子邮件命名空间或属性时作为目标身份。 |
| Email_LC_SHA256 | 电子邮件地址需要使用SHA256和小写进行哈希处理。 请务必遵循任意 [电子邮件标准化](https://github.com/UnifiedID2/uid2docs/tree/main/api#email-address-normalization) 需要规则。 您以后将无法更改此设置。 | 输入 `hashed_email` 当源身份是Email_LC_SHA256命名空间或属性时作为目标身份。 |

{style="table-layout:auto"}

## 电子邮件哈希处理要求 {#hashing-requirements}

您可以在将电子邮件地址摄取到Adobe Experience Platform中之前对其进行哈希处理，或者使用原始电子邮件地址。

要了解如何在Experience Platform中摄取电子邮件地址，请阅读 [批量摄取概述](/help/ingestion/batch-ingestion/overview.md).

如果您选择自己对电子邮件地址进行哈希处理，请确保符合以下要求：

* 删除前导空格和尾随空格。
* 将所有ASCII字符转换为小写。
* In `gmail.com` 电子邮件地址，从电子邮件地址的用户名部分删除以下字符：
   * 句点(. （ASCII代码46）。 例如，标准化 `jane.doe@gmail.com` 到 `janedoe@gmail.com`.
   * 加号(+ （ASCII代码43）)和所有后续字符。 例如，标准化 `janedoe+home@gmail.com` 到 `janedoe@gmail.com`.

## 导出类型和频率 {#export-type-frequency}

有关目标导出类型和频率的信息，请参阅下表。

| 项目 | 类型 | 注释 |
---------|----------|---------|
| 导出类型 | **[!UICONTROL 区段导出]** | 您正在导出区段（受众）的所有成员，其中包含交易台目标中使用的标识符（电子邮件或哈希电子邮件）。 |
| 导出频率 | **[!UICONTROL 每日批次]** | 由于配置文件是根据区段评估在Experience Platform中更新的，因此配置文件（身份）每天都会更新一次，以流向目标平台。 详细了解 [批量导出](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## 连接到目标 {#connect}

### 向目标进行身份验证 {#authenticate}

[!DNL The Trade Desk] CRM目标是每天批量上传文件，不需要用户进行身份验证。

### 填写目标详细信息 {#fill-in-details}

在将受众数据发送到或激活到目标之前，您必须先设置与自己的目标平台的连接。 While [设置](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html?lang=en) 必须提供以下信息，才能使用此目标：

* **[!UICONTROL 帐户类型]**：请选择 **[!UICONTROL 现有帐户]** 选项。
* **[!UICONTROL 名称]**：将来用于识别此目标的名称。
* **[!UICONTROL 描述]**：可帮助您将来识别此目标的描述。
* **[!UICONTROL 广告商ID]**：您的 [!DNL Trade Desk Advertiser ID]，可以由您的 [!DNL Trade Desk] 客户经理或位于以下位置： [!DNL Advertiser Preferences] 在 [!DNL Trade Desk] UI。

![显示如何填写目标详细信息的Platform UI屏幕快照。](/help/destinations/assets/catalog/advertising/tradedesk/configuredestination2.png)

连接到目标时，设置数据治理策略是完全可选的。 请查看Experience Platform [数据治理概述](/help/data-governance/policies/overview.md) 了解更多详细信息。

## 将区段激活到此目标 {#activate}

读取 [将受众数据激活到批量配置文件导出目标](/help/destinations/ui/activate-batch-profile-destinations.md) 有关将受众区段激活到目标的说明。

在 **[!UICONTROL 计划]** 页面上，您可以为要导出的每个区段配置计划和文件名。 必须配置计划，但可以选择是否配置文件名。

![用于计划区段激活的平台UI屏幕快照。](/help/destinations/assets/catalog/advertising/tradedesk/schedulesegment1.png)

>[!NOTE]
>
>所有区段均激活至 [!DNL The Trade Desk] CRM目标会自动设置为每日频率和完整文件导出。

![用于计划区段激活的平台UI屏幕快照。](/help/destinations/assets/catalog/advertising/tradedesk/schedulesegment2.png)

在 **[!UICONTROL 映射]** 页上，您必须从源列中选择属性或身份命名空间并映射到目标列。

![用于映射区段激活的平台UI屏幕快照。](/help/destinations/assets/catalog/advertising/tradedesk/mappingsegment1.png)

下面是激活区段到时正确的标识映射示例 [!DNL The Trade Desk] CRM目标。

>[!IMPORTANT]
>
> [!DNL The Trade Desk] CRM目标不接受原始和经过哈希处理的电子邮件地址作为同一激活流中的身份。 为原始电子邮件地址和经过哈希处理的电子邮件地址创建单独的激活流程。

选择源字段：

* 选择 `Email` 如果在数据摄取时使用原始电子邮件地址，则使用命名空间或属性作为源身份。
* 选择 `Email_LC_SHA256` 如果在数据摄取到Platform时为客户电子邮件地址进行了哈希处理，则使用命名空间或属性作为源身份。

选择目标字段：

* 输入  `email` 当源命名空间或属性为 `Email`.
* 输入  `hashed_email` 当源命名空间或属性为 `Email_LC_SHA256`.

## 验证数据导出 {#validate}

验证数据是否已正确地从Experience Platform导出并导出到 [!DNL The Trade Desk]，请在Adobe1PD数据拼贴下找到区段 [!DNL The Trade Desk] 数据管理平台(DMP)。 以下是在中找到相应ID的步骤 [!DNL Trade Desk] UI：

1. 首先，单击 **[!UICONTROL 数据]** 选项卡，然后查看 **[!UICONTROL 第一方]**.
2. 向下滚动页面，在下 **[!UICONTROL 导入的数据]**，您将找到 **[!UICONTROL Adobe1PD磁贴]**.
3. 单击**[!UICONTROL Adobe1PD]**图块，它将列出激活到的所有区段 [!DNL Trade Desk] 广告商的目标。 您还可以使用搜索功能。
4. Experience Platform中的区段ID #将显示为中的区段名称， [!DNL Trade Desk] UI。

## 数据使用和管理 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 目标在处理您的数据时符合数据使用策略。 有关以下方面的详细信息： [!DNL Adobe Experience Platform] 强制执行数据管理，请参见 [数据治理概述](/help/data-governance/home.md).
