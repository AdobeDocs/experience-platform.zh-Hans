---
title: 交易台 — CRM连接
description: 激活交易台帐户中的配置文件，以根据CRM数据进行受众定位和抑制。
last-substantial-update: 2025-01-16T00:00:00Z
exl-id: e09eaede-5525-4a51-a0e6-00ed5fdc662b
source-git-commit: 47d4078acc73736546d4cbb2d17b49bf8945743a
workflow-type: tm+mt
source-wordcount: '1643'
ht-degree: 2%

---

# [!DNL Trade Desk] - CRM连接

>[!IMPORTANT]
>
>[目标目录](/help/destinations/catalog/overview.md)中有两个交易台 — CRM目标。
>
>* 如果您在欧盟境内收集数据，请使用&#x200B;**[!DNL The Trade Desk - CRM (EU)]**&#x200B;目标。
>* 如果您在APAC或NAMER区域获取数据，请使用&#x200B;**[!DNL The Trade Desk - CRM (NAMER & APAC)]**&#x200B;目标。
>
>此目标连接器和文档页面由&#x200B;*[!DNL Trade Desk]*&#x200B;团队创建和维护。 有关查询或更新请求，请联系您的[!DNL Trade Desk]代表。

## 概述 {#overview}

了解如何根据CRM数据向[!DNL Trade Desk]帐户激活配置文件以进行受众定位和抑制。

此连接器将数据发送到[!DNL The Trade Desk]以进行第一方数据激活。 [!DNL The Trade Desk]存储您的原始（未散列）电子邮件和电话号码。

>[!TIP]
>
>使用[!DNL The Trade Desk - CRM]目标发送CRM数据（如电子邮件和电话号码）和其他第一方数据标识符（如Cookie和设备ID）。 您可以继续将Experience Platform目录中的[交易台目标](/help/destinations/catalog/advertising/tradedesk.md)用于Cookie和设备ID映射。

## 先决条件 {#prerequisites}

>[!IMPORTANT]
>
>在激活交易台受众之前，必须联系[!DNL Trade Desk]客户经理以启用该功能。 如果您要发送电子邮件、电话号码和UID2/EUID，则必须与[!DNL The Trade Desk]共享已签名的UID2/EUID协议。

## ID匹配要求 {#id-matching-requirements}

根据您摄取到Adobe Experience Platform中的ID类型，您必须遵守其相应的要求。 有关详细信息，请阅读[身份命名空间概述](/help/identity-service/features/namespaces.md)。

## 支持的身份 {#supported-identities}

[!DNL The Trade Desk]支持激活下表中描述的标识。 了解有关[标识](/help/identity-service/features/namespaces.md)的更多信息。

Adobe Experience Platform支持未哈希和哈希处理的电子邮件地址和电话号码。 按照ID匹配要求部分中的说明进行操作，并分别将适当的命名空间用于纯文本和经过哈希处理的电子邮件地址。

| 目标身份 | 描述 |
|---|---|
| 电子邮件 | 电子邮件地址（明文） |
| Email_LC_SHA256 | 电子邮件地址需要使用SHA256和小写进行哈希处理。 您以后将无法更改此设置。 |
| 电话(E.164) | 需要以E.164格式规范化的电话号码。 E.164格式包括加号(+)、国际国家/地区呼叫代码、本地区号和电话号码。 例如：(+)（国家代码）（区号）（电话号码）。 此标识符不适用于交易台 — 第一方数据(EU)。 |
| 电话(SHA256_E.164) | 已经标准化为E.164格式，然后使用SHA-256进行哈希处理的电话号码，生成的哈希值为Base64-encoded。 此标识符不适用于交易台 — 第一方数据(EU)。 |
| TDID | 交易台中的Cookie ID |
| GAID | GOOGLE ADVERTISING ID |
| IDFA | 广告商的Apple ID |
| UID2 | 原始UID2值 |
| UID2Token | 加密的UID2令牌，也称为广告令牌。 |
| EUID | 原始欧盟ID值 |
| EUIDToken | 加密的EUID令牌，也称为广告令牌。 |
| RampID | 49个字符或70个字符的RampID（以前称为IdentityLink或IDL）。 这必须是专门为交易台映射的LiveRamp中的RampID。 |
| netid | 用户的netID，作为70个字符的base64编码字符串。 此ID仅在欧洲受支持。 |
| 第一ID | 用户的First-id，这是法国出版商通常设置的第一方Cookie。 此ID仅在欧洲受支持。 |

{style="table-layout:auto"}

## 电子邮件哈希处理要求 {#email-hashing}

您可以在将电子邮件地址摄取到Adobe Experience Platform中之前对其进行哈希处理，或者使用原始电子邮件地址。

要了解如何在Experience Platform中摄取电子邮件地址，请阅读[批次摄取概述](/help/ingestion/batch-ingestion/overview.md)。

如果选择自己对电子邮件地址进行哈希处理，请确保符合以下要求：

* 删除前导空格和尾随空格。
* 将所有ASCII字符转换为小写。
* 在`gmail.com`电子邮件地址中，从电子邮件地址的用户名部分删除以下字符：

      *句点(“。”) 字符（ASCII代码46）。 例如，将“jane.doe@gmail.com”标准化为“janedoe@gmail.com”。
     *加号(“+”)字符（ASCII代码43）和所有后续字符。 例如，将“janedoe+home@gmail.com”标准化为“janedoe@gmail.com”。
  

## 电话号码规范化和哈希处理要求 {#phone-hashing}

以下是关于上传电话号码的须知信息：

* 无论是在请求中发送经过哈希处理还是未经哈希处理的电话号码，在请求中发送电话号码之前都必须对其进行标准化。
* 要上传规范化、哈希化和编码的数据，您必须将电话号码作为规范化电话号码的Base64编码SHA-256哈希发送。

无论您是要上传原始电话号码还是经过哈希处理的电话号码，都必须将其规范化。

>[!IMPORTANT]
>
>哈希处理前的标准化可以确保生成的ID值始终相同，并且数据可以准确匹配。

以下是您需要了解的有关电话号码标准化要求的内容：

* UID2运营商接受E.164格式的电话号码，这是确保全球唯一性的国际电话号码格式。
* E.164电话号码最多可有15位。
* 规范化E.164电话号码使用以下语法： `[+][country code][subscriber number including area code]`不含空格、连字符、括号或其他特殊字符。 下面是一些示例：

      *美国： 1 (234) 567-8901被标准化为+12345678901。
     *新加坡： 65 1243 5678已标准化为+6512345678。
     *澳大利亚：手机号码0491 570 006已规范化，添加国家/地区代码并去除前导零： +61491570006。
     *英国：手机号码07812 345678已标准化，以添加国家/地区代码并丢弃前导零： +447812345678。
  
确保规范化的电话号码是UTF-8，而不是其他编码系统，如UTF-16。

电话号码哈希是规范化电话号码的Base64编码SHA-256哈希。 首先规范化电话号码，然后使用SHA-256散列算法进行散列，然后使用Base64编码对散列值的结果字节进行编码。 请注意，Base64编码应用于哈希值的字节，而不是十六进制编码的字符串表示形式。
下表显示了一个简单输入电话号码的示例，并在应用每个步骤时获得一个安全、不透明的值。

| 类型 | 示例 | 注释和使用情况 |
|---|---|---|
| 原始电话号码 | 1 (234) 567-8901 | 这是起点。 |
| 规范化的电话号码 | +12345678901 | 标准化始终是第一步。 |
| 规范化电话号码的SHA-256哈希值 | 10e6f0b47054a83359477dcb35231db6de5c69fb1816e1a6b98e192de9e5b9ee | 此64个字符的字符串是32字节SHA-256的十六进制编码表示形式。 |
| 规范化和散列电话号码的十六进制到Base64 SHA-256编码 | EObwtHBUqDNZR33LNSMdtt5cafsYFuGmuY4ZLenlue4 | 此44字符字符串是32字节SHA-256的Base64编码表示形式。 SHA-256哈希为十六进制值。 必须使用采用十六进制值作为输入的Base64编码器。 对请求正文中发送的phone_hash值使用此编码。 |

>[!IMPORTANT]
>
>应用Base64编码时，请确保使用接受十六进制值作为输入的函数。 如果您使用接受文本作为输入的函数，则结果会是一个较长的字符串，并且对于UID2而言，该字符串无效。

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

选择源字段和目标字段：

| 源字段 | 目标字段 |
|---|---|
| 电子邮件 | 电子邮件 |
| Email_LC_SHA256 | hashed_email |
| 电话(E.164) | 电话 |
| 电话(SHA256_E.164) | hashed_phone |
| TDID | tdid |
| GAID | daid |
| IDFA | idfa |
| UID2 | uid2 |
| UID2Token | uid2_token |
| EUID | euid |
| EUIDToken | euid_token |
| RampID | idl |
| ID5 | id5 |
| netid | net_id |
| 第一ID | first_id |


## 验证数据导出 {#validate}

要验证数据是否已从Experience Platform正确导出到[!DNL The Trade Desk]，请在[!DNL The Trade Desk]“广告商数据和标识”库的“Adobe 1PD”选项卡下找到受众。 以下是在[!DNL Trade Desk] UI中查找相应ID的步骤：

1. 首先，选择&#x200B;**[!UICONTROL Libraries]**&#x200B;选项卡，并查看&#x200B;**[!UICONTROL Advertiser data and identity]**&#x200B;部分。
2. 单击&#x200B;**[!UICONTROL Adobe 1PD]**，它将列出激活到[!DNL The Trade Desk]的所有受众。
3. Experience Platform中的区段名称或区段ID将显示为[!DNL Trade Desk] UI中的区段名称。

## 数据使用和治理 {#data-usage-governance}

在处理您的数据时，所有[!DNL Adobe Experience Platform]目标都符合数据使用策略。 有关[!DNL Adobe Experience Platform]如何实施数据治理的详细信息，请参阅[数据治理概述](/help/data-governance/home.md)。
