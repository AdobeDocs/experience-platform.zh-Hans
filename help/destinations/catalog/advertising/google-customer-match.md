---
keywords: Google客户匹配；Google客户匹配；Google客户匹配
title: Google客户匹配连接
description: Google客户匹配允许您使用线上和线下数据在Google自有和运营的资产（如搜索、购物、Gmail和YouTube）中触及客户并与其重新互动。
translation-type: tm+mt
source-git-commit: bec44832a235dd3f9e2ee0f3ffc77854ee5784d7
workflow-type: tm+mt
source-wordcount: '1432'
ht-degree: 0%

---


# [!DNL Google Customer Match] 连接

[Google客](https://support.google.com/google-ads/answer/6379332?hl=en) 户匹配允许您使用线上和线下数据，通过Google自有和运营的资产触及客户并与其重新互动，例如： [!DNL Search]、 [!DNL Shopping]、 [!DNL Gmail]和 [!DNL YouTube]。

![Google实时CDP UI中的客户匹配目标](../../assets/catalog/advertising/google-customer-match/catalog.png)

## 用例

为了帮助您更好地了解应如何以及何时使用[!DNL Google Customer Match]目标，以下是实时客户数据平台客户可通过使用此功能解决的示例使用案例。

### 用例#1

运动服装品牌希望通过[!DNL Google Search]和[!DNL Google Shopping]接触现有客户，以根据其过去的购买和浏览历史个性化优惠和项目。 服装品牌可以将电子邮件地址从自己的CRM收录到实时CDP，根据自己的离线数据构建细分，并将这些细分发送到[!DNL Google Customer Match]以用于[!DNL Search]和[!DNL Shopping]，从而优化其广告支出。

### 用例#2

一位知名科技公司刚刚发布了一部新手机。 为了推广这种新型号的手机，他们希望将手机的新特性和功能提升到拥有旧型号手机的客户的认识。

要提升发行版，他们会将电子邮件地址从CRM数据库上载到实时CDP中，使用电子邮件地址作为标识符。 细分是根据拥有旧型号的客户创建的，并发送给[!DNL Google Customer Match]，以便他们能够目标当前客户、拥有旧型号的客户以及[!DNL YouTube]上的类似客户。

## 目标特性{#destination-specs}

### [!DNL Google Customer Match]目标{#data-governance}的数据管理

实时CDP中的目标可能具有特定的规则和义务，用于向目标平台发送或从目标平台接收数据。 您有责任了解数据的限制和义务，以及您如何在Adobe Experience Platform和目标平台中使用这些数据。 Adobe Experience Platform提供数据管理工具，帮助您管理其中的一些数据使用义务。 [进一步](../../..//data-governance/labels/overview.md) 了解数据治理工具和策略。

### 导出类型和标识{#export-type}

**区段导出**  — 您正在导出包含标识符（名称、电话号码等）的区段(受众)的所有成员在[!DNL Google Customer Match]目标中使用。

**身份**  — 您可以在Google中将原始或哈希电子邮件用作客户ID

### [!DNL Google Customer Match] 帐户先决条件  {#google-account-prerequisites}

在实时CDP中设置[!DNL Google Customer Match]目标之前，请确保阅读并遵守Google关于使用[!DNL Customer Match]的策略，该策略在[Google支持文档](https://support.google.com/google-ads/answer/6299717)中进行了概述。

### 允许列表{#allowlist}

>[!NOTE]
>
>必须先将它添加到Google的允许列表中，然后才能在实时CDP中设置您的第一个[!DNL Google Customer Match]目标。 在创建目标之前，请确保Google已完成下面描述的允许列表过程。

在实时CDP中创建[!DNL Google Customer Match]目标之前，必须联系Google并按照[使用允许列表匹配合作伙伴上传Google文档中的数据](https://support.google.com/google-ads/answer/7361372?hl=en&amp;ref_topic=6296507)中的说明进行操作。

此外，如果您计划使用Google的[User_ID](https://developers.google.com/adwords/api/docs/guides/remarketing#customer_match_with_email_address_address_or_user_id)上载数据，则还必须添加第二个Google允许列表。 请与您的Google客户经理联系，以确保您已添加到允许列表。

### ID匹配要求{#id-matching-requirements}

[!DNL Google] 要求不要发送任何清晰的个人身份信息(PII)。因此，激活到[!DNL Google Customer Match]的受众可以键出&#x200B;*散列*&#x200B;标识符，如电子邮件地址或电话号码。

根据您将ID引入Adobe Experience Platform的类型，您需要遵守其相应要求。

#### 电话号码哈希要求{#phone-number-hashing-requirements}

在[!DNL Google Customer Match]中激活电话号码有两种方法：

* **接收原始电话号码**:您可以将原始电话号码的格 [!DNL E.164] 式录 [!DNL Platform]制为，该格式将在激活时自动散列。如果选择此选项，请确保始终将原始电话号码收录到`Phone_E.164`命名空间。
* **正在获取哈希电话号码**:你可以先对电话号码进行哈希处理，然后再将其引入 [!DNL Platform]。如果选择此选项，请确保始终将哈希电话号码收录到`PHONE_SHA256_E.164`命名空间。

>[!NOTE]
>
>无法在[!DNL Google Customer Match]中激活被引入`Phone`命名空间的电话号码。

#### 电子邮件散列要求{#hashing-requirements}

您可以选择在将电子邮件地址引入Adobe Experience Platform之前对它们进行哈希处理，也可以选择在Experience Platform中清晰地处理电子邮件地址，并在激活上使用我们的算法对它们进行哈希处理。

有关Google散列要求和其他激活限制的详细信息，请参阅Google文档中的以下部分：

* [[!DNL Customer Match] 和电子邮件地址、地址或用户ID](https://developers.google.com/adwords/api/docs/guides/remarketing#customer_match_with_email_address_address_or_user_id)
* [[!DNL Customer Match] 注意事项](https://developers.google.com/adwords/api/docs/guides/remarketing#customer_match_considerations)
* [客户与电话号码匹配](https://developers.google.com/adwords/api/docs/guides/remarketing#customer_match_with_phone_number)
* [客户与移动设备ID匹配](https://developers.google.com/adwords/api/docs/guides/remarketing#customer_match_with_mobile_device_ids)


要了解在Experience Platform中摄取电子邮件地址的信息，请参阅[批摄取概述](../../../ingestion/batch-ingestion/overview.md)和[流摄取概述](../../../ingestion/streaming-ingestion/overview.md)。

如果您选择自己对电子邮件地址进行哈希处理，请确保符合上面链接中概述的Google要求。

#### 使用自定义命名空间{#custom-namespaces}

在使用`User_ID`命名空间向Google发送数据之前，请确保使用[!DNL gTag]同步您自己的标识符。 有关详细信息，请参阅[官方文档](https://support.google.com/google-ads/answer/9199250)。

<!-- Data from unhashed namespaces is automatically hashed by [!DNL Platform] upon activation.

Attribute source data is not automatically hashed. When your source field contains unhashed attributes, check the **[!UICONTROL Apply transformation]** option, to have [!DNL Platform] automatically hash the data on activation.
![Identity mapping transformation](../../assets/ui/activate-destinations/identity-mapping-transformation.png) -->

## 连接到目标{#connect-destination}

在&#x200B;**[!UICONTROL 目标]** > **[!UICONTROL 目录]**&#x200B;中，滚动到&#x200B;**[!UICONTROL 广告]**&#x200B;类别。 选择[!DNL Google Customer Match]，然后选择&#x200B;**[!UICONTROL 配置]**。

![连接到Google客户匹配目标](../../assets/catalog/advertising/google-customer-match/connect.png)

>[!NOTE]
>
>如果与此目标的连接已存在，您可以在目标卡上看到&#x200B;**[!UICONTROL 激活]**&#x200B;按钮。 有关&#x200B;**[!UICONTROL Activate]**&#x200B;和&#x200B;**[!UICONTROL Configure]**&#x200B;之间差异的详细信息，请参阅目标工作区文档的[Catalog](../../ui/destinations-workspace.md#catalog)部分。

在&#x200B;**帐户**&#x200B;步骤中，如果您之前已设置到[!DNL Google Customer Match]目标的连接，请选择&#x200B;**[!UICONTROL 现有帐户]**&#x200B;并选择您的现有连接。 或者，您可以选择&#x200B;**[!UICONTROL 新建帐户]**&#x200B;来设置到[!DNL Google Customer Match]的新连接。 选择&#x200B;**[!UICONTROL 连接到目标]**&#x200B;以登录，并将Adobe Experience Cloud连接到您的[!DNL Google Ad]帐户。

>[!NOTE]
>
>实时CDP支持身份验证过程中的凭据验证，如果您向[!DNL Google Ad]帐户输入了不正确的凭据，则会显示错误消息。 这可确保您没有使用不正确的凭据完成工作流。

![连接到Google客户匹配目标 — 身份验证步骤](../../assets/catalog/advertising/google-customer-match/connection.png)

确认您的凭据并将Adobe Experience Cloud连接到您的Google帐户后，您可以选择&#x200B;**[!UICONTROL Next]**&#x200B;以继续执行&#x200B;**[!UICONTROL Setup]**&#x200B;步骤。

![已确认凭据](../../assets/catalog/advertising/google-customer-match/connection-success.png)

在&#x200B;**[!UICONTROL 身份验证]**&#x200B;步骤中，输入激活流的[!UICONTROL 名称]和[!UICONTROL 说明]，然后在Google中填写[!UICONTROL 帐户ID]。

此外，在此步骤中，您还可以选择应用于此目标的任何&#x200B;**[!UICONTROL 营销操作]**。 营销活动指示要将数据导出到目标的目的。 您可以从Adobe定义的营销活动中进行选择，也可以创建自己的营销活动。 有关营销操作的详细信息，请参阅[实时CDP](../../../rtcdp/privacy/data-governance-overview.md#destinations)数据治理页。 有关各个Adobe定义的营销操作的信息，请参阅[数据使用策略概述](../../../data-governance/policies/overview.md#core-actions)。

在填写上面的字段后，选择&#x200B;**[!UICONTROL 创建目标]**。

>[!IMPORTANT]
>
> * 默认情况下，**[!UICONTROL 与PII]**&#x200B;组合营销操作会为[!DNL Google Customer Match]目标选择，并且无法删除。
> * 对于[!DNL Google Customer Match]目标。 **[!UICONTROL 帐]** 户ID是您的Google客户端ID。ID的格式为xxx-xxx-xxxx。


![连接Google客户匹配 — 身份验证步骤](../../assets/catalog/advertising/google-customer-match/authentication.png)

您的目标现在已创建。 如果您希望稍后激活区段，可以选择&#x200B;**[!UICONTROL 保存并退出]**，也可以选择&#x200B;**[!UICONTROL 下一步]**&#x200B;继续工作流并选择要激活的区段。 在任一情况下，请参阅工作流其余部分的下一节[将区段激活为 [!DNL Google Customer Match]](#activate-segments)。

## 将区段激活到[!DNL Google Customer Match] {#activate-segments}

有关如何将区段激活到[!DNL Google Customer Match]的说明，请参阅[将数据激活到目标](../../ui/activate-destinations.md)。


在&#x200B;**[!UICONTROL 区段计划]**&#x200B;步骤中，当将[!DNL IDFA]或[!DNL GAID]区段发送到[!DNL Google Customer Match]时，必须提供[!UICONTROL 应用程序ID]。

![Google客户匹配应用程序ID](../../assets/catalog/advertising/google-customer-match/gcm-destination-appid.png)

有关如何查找[!DNL App ID]的详细信息，请参阅[官方文档](https://developers.google.com/adwords/api/docs/reference/v201809/AdwordsUserListService.CrmBasedUserList#appid)。







<!-- 
To activate segments to [!DNL Google Customer Match], follow the steps below: 

In **[!UICONTROL Destinations > Browse]**, select the [!DNL Google Customer Match] destination where you want to activate your segments.

Click the name of the destination. This takes you to the Activate flow.

![activate-flow](../../assets/catalog/advertising/google-customer-match/activate-flow.png)

Note that if an activation flow already exists for a destination, you can see the segments that are currently being sent to the destination. Select **[!UICONTROL Edit activation]** in the right rail and follow the steps below to modify the activation details.

Select **[!UICONTROL Activate]**. In the **[!UICONTROL Activate destination]** workflow, on the **[!UICONTROL Select Segments]** page, select which segments to send to [!DNL Google Customer Match].

![segments-to-destination](../../assets/catalog/advertising/google-customer-match/activate-segments.png)

In the **[!UICONTROL Identity mapping]** step, select which attributes to be included as an identity in this destination. Select **[!UICONTROL Add new mapping]** and browse your schema, select email and/or hashed email, and map them to the corresponding target identity.

![identity mapping initial screen](../../assets/catalog/advertising/google-customer-match/identity-mapping.png) 

**Plain text email address as primary identity**: If you have plain text (unhashed) email addresses as primary identity in your schema, select the email field in your **[!UICONTROL Source Attributes]** and map to the Email field in the right column under **[!UICONTROL Target Identities]**, as shown below:

![select plain text emails identity](../../assets/catalog/advertising/google-customer-match/raw-email.gif) 

**Hashed email address as primary identity**: If you have hashed email addresses as primary identity in your schema, select the hashed email field in your **[!UICONTROL Source Attributes]** and map to the Email_LC_SHA256 field in the right column under **[!UICONTROL Target Identities]**, as shown below:

![select hashed emails identity](../../assets/catalog/advertising/google-customer-match/hashed-emails.gif)

On the **[!UICONTROL Segment schedule]** page, you can set the start date for sending data to the destination.

On the **[!UICONTROL Review]** page, you can see a summary of your selection. Select **[!UICONTROL Cancel]** to break up the flow, **[!UICONTROL Back]** to modify your settings, or **[!UICONTROL Finish]** to confirm your selection and start sending data to the destination.

>[!IMPORTANT]
>
>In this step, Real-time CDP checks for data usage policy violations. Shown below is an example where a policy is violated. You cannot complete the segment activation workflow until you have resolved the violation. For information on how to resolve policy violations, see [Policy enforcement](../../../rtcdp/privacy/data-governance-overview.md#enforcement) in the data governance documentation section.
 
![confirm-selection](../../assets/common/data-policy-violation.png)

If no policy violations have been detected, select **[!UICONTROL Finish]** to confirm your selection and start sending data to the destination.

![confirm-selection](../../assets/catalog/advertising/google-customer-match/review.png) -->

## 验证区段激活是否成功{#verify-activation}

完成激活流后，切换到您的&#x200B;**[!UICONTROL Google Ads]**&#x200B;帐户。 激活的区段现在将作为客户列表显示在您的Google帐户中。 请注意，根据您的区段大小，除非有100多个活动用户提供服务，否则某些受众将不会填充。

将区段映射到[!DNL IDFA]和[!DNL GAID]移动ID时， [!DNL Google Customer Match]会为每个ID映射创建单独的区段。 您的[!DNL Google Ads]帐户将显示两个不同的区段，一个用于[!DNL IDFA]，另一个用于[!DNL GAID]映射。

## 其他资源 {#additional-resources}

* [集成Google客户匹配 — 视频教程](https://experienceleague.adobe.com/docs/platform-learn/tutorials/rtcdp/integrate-with-google-customer-match.html)