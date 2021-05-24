---
keywords: linkedin连接；linkedin连接；linkedin目标；linkedin;
title: Linkedin匹配的受众连接
description: 根据经过哈希处理的电子邮件，激活LinkedIn营销活动的用户档案以进行受众定位、个性化和抑制。
exl-id: 74c233e9-161a-4e4a-98ef-038a031feff0
source-git-commit: 8ec6f1eb38f4865daaa4fe4cd749a9014742dce6
workflow-type: tm+mt
source-wordcount: '677'
ht-degree: 1%

---

# [!DNL LinkedIn Matched Audiences] 连接

## 概述 {#overview}

根据经过哈希处理的电子邮件和移动ID，激活[!DNL LinkedIn]营销活动的用户档案以进行受众定位、个性化和抑制。

![linkedInAdobe Experience Platform UI中的目标](../../assets/catalog/social/linkedin/catalog.png)

## 用例

为了帮助您更好地了解如何以及何时使用[!DNL LinkedIn Matched Audiences]目标，以下是Adobe Experience Platform客户可以使用此功能解决的用例。

软件公司组织会议并希望与参与者保持联系，并根据他们的会议出席状态向他们展示个性化的优惠。 公司可以将自己的[!DNL CRM]电子邮件地址或移动设备ID摄取到Adobe Experience Platform。 然后，他们可以根据自己的离线数据构建区段，并将这些区段发送到[!DNL LinkedIn]社交平台，从而优化广告支出。

## 支持的标识{#supported-identities}

[!DNL LinkedIn Matched Audiences] 支持激活下表所述的身份。了解有关[identities](/help/identity-service/namespaces.md)的更多信息。

| Target标识 | 描述 | 注意事项 |
|---|---|---|
| GAID | Google广告ID | 如果源标识是GAID命名空间，请选择此目标标识。 |
| IDFA | 适用于广告商的Apple ID | 如果源标识是IDFA命名空间，请选择此目标标识。 |
| email_lc_sha256 | 使用SHA256算法进行哈希处理的电子邮件地址 | Adobe Experience Platform支持纯文本和SHA256哈希电子邮件地址。 按照[ID匹配要求](#id-matching-requirements-id-matching-requirements)部分中的说明，分别对纯文本和经过哈希处理的电子邮件使用适当的命名空间。 当源字段包含未哈希属性时，请选中&#x200B;**[!UICONTROL Apply transformation]**&#x200B;选项，以使[!DNL Platform]在激活时自动对数据进行哈希处理。 |


## 导出类型{#export-type}

**区段导出**  — 您正在导出区段（受众）的所有成员，以及目标中使用的标识符（名称、电话号码和其他） [!DNL LinkedIn Matched Audiences] 。

## linkedIn帐户先决条件{#LinkedIn-account-prerequisites}

在使用[!UICONTROL LinkedIn匹配受众]目标之前，请确保您的[!DNL LinkedIn Campaign Manager]帐户具有[!DNL Creative Manager]权限级别或更高级别。

要了解如何编辑[!DNL LinkedIn Campaign Manager]用户权限，请参阅LinkedIn文档中的[添加、编辑和删除广告帐户的用户权限](https://www.linkedin.com/help/lms/answer/5753) 。

## ID匹配要求{#id-matching-requirements}

[!DNL LinkedIn Matched Audiences] 要求不要发送任何个人身份信息(PII)。因此，激活到[!DNL LinkedIn Matched Audiences]的受众可以与&#x200B;*哈希*&#x200B;标识符（如电子邮件地址或移动设备ID）关联。

根据您摄取到Adobe Experience Platform中的ID类型，您必须遵循其相应要求。

## 电子邮件哈希处理要求{#email-hashing-requirements}

您可以在将电子邮件地址摄取到Adobe Experience Platform之前对其进行哈希处理，或在Experience Platform中明确使用电子邮件地址，并在激活时对它们进行[!DNL Platform]哈希处理。

要了解如何在Experience Platform中摄取电子邮件地址，请参阅[批量摄取概述](/help/ingestion/batch-ingestion/overview.md)和[流摄取概述](/help/ingestion/streaming-ingestion/overview.md)。

如果您选择自行对电子邮件地址进行哈希处理，请确保符合以下要求：

- 从电子邮件字符串中裁切所有前导和尾随空格。 例如：`johndoe@example.com`，不是`<space>johndoe@example.com<space>`;
- 对电子邮件字符串进行哈希处理时，请确保对小写字符串进行哈希处理；
   - 示例：`example@email.com`，不是`EXAMPLE@EMAIL.COM`;
- 确保经过哈希处理的字符串全部为小写
   - 示例：`55e79200c1635b37ad31a378c39feb12f120f116625093a19bc32fff15041149`，不是`55E79200C1635B37AD31A378C39FEB12F120F116625093A19bC32FFF15041149`;
- 不要加盐。

>[!NOTE]
>
>未哈希命名空间中的数据在激活后由[!DNL Platform]自动进行哈希处理。
> 属性源数据不会自动进行哈希处理。
> 
> 在[身份映射](../../ui/activate-destinations.md#mapping)步骤中，当源字段包含未哈希属性时，请选中&#x200B;**[!UICONTROL Apply transformation]**&#x200B;选项，以使[!DNL Platform]在激活时自动对数据进行哈希处理。
> 
> 仅当选择属性作为源字段时，才会显示&#x200B;**[!UICONTROL Apply transformation]**&#x200B;选项。 选择命名空间时，不会显示该参数。

![身份映射转换](../../assets/ui/activate-destinations/identity-mapping-transformation.png)

## 连接到目标{#connect-destination}

要连接到[!DNL LinkedIn Matched Audiences]目标，请参阅[社交目标身份验证工作流](./workflow.md)。

以下视频还演示了配置[!DNL LinkedIn Matched Audiences]目标和激活区段的步骤。

>[!VIDEO](https://video.tv.adobe.com/v/332599/?quality=12&learn=on&captions=eng)

## 将区段激活到[!DNL LinkedIn Matched Audiences] {#activate-segments}

有关如何将区段激活到[!DNL LinkedIn Matched Audiences]的说明，请参阅[将数据激活到目标](../../ui/activate-destinations.md)。

## 导出的数据{#exported-data}

成功激活意味着将以编程方式在[[!DNL LinkedIn Campaign Manager]](https://www.linkedin.com/campaignmanager/login)中创建[!DNL LinkedIn]自定义受众。 由于用户符合激活区段的资格条件或被取消资格，因此将会添加和删除受众中的区段成员资格。

>[!TIP]
>
>Adobe Experience Platform与[!DNL LinkedIn Matched Audiences]之间的集成支持历史受众回填。 当您将区段激活到目标时，所有历史区段资格都会发送到[!DNL LinkedIn]。
