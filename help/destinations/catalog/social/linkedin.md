---
keywords: linkedin连接；linkedin连接；linkedin目标；linkedin;
title: Linkedin匹配的受众连接
description: 根据经过哈希处理的电子邮件，激活LinkedIn营销活动的用户档案以进行受众定位、个性化和抑制。
exl-id: 74c233e9-161a-4e4a-98ef-038a031feff0
source-git-commit: c5d2427635d90f3a9551e2a395d01d664005e8bc
workflow-type: tm+mt
source-wordcount: '834'
ht-degree: 2%

---

# [!DNL LinkedIn Matched Audiences] 连接

## 概述 {#overview}

为 [!DNL LinkedIn] 基于经过哈希处理的电子邮件和移动ID的受众定位、个性化和抑制促销活动。

![linkedInAdobe Experience Platform UI中的目标](../../assets/catalog/social/linkedin/catalog.png)

## 用例

以帮助您更好地了解如何以及何时使用 [!DNL LinkedIn Matched Audiences] 目标，以下是Adobe Experience Platform客户可以使用此功能解决的用例。

软件公司组织会议并希望与参与者保持联系，并根据他们的会议出席状态向他们展示个性化的优惠。 公司可以从自己的网站中摄取电子邮件地址或移动设备ID [!DNL CRM] 进入Adobe Experience Platform。 然后，他们可以根据自己的离线数据构建区段，并将这些区段发送到 [!DNL LinkedIn] 社交平台，优化广告支出。

## 支持的身份 {#supported-identities}

[!DNL LinkedIn Matched Audiences] 支持激活下表所述的身份。 详细了解 [标识](/help/identity-service/namespaces.md).

| Target标识 | 描述 | 注意事项 |
|---|---|---|
| GAID | Google Advertising ID | 如果源标识是GAID命名空间，请选择此目标标识。 |
| IDFA | Apple ID for Advertisers | 如果源标识是IDFA命名空间，请选择此目标标识。 |
| email_lc_sha256 | 使用SHA256算法进行哈希处理的电子邮件地址 | Adobe Experience Platform支持纯文本和SHA256哈希电子邮件地址。 按照 [ID匹配要求](#id-matching-requirements-id-matching-requirements) 部分，并分别将相应的命名空间用于纯文本和经过哈希处理的电子邮件。 当源字段包含未哈希属性时，请检查 **[!UICONTROL 应用转换]** 选项， [!DNL Platform] 自动对激活时的数据进行哈希处理。 |

{style=&quot;table-layout:auto&quot;}

## 导出类型和频度 {#export-type-frequency}

有关目标导出类型和频率的信息，请参阅下表。

| 项目 | 类型 | 注释 |
---------|----------|---------|
| 导出类型 | **[!UICONTROL 区段导出]** | 您要导出区段（受众）的所有成员，以及 [!DNL LinkedIn Matched Audiences] 目标。 |
| 导出频度 | **[!UICONTROL 流]** | 流目标“始终运行”基于API的连接。 在基于区段评估的Experience Platform中更新用户档案后，连接器会立即将更新发送到目标平台下游。 有关更多信息 [流目标](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## linkedIn帐户先决条件 {#LinkedIn-account-prerequisites}

在使用 [!UICONTROL linkedIn匹配受众] 目标，确保 [!DNL LinkedIn Campaign Manager] 帐户具有 [!DNL Creative Manager] 权限级别或更高级别。

了解如何编辑 [!DNL LinkedIn Campaign Manager] 用户权限，请参阅 [添加、编辑和删除广告帐户的用户权限](https://www.linkedin.com/help/lms/answer/5753) (在LinkedIn文档中)。

## ID匹配要求 {#id-matching-requirements}

[!DNL LinkedIn Matched Audiences] 要求不要发送任何个人身份信息(PII)。 因此，激活的受众 [!DNL LinkedIn Matched Audiences] 可以锁上 *哈希* 标识符，如电子邮件地址或移动设备ID。

根据您摄取到Adobe Experience Platform中的ID类型，您必须遵循其相应要求。

## 电子邮件哈希处理要求 {#email-hashing-requirements}

您可以在将电子邮件地址摄取到Adobe Experience Platform之前对其进行哈希处理，或者在Experience Platform中明确使用电子邮件地址，并且 [!DNL Platform] 在激活时对它们进行哈希处理。

要了解如何在Experience Platform中摄取电子邮件地址，请参阅 [批量摄取概述](/help/ingestion/batch-ingestion/overview.md) 和 [流摄取概述](/help/ingestion/streaming-ingestion/overview.md).

如果您选择自行对电子邮件地址进行哈希处理，请确保符合以下要求：

* 从电子邮件字符串中裁切所有前导和尾随空格。 例如： `johndoe@example.com`，否 `<space>johndoe@example.com<space>`;
* 对电子邮件字符串进行哈希处理时，请确保对小写字符串进行哈希处理；
   * 示例： `example@email.com`，否 `EXAMPLE@EMAIL.COM`;
* 确保经过哈希处理的字符串全部为小写
   * 示例： `55e79200c1635b37ad31a378c39feb12f120f116625093a19bc32fff15041149`，否 `55E79200C1635B37AD31A378C39FEB12F120F116625093A19bC32FFF15041149`;
* 不要加盐。

>[!NOTE]
>
>来自未哈希命名空间的数据将由自动进行哈希处理 [!DNL Platform] 激活时。
> 属性源数据不会自动进行哈希处理。
> 
> 在 [身份映射](../../ui/activate-segment-streaming-destinations.md#mapping) 步骤，当源字段包含未哈希属性时，请检查 **[!UICONTROL 应用转换]** 选项， [!DNL Platform] 自动对激活时的数据进行哈希处理。
> 
> 的 **[!UICONTROL 应用转换]** 选择属性作为源字段时，才会显示选项。 选择命名空间时，不会显示该参数。

![身份映射转换](../../assets/ui/activate-destinations/identity-mapping-transformation.png)

## 连接到目标 {#connect}

要连接到此目标，请按照 [目标配置教程](../../ui/connect-destination.md).

以下视频还演示了配置 [!DNL LinkedIn Matched Audiences] 目标和激活区段。

>[!VIDEO](https://video.tv.adobe.com/v/332599/?quality=12&learn=on&captions=eng)

>[!NOTE]
>
>Experience Platform用户界面经常更新，自此视频录制以来可能已发生更改。 有关最新信息，请参阅 [目标配置教程](../../ui/connect-destination.md).

### 连接参数 {#parameters}

While [设置](../../ui/connect-destination.md) 此目标中，您必须提供以下信息：

* **[!UICONTROL 名称]**:一个名称，您将在将来通过此名称来识别此目标。
* **[!UICONTROL 描述]**:此描述将帮助您在将来确定此目标。
* **[!UICONTROL 帐户ID]**:您的 [!DNL LinkedIn Campaign Manager Account ID]. 您可以在 [!DNL LinkedIn Campaign Manager] 帐户。

## 将区段激活到此目标 {#activate}

请参阅 [将受众数据激活到流区段导出目标](../../ui/activate-segment-streaming-destinations.md) 有关将受众区段激活到此目标的说明。

## 导出的数据 {#exported-data}

成功激活表示 [!DNL LinkedIn] 自定义受众将在 [[!DNL LinkedIn Campaign Manager]](https://www.linkedin.com/campaignmanager/login). 由于用户符合激活区段的资格条件或被取消资格，因此将会添加和删除受众中的区段成员资格。

>[!TIP]
>
>Adobe Experience Platform与 [!DNL LinkedIn Matched Audiences] 支持历史受众回填。 所有历史区段资格都将发送到 [!DNL LinkedIn] 在您将区段激活到目标时。
