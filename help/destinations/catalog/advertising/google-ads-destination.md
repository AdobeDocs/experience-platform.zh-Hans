---
keywords: Google广告；Google广告；Google AdWords;Google AdWords
title: Google Ads连接
description: Google Ads（以前称为Google AdWords）是一种在线广告服务，允许企业通过基于文本的搜索、图形显示、YouTube视频和应用程序内移动显示，按次点击付费广告。
exl-id: 7143f476-49a8-42aa-bfb4-b11fc2b8f5c3
source-git-commit: 7e2f6f54e754c52c8de7f98372d041b2a6520d46
workflow-type: tm+mt
source-wordcount: '716'
ht-degree: 2%

---

# [!DNL Google Ads] 连接

## 概述 {#overview}

[!DNL Google Ads]（以前称为） [!DNL Google AdWords]是一种在线广告服务，允许企业通过基于文本的搜索、图形显示、视频和应用程序内移动显示，按 [!DNL YouTube] 次点击量付费广告。

## 目标详情 {#specifics}

请注意特定于[!DNL Google Ads]目标的以下详细信息：

* 在[!DNL Google]平台中以编程方式创建激活的受众。
* [!DNL Platform] 当前不包括用于验证激活是否成功的测量量度。请参阅Google中的受众计数，以验证集成并了解受众定位大小。

>[!IMPORTANT]
>
>如果您希望使用[!DNL Google Ads]创建您的第一个目标，并且过去(使用Audience Manager或其他应用程序)未在Experience CloudID服务中启用[ ID同步功能](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html)，请联系Adobe咨询或客户关怀团队以启用ID同步。 如果您之前在Audience Manager中设置了Google集成，则您设置的ID同步会传递到Platform。

## 支持的标识 {#supported-identities}

[!DNL Google Ad Manager] 支持激活下表所述的身份。

| Target标识 | 描述 | 注意事项 |
|---|---|---|
| GAID | [!DNL Google Advertising ID] | 如果源标识是GAID命名空间，请选择此目标标识。 |
| IDFA | [!DNL Apple ID for Advertisers] | 如果源标识是IDFA命名空间，请选择此目标标识。 |
| AAM UUID | [Adobe Audience Manager [!DNL Unique User ID]](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html)，也称为 [!DNL Device ID]。一个38位数的数字设备ID，Audience Manager会将其与之交互的每个设备相关联。 | Google使用[AAM UUID](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html?lang=en)来定位加利福尼亚州的用户，并针对所有其他用户使用Google Cookie ID。 |
| [!DNL Google] Cookie ID | [!DNL Google] Cookie ID | [!DNL Google] 会使用此ID来定位加州以外的用户。 |
| RIDA | 用于广告的Roku ID。 此ID唯一标识Roku设备。 |  |
| 女佣 | Microsoft广告ID。 此ID唯一标识运行Windows 10的设备。 |  |
| Amazon Fire TV ID | 此ID可唯一标识Amazon Fire TV。 |  |

## 导出类型 {#export-type}

**区段导出**  — 您要将区段（受众）的所有成员导出到Google目标。

## 先决条件

### 现有[!DNL Google Ads]帐户

>[!IMPORTANT]
>
> [!DNL Google] 已弃用与 [!DNL Google Ads] 第三方供应商的新cookie集成。要执行下一节中的允许列表步骤，您必须具有与[!DNL Google Ads]的现有集成。 因此，使用[!DNL Google Ads]的建议方法是设置[!DNL Google Customer Match]集成。 有关创建[!DNL Google Customer Match]集成的更多详细信息，请阅读有关创建[[!DNL Google Customer Match]](./google-customer-match.md)连接的教程。

### 允许列表

>[!NOTE]
>
>在Platform中设置您的第一个[!DNL Google Ads]目标之前，必须允许列表。 在创建目标之前，请确保[!DNL Google]已完成下述允许列表过程。

在Platform中创建[!DNL Google Ads]目标之前，您必须联系[!DNL Google]，以便Adobe被列入允许的数据提供程序列表，并将帐户添加到允许列表。 联系[!DNL Google]并提供以下信息：

* **帐户ID**:Adobe的帐户ID。帐户ID:87933855。
* **客户ID**:Adobe的客户帐户ID与Google。客户ID:89690775。
* 您的帐户类型：**AdWords**
* **Google AdWords ID**:这是您的ID  [!DNL Google]。ID格式通常为123-456-7890。

## 配置目标

在&#x200B;**[!UICONTROL 连接]** > **[!UICONTROL 目标]**&#x200B;中，选择[!DNL Google Ads]，然后选择&#x200B;**[!UICONTROL 配置]**。

![连接Google Ads目标](../../assets/catalog/advertising/google-ads-destination/catalog.png)

>[!NOTE]
>
>如果与此目标的连接已存在，则可以在目标卡上看到&#x200B;**[!UICONTROL 激活]**&#x200B;按钮。 有关&#x200B;**[!UICONTROL Activate]**&#x200B;和&#x200B;**[!UICONTROL Configure]**&#x200B;之间差异的更多信息，请参阅目标工作区文档的[Catalog](../../ui/destinations-workspace.md#catalog)部分。

在创建目标工作流的&#x200B;**设置**&#x200B;步骤中，填写目标的[!UICONTROL 基本信息]。

![Google Ads基本信息](../../assets/catalog/advertising/google-ads-destination/setup.png)

* **[!UICONTROL 名称]**:填写此目标的首选名称。
* **[!UICONTROL 描述]**:可选。例如，您可以提及您使用此目标的促销活动。
* **[!UICONTROL 帐户类型]**:AdWords是唯一可用的选项。
* **[!UICONTROL 帐户ID]**:使用填写您的帐户ID  [!DNL Google Ads]。ID格式通常为123-456-7890。
* **[!UICONTROL 营销操作]**:营销操作指示将数据导出到目标的意图。您可以从Adobe定义的营销操作中进行选择，也可以创建自己的营销操作。 有关营销操作的更多信息，请参阅[数据使用策略概述](../../../data-governance/policies/overview.md)。

## 将区段激活到[!DNL Google Ads]

有关如何将区段激活到[!DNL Google Ads]的说明，请参阅[将数据激活到目标](../../ui/activate-destinations.md)。

## 导出的数据

要验证数据是否已成功导出到[!DNL Google Ads]目标，请检查您的[!DNL Google Ads]帐户。 如果激活成功，则帐户中会填充受众。
