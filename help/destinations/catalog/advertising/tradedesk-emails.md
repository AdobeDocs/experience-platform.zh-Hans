---
title: (Beta)交易台 — CRM连接
description: 激活交易台帐户中的配置文件，以根据CRM数据进行受众定位和抑制。
last-substantial-update: 2023-01-25T00:00:00Z
exl-id: e09eaede-5525-4a51-a0e6-00ed5fdc662b
source-git-commit: 661ef040398a9e2ef8dd9cebdf7bd27d4268636b
workflow-type: tm+mt
source-wordcount: '1150'
ht-degree: 4%

---

# (Beta) [!DNL Trade Desk] - CRM连接

>[!IMPORTANT]
>
>[!DNL The Trade Desk - CRM] Platform中的目标当前为测试版。 文档和功能可能会发生更改。
>
>随着 EUID (European Unified ID) 的发布，现在您在[目标目录](/help/destinations/catalog/overview.md)中会看到两个 [!DNL The Trade Desk - CRM] 目标。
>* 如果您在欧盟获取数据，请使用 **[!DNL The Trade Desk - CRM (EU)]** 目标。
>* 如果您在 APAC 或 NAMER 地区获取数据，请使用 **[!DNL The Trade Desk - CRM (NAMER & APAC)]** 目标。
>
>Experience Platform中的两个目标当前均处于Beta版。 此目标连接器和文档页面由 *[!DNL Trade Desk]* 团队。 如有任何查询或更新请求，请联系 [!DNL Trade Desk] 代表，文档和功能可能会发生更改。

## 概述 {#overview}

本文档旨在帮助您向激活配置文件 [!DNL Trade Desk] 帐户基于CRM数据进行受众定位和隐藏。

[!DNL The Trade Desk(TTD)] 不会随时直接处理电子邮件地址的上传文件，也不会 [!DNL The Trade Desk] 存储原始（未散列）电子邮件。

>[!TIP]
>
>使用 [!DNL The Trade Desk] CRM数据映射的CRM目标，如电子邮件或哈希电子邮件地址。 使用 [其他交易台目标](/help/destinations/catalog/advertising/tradedesk.md) Adobe Experience Platform目录中的Cookie和设备ID映射。

## 先决条件 {#prerequisites}

在将受众激活到之前 [!DNL The Trade Desk]，您必须联系 [!DNL The Trade Desk] 客户经理签署CRM载入合同。 [!DNL The Trade Desk] 将授予权限并共享您的广告商ID以配置您的目标。

## ID匹配要求 {#id-matching-requirements}

根据您摄取到Adobe Experience Platform中的ID类型，您必须遵守其相应的要求。 请阅读 [身份命名空间概述](/help/identity-service/namespaces.md) 以了解更多信息。

## 支持的身份 {#supported-identities}

[!DNL The Trade Desk] 支持激活下表中描述的标识。 了解有关 [身份](/help/identity-service/namespaces.md).

Adobe Experience Platform支持纯文本和SHA256哈希电子邮件地址。 按照ID匹配要求部分中的说明进行操作，并分别将适当的命名空间用于纯文本和经过哈希处理的电子邮件地址。

| 目标身份 | 描述 | 注意事项 |
|---|---|---|
| 电子邮件 | 电子邮件地址（明文） | 输入 `email` 作为目标身份（当源身份是电子邮件命名空间或属性时）。 |
| Email_LC_SHA256 | 电子邮件地址需要使用SHA256和小写进行哈希处理。 请务必遵循任意 [电子邮件标准化](https://github.com/UnifiedID2/uid2docs/tree/main/api#email-address-normalization) 需要规则。 您以后将无法更改此设置。 | 输入 `hashed_email` 作为目标身份，前提是您的源身份是Email_LC_SHA256命名空间或属性。 |

{style="table-layout:auto"}

## 电子邮件哈希处理要求 {#hashing-requirements}

您可以在将电子邮件地址摄取到Adobe Experience Platform中之前对其进行哈希处理，或者使用原始电子邮件地址。

要了解如何在Experience Platform中引入电子邮件地址，请参阅 [批量摄取概述](/help/ingestion/batch-ingestion/overview.md).

如果选择自己对电子邮件地址进行哈希处理，请确保符合以下要求：

* 删除前导空格和尾随空格。
* 将所有ASCII字符转换为小写。
* 在 `gmail.com` 电子邮件地址，从电子邮件地址的用户名部分删除以下字符：
   * 句点(. （ASCII代码46）。 例如，标准化 `jane.doe@gmail.com` 到 `janedoe@gmail.com`.
   * 加号(+ （ASCII代码43）)和所有后续字符。 例如，标准化 `janedoe+home@gmail.com` 到 `janedoe@gmail.com`.

## 导出类型和频率 {#export-type-frequency}

有关目标导出类型和频率的信息，请参阅下表。

| 项目 | 类型 | 注释 |
---------|----------|---------|
| 导出类型 | **[!UICONTROL 受众导出]** | 您正在导出具有在交易台目标中使用的标识符（电子邮件或哈希电子邮件）的受众的所有成员。 |
| 导出频率 | **[!UICONTROL 每日批次]** | 由于配置文件是根据受众评估在Experience Platform中进行更新的，因此配置文件（身份）每天会更新一次以流向目标平台。 详细了解 [批量导出](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## 连接到目标 {#connect}

### 验证目标 {#authenticate}

[!DNL The Trade Desk] CRM目标是每天上传批量文件，不需要用户进行身份验证。

### 填写目标详细信息 {#fill-in-details}

在将受众数据发送到或激活到目标之前，您必须先设置与自己的目标平台的连接。 同时 [设置](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html?lang=en) 此目标必须提供以下信息：

* **[!UICONTROL 帐户类型]**：请选择 **[!UICONTROL 现有帐户]** 选项。
* **[!UICONTROL 名称]**：将来用于识别此目标的名称。
* **[!UICONTROL 描述]**：可帮助您将来识别此目标的描述。
* **[!UICONTROL 广告商ID]**：您的 [!DNL Trade Desk Advertiser ID]，可由您的 [!DNL Trade Desk] 客户经理或位于下 [!DNL Advertiser Preferences] 在 [!DNL Trade Desk] UI。

![显示如何填写目标详细信息的平台UI屏幕截图。](/help/destinations/assets/catalog/advertising/tradedesk/configuredestination2.png)

连接到目标时，设置数据管理策略是完全可选的。 请查看Experience Platform [数据治理概述](/help/data-governance/policies/overview.md) 以了解更多详细信息。

## 将受众激活到此目标 {#activate}

>[!IMPORTANT]
> 
>* 要激活数据，您需要 **[!UICONTROL 管理目标]**， **[!UICONTROL 激活目标]**， **[!UICONTROL 查看配置文件]**、和 **[!UICONTROL 查看区段]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或与产品管理员联系以获取所需的权限。
>* 要导出 *身份*，您需要 **[!UICONTROL 查看身份图]** [访问控制权限](/help/access-control/home.md#permissions). <br> ![选择工作流中突出显示的身份命名空间以将受众激活到目标。](/help/destinations/assets/overview/export-identities-to-destination.png "选择工作流中突出显示的身份命名空间以将受众激活到目标。"){width="100" zoomable="yes"}

读取 [将受众数据激活到批量配置文件导出目标](/help/destinations/ui/activate-batch-profile-destinations.md) 有关将受众激活到目标的说明。

在 **[!UICONTROL 正在计划]** 页面上，您可以为要导出的每个受众配置计划和文件名。 配置时间表是强制性的，但配置文件名是可选的。

![用于安排受众激活的平台UI屏幕截图。](/help/destinations/assets/catalog/advertising/tradedesk/schedulesegment1.png)

>[!NOTE]
>
>所有受众已激活到 [!DNL The Trade Desk] CRM目标会自动设置为每日频率和完整文件导出。

![用于安排受众激活的平台UI屏幕截图。](/help/destinations/assets/catalog/advertising/tradedesk/schedulesegment2.png)

在 **[!UICONTROL 映射]** 页上，必须从source列中选择属性或身份命名空间并映射到目标列。

![用于映射受众激活的平台UI屏幕截图。](/help/destinations/assets/catalog/advertising/tradedesk/mappingsegment1.png)

下面是将受众激活到时的正确标识映射示例 [!DNL The Trade Desk] CRM目标。

>[!IMPORTANT]
>
> [!DNL The Trade Desk] CRM目标不接受原始和经过哈希处理的电子邮件地址作为同一激活流中的身份。 为原始电子邮件地址和经过哈希处理的电子邮件地址创建单独的激活流程。

选择源字段：

* 选择 `Email` 如果在数据摄取时使用原始电子邮件地址，则使用命名空间或属性作为源身份。
* 选择 `Email_LC_SHA256` 如果对数据摄取到Platform中的客户电子邮件地址进行哈希处理，则使用命名空间或属性作为源身份。

选择目标字段：

* 输入  `email` 当源命名空间或属性为 `Email`.
* 输入  `hashed_email` 当源命名空间或属性为 `Email_LC_SHA256`.

## 验证数据导出 {#validate}

验证数据是否已正确地从Experience Platform导出并导出到 [!DNL The Trade Desk]，请在Adobe1PD数据拼贴下找到受众 [!DNL The Trade Desk] 数据管理平台(DMP)。 以下是查找中的相应ID的步骤 [!DNL Trade Desk] UI：

1. 首先，单击 **[!UICONTROL 数据]** 制表符和复查 **[!UICONTROL 第一方]**.
2. 向下滚动页面，在下 **[!UICONTROL 导入的数据]**，您将找到 **[!UICONTROL Adobe1PD磁贴]**.
3. 单击**[!UICONTROL Adobe1PD]**图块，它将列出激活到 [!DNL Trade Desk] 广告商的目标。 您还可以使用搜索功能。
4. Experience Platform中的区段ID #将显示为以下位置中的区段名称： [!DNL Trade Desk] UI。

## 数据使用和治理 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 目标在处理您的数据时符合数据使用策略。 有关如何执行操作的详细信息 [!DNL Adobe Experience Platform] 强制执行数据管理，请参见 [数据管理概述](/help/data-governance/home.md).
