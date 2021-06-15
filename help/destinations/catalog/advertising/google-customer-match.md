---
keywords: Google客户匹配；Google客户匹配；Google客户匹配
title: Google客户匹配连接
description: Google客户匹配允许您使用在线和离线数据，通过Google自有资产和运营资产(如搜索、购物、Gmail和YouTube)来联系客户并与其重新互动。
exl-id: 8209b5eb-b05c-4ef7-9fdc-22a528d5f020
source-git-commit: da069c6c931bfd2af38b40fc061d5eb633aba9ea
workflow-type: tm+mt
source-wordcount: '1521'
ht-degree: 0%

---

# [!DNL Google Customer Match] 连接

## 概述 {#overview}

[Google客户](https://support.google.com/google-ads/answer/6379332?hl=en) 匹配功能允许您使用在线和离线数据，通过Google自有和运营的资产来联系和重新吸引客户，例如： [!DNL Search]、  [!DNL Shopping]、  [!DNL Gmail]和 [!DNL YouTube]。

![Adobe Experience Platform UI中的Google客户匹配目标](../../assets/catalog/advertising/google-customer-match/catalog.png)

## 用例

为了帮助您更好地了解如何以及何时使用[!DNL Google Customer Match]目标，以下是Adobe Experience Platform客户可以使用此功能解决的示例用例。

### 用例#1

运动服装品牌希望通过[!DNL Google Search]和[!DNL Google Shopping]联系现有客户，以根据其过去的购买和浏览历史个性化选件和项目。 服装品牌可以将电子邮件地址从自己的CRM摄取到Experience Platform，并根据自己的离线数据构建区段。 然后，他们可以将这些区段发送到[!DNL Google Customer Match]以用于[!DNL Search]和[!DNL Shopping]，从而优化其广告支出。

### 用例#2

一家知名科技公司推出了一款新手机。 为推广这款新型手机，他们希望将手机的新特性和功能提升到拥有其旧款手机的客户的认识。

要推广此版本，他们会将电子邮件地址从其CRM数据库上传到Experience Platform，并使用电子邮件地址作为标识符。 区段是根据拥有旧手机型号的客户创建的。 然后，区段会发送到[!DNL Google Customer Match]，以便公司可以定位当前客户、拥有旧手机型号的客户以及[!DNL YouTube]上的类似客户。

## [!DNL Google Customer Match]目标{#data-governance}的数据管理

Experience Platform中的某些目标对于发送到目标平台或从目标平台接收的数据具有特定规则和义务。 您有责任了解数据的限制和义务，以及如何在Adobe Experience Platform和目标平台中使用该数据。 Adobe Experience Platform提供了数据管理工具，可帮助您管理其中一些数据使用义务。 [进一](../../../data-governance/labels/overview.md) 步了解数据管理工具和策略。

## 支持的标识{#supported-identities}

[!DNL Google Customer Match] 支持激活下表所述的身份。了解有关[identities](/help/identity-service/namespaces.md)的更多信息。

| Target标识 | 描述 | 注意事项 |
|---|---|---|
| GAID | Google广告ID | 如果源标识是GAID命名空间，请选择此目标标识。 |
| IDFA | 适用于广告商的Apple ID | 如果源标识是IDFA命名空间，请选择此目标标识。 |
| phone_sha256_e.164 | E164格式的电话号码，使用SHA256算法进行哈希处理 | Adobe Experience Platform支持纯文本和SHA256哈希电话号码。 按照[ID匹配要求](#id-matching-requirements-id-matching-requirements)部分中的说明，分别将相应的命名空间用于纯文本和经过哈希处理的电话号码。 当源字段包含未哈希属性时，请选中&#x200B;**[!UICONTROL Apply transformation]**&#x200B;选项，以使[!DNL Platform]在激活时自动对数据进行哈希处理。 |
| email_lc_sha256 | 使用SHA256算法进行哈希处理的电子邮件地址 | Adobe Experience Platform支持纯文本和SHA256哈希电子邮件地址。 按照[ID匹配要求](#id-matching-requirements-id-matching-requirements)部分中的说明，分别对纯文本和经过哈希处理的电子邮件地址使用适当的命名空间。 当源字段包含未哈希属性时，请选中&#x200B;**[!UICONTROL Apply transformation]**&#x200B;选项，以使[!DNL Platform]在激活时自动对数据进行哈希处理。 |
| user_id | 自定义用户ID | 如果源标识是自定义命名空间，请选择此目标标识。 |

## 导出类型{#export-type}

**区段导出**  — 您正在导出区段（受众）的所有成员，以及目标中使用的标识符（名称、电话号码和其他） [!DNL Google Customer Match] 。

## [!DNL Google Customer Match] 帐户先决条件  {#google-account-prerequisites}

在Experience Platform中设置[!DNL Google Customer Match]目标之前，请确保阅读并遵循Google关于使用[!DNL Customer Match]的策略，如[Google支持文档](https://support.google.com/google-ads/answer/6299717)中所述。

### 允许列表 {#allowlist}

在Experience Platform中创建[!DNL Google Customer Match]目标之前，请确保您的[!DNL Google Ads]帐户符合[Google客户匹配策略](https://support.google.com/google-ads/answer/6299717/customer-match-policy)。

具有合规帐户的客户会自动被Google允许列出。

## ID匹配要求{#id-matching-requirements}

[!DNL Google] 要求不要发送任何个人身份信息(PII)。因此，激活到[!DNL Google Customer Match]的受众可以与&#x200B;*哈希*&#x200B;标识符（如电子邮件地址或电话号码）关联。

根据您摄取到Adobe Experience Platform中的ID类型，您必须遵循其相应要求。

## 电话号码哈希处理要求{#phone-number-hashing-requirements}

在[!DNL Google Customer Match]中激活电话号码的方法有两种：

* **摄取原始电话号码**:您可以将格式的原始电话号码摄 [!DNL E.164] 入到中 [!DNL Platform]，激活后这些电话号码会自动进行哈希处理。如果选择此选项，请确保始终将原始电话号码摄取到`Phone_E.164`命名空间中。
* **摄取经过哈希处理的电话号码**:您可以在将电话号码摄取到中之前，对您的电话号码进行 [!DNL Platform]哈希处理。如果选择此选项，请确保始终将您经过哈希处理的电话号码摄取到`PHONE_SHA256_E.164`命名空间中。

>[!NOTE]
>
>无法在[!DNL Google Customer Match]中激活被摄取到`Phone`命名空间的电话号码。

## 电子邮件哈希处理要求{#hashing-requirements}

您可以在将电子邮件地址摄取到Adobe Experience Platform之前对其进行哈希处理，或在Experience Platform中明确使用电子邮件地址，并在激活时对它们进行[!DNL Platform]哈希处理。

有关Google哈希要求和其他激活限制的更多信息，请参阅Google文档中的以下部分：

* [[!DNL Customer Match] 具有电子邮件地址、地址或用户ID](https://developers.google.com/adwords/api/docs/guides/remarketing#customer_match_with_email_address_address_or_user_id)
* [[!DNL Customer Match] 注意事项](https://developers.google.com/adwords/api/docs/guides/remarketing#customer_match_considerations)
* [客户与电话号码匹配](https://developers.google.com/adwords/api/docs/guides/remarketing#customer_match_with_phone_number)
* [与移动设备ID匹配的客户](https://developers.google.com/adwords/api/docs/guides/remarketing#customer_match_with_mobile_device_ids)


要了解如何在Experience Platform中摄取电子邮件地址，请参阅[批量摄取概述](../../../ingestion/batch-ingestion/overview.md)和[流摄取概述](../../../ingestion/streaming-ingestion/overview.md)。

如果您选择自行对电子邮件地址进行哈希处理，请确保符合上面链接中所述的Google要求。

## 使用自定义命名空间{#custom-namespaces}

在使用`User_ID`命名空间将数据发送到Google之前，请确保使用[!DNL gTag]同步您自己的标识符。 有关详细信息，请参阅[Google官方文档](https://support.google.com/google-ads/answer/9199250)。

<!-- Data from unhashed namespaces is automatically hashed by [!DNL Platform] upon activation.

Attribute source data is not automatically hashed. When your source field contains unhashed attributes, check the **[!UICONTROL Apply transformation]** option, to have [!DNL Platform] automatically hash the data on activation.
![Identity mapping transformation](../../assets/ui/activate-destinations/identity-mapping-transformation.png) -->

## 配置目标 — 视频演练 {#video}

以下视频演示了配置[!DNL Google Customer Match]目标和激活区段的步骤。 这些步骤也在后续各节中按顺序排列。

>[!VIDEO](https://video.tv.adobe.com/v/332599/?quality=12&learn=on&captions=eng)

## 连接到目标{#connect-destination}

在&#x200B;**[!UICONTROL 目标]** > **[!UICONTROL 目录]**&#x200B;中，滚动到&#x200B;**[!UICONTROL Advertising]**&#x200B;类别。 选择[!DNL Google Customer Match]，然后选择&#x200B;**[!UICONTROL 配置]**。

![连接到Google客户匹配目标](../../assets/catalog/advertising/google-customer-match/connect.png)

>[!NOTE]
>
>如果与此目标存在连接，则可以在目标卡上看到&#x200B;**[!UICONTROL 激活]**&#x200B;按钮。 有关&#x200B;**[!UICONTROL Activate]**&#x200B;和&#x200B;**[!UICONTROL Configure]**&#x200B;之间差异的更多信息，请参阅目标工作区文档的[Catalog](../../ui/destinations-workspace.md#catalog)部分。

在&#x200B;**帐户**&#x200B;步骤中，如果您之前已设置到[!DNL Google Customer Match]目标的连接，请选择&#x200B;**[!UICONTROL 现有帐户]**&#x200B;并选择现有连接。 或者，您也可以选择&#x200B;**[!UICONTROL 新帐户]**&#x200B;以设置到[!DNL Google Customer Match]的新连接。 要登录并将Adobe Experience Cloud连接到您的[!DNL Google Ad]帐户，请选择&#x200B;**[!UICONTROL 连接到目标]**。

>[!NOTE]
>
>Experience Platform支持身份验证过程中的凭据验证。 如果您向[!DNL Google Ad]帐户输入了不正确的凭据，则会显示一条错误消息，以确保您没有使用不正确的凭据完成工作流。

![连接到Google客户匹配目标 — 身份验证步骤](../../assets/catalog/advertising/google-customer-match/connection.png)

确认您的凭据并将Adobe Experience Cloud连接到您的Google帐户后，您可以选择&#x200B;**[!UICONTROL Next]**&#x200B;以继续执行&#x200B;**[!UICONTROL Authentication]**&#x200B;步骤。

![已确认凭据](../../assets/catalog/advertising/google-customer-match/connection-success.png)

在&#x200B;**[!UICONTROL 身份验证]**&#x200B;步骤中，为激活流程输入&#x200B;**[!UICONTROL 名称]**&#x200B;和&#x200B;**[!UICONTROL 描述]**，并填写Google **[!UICONTROL 帐户ID]**。

在此步骤中，您还可以选择应用于此目标的任何&#x200B;**[!UICONTROL 营销操作]**。 营销操作指示将数据导出到目标的意图。 您可以从Adobe定义的营销操作中进行选择，也可以创建自己的营销操作。 有关营销操作的更多信息，请参阅[数据使用策略概述](../../../data-governance/policies/overview.md)。

在填写上面的字段后，选择&#x200B;**[!UICONTROL 创建目标]**。

>[!IMPORTANT]
>
> * 默认情况下，**[!UICONTROL 与PII]**&#x200B;组合营销操作会为[!DNL Google Customer Match]目标选中，且无法删除。
> * 用于[!DNL Google Customer Match]目标。 **[!UICONTROL 帐]** 户ID是您使用Google的客户客户ID。ID的格式为xxx-xxx-xxxx。


![连接Google客户匹配 — 身份验证步骤](../../assets/catalog/advertising/google-customer-match/authentication.png)

您的目标现已创建完成。 如果要稍后激活区段，则可以选择&#x200B;**[!UICONTROL 保存并退出]**，或者选择&#x200B;**[!UICONTROL 下一步]**&#x200B;以继续工作流并选择要激活的区段。 无论哪种情况，请参阅下一节[将区段激活到 [!DNL Google Customer Match]](#activate-segments)，以了解工作流的其余部分。

## 将区段激活到[!DNL Google Customer Match] {#activate-segments}

有关如何将区段激活到[!DNL Google Customer Match]的说明，请参阅[将数据激活到目标](../../ui/activate-destinations.md)。


在&#x200B;**[!UICONTROL 区段计划]**&#x200B;步骤中，在向[!DNL Google Customer Match]发送[!DNL IDFA]或[!DNL GAID]区段时，必须提供[!UICONTROL 应用程序ID]。

![Google客户匹配应用程序ID](../../assets/catalog/advertising/google-customer-match/gcm-destination-appid.png)

有关如何查找[!DNL App ID]的详细信息，请参阅[Google官方文档](https://developers.google.com/adwords/api/docs/reference/v201809/AdwordsUserListService.CrmBasedUserList#appid)。

## 验证区段激活是否成功{#verify-activation}

完成激活流程后，切换到您的&#x200B;**[!UICONTROL Google Ads]**&#x200B;帐户。 激活的区段将作为客户列表显示在您的Google帐户中。 请注意，根据区段大小，某些受众不会填充，除非要提供的活动用户超过100个。

将区段同时映射到[!DNL IDFA]和[!DNL GAID]移动ID时， [!DNL Google Customer Match]会为每个ID映射创建一个单独的区段。 您的[!DNL Google Ads]帐户显示两个不同的区段，一个用于[!DNL IDFA]，另一个用于[!DNL GAID]映射。

## 额外资源{#additional-resources}

* [集成Google客户匹配 — 视频教程](https://experienceleague.adobe.com/docs/platform-learn/tutorials/rtcdp/integrate-with-google-customer-match.html)
