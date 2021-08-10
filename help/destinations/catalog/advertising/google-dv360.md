---
keywords: 双击竞价管理器；双击竞价管理器；双击；显示和视频360；显示360；视频360；视频360；显示360；显示360；显示360；显示360；显示
title: Google Display & Video 360连接
description: 显示和视频360（以前称为“双击竞价管理器”）是一种工具，用于在显示、视频和移动设备库存源中执行重定位和受众定位的数字促销活动。
exl-id: bdd3b3fd-891f-44ec-bd47-daf7f3289f92
source-git-commit: 7e2f6f54e754c52c8de7f98372d041b2a6520d46
workflow-type: tm+mt
source-wordcount: '764'
ht-degree: 1%

---

# [!DNL Google Display & Video 360] 连接

## 概述 {#overview}

[!DNL Display & Video 360]（以前称为）是一 [!DNL DoubleClick Bid Manager]个工具，用于在显示、视频和移动设备库存源中执行重定向和受众定位的数字促销活动。

## 目标详情 {#specifics}

请注意特定于[!DNL Google Display & Video 360]目标的以下详细信息：

* 激活的受众在Google平台中以编程方式创建。
* [!DNL Platform] 当前不包括用于验证激活是否成功的测量量度。请参阅Google中的受众计数，以验证集成并了解受众定位大小。

>[!IMPORTANT]
>
>如果您希望使用Google Display &amp; Video 360创建您的第一个目标，并且过去(使用Adobe Audience Manager或其他应用程序)未在Experience CloudID服务中启用[ID同步功能](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html)，请联系Adobe咨询或客户关怀团队以启用ID同步。 如果您之前在Audience Manager中设置了Google集成，则您设置的ID同步会传递到Platform。

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

### 允许列表

>[!NOTE]
>
>在Platform中设置您的第一个[!DNL Google Display & Video 360]目标之前，必须允许列表。 在创建目标之前，请确保Google已完成下述允许列表过程。

在Platform中创建[!DNL Google Display & Video 360]目标之前，您必须联系Google以请求将Adobe添加到允许的数据提供商列表中，并将您的帐户添加到允许列表中。 联系Google并提供以下信息：

* **帐户ID**:Adobe的帐户ID。帐户ID:87933855。
* **客户ID**:Adobe的客户帐户ID与Google。客户ID:89690775。
* **您的帐户类型**:使 **[!DNL Invite advertiser]** 用可仅将受众共享到Display &amp; Video 360帐户中的特定品牌，或使用 **[!DNL Invite partner]** 可将受众共享到Display &amp; Video 360帐户中的所有品牌。

## 配置目标

在&#x200B;**[!UICONTROL 连接]** > **[!UICONTROL 目标]**&#x200B;中，选择[!DNL Google Display & Video 360]，然后选择&#x200B;**[!UICONTROL 配置]**。

![连接Google Display &amp; Video 360目标](../../assets/catalog/advertising/google-dv360/catalog.png)

>[!NOTE]
>
>如果与此目标的连接已存在，则可以在目标卡上看到&#x200B;**[!UICONTROL 激活]**&#x200B;按钮。 有关[!UICONTROL Activate]和[!UICONTROL Configure]之间差异的更多信息，请参阅目标工作区文档的[Catalog](../../ui/destinations-workspace.md#catalog)部分。

在创建目标工作流的&#x200B;**设置**&#x200B;步骤中，填写目标的[!UICONTROL 基本信息]以及应用于此目标的营销操作。

![Google Display &amp; Video 360的基本信息](../../assets/catalog/advertising/google-dv360/setup.png)

* **[!UICONTROL 名称]**:填写此目标的首选名称。
* **[!UICONTROL 描述]**:可选。例如，您可以提及您使用此目标的促销活动。
* **[!UICONTROL 帐户类型]**:根据您在Google上的帐户选择一个选项：
   * 使用`Invite Advertiser`可仅将受众共享到您的Display &amp; Video 360帐户中的特定品牌。
   * 使用`Invite Partner`可允许将受众共享到您的Display &amp; Video 360帐户中的所有品牌。
* **[!UICONTROL 帐户ID]**:使用Google填 **[!DNL Invite partner]** 写您 **[!DNL Invite advertiser]** 的或帐户ID。通常是一个六位或七位数的ID。
* **[!UICONTROL 营销操作]**:营销操作指示将数据导出到目标的意图。您可以从Adobe定义的营销操作中进行选择，也可以创建自己的营销操作。 有关营销操作的更多信息，请参阅[数据使用策略概述](../../../data-governance/policies/overview.md)。

>[!NOTE]
>
>设置[!DNL Google Display & Video 360]目标时，请与您的[!DNL Google Account Manager]或Adobe代表合作，了解您拥有的帐户类型。

## 将区段激活到[!DNL Google Display & Video 360]

有关如何将区段激活到[!DNL Google Display & Video 360]的说明，请参阅[将数据激活到目标](../../ui/activate-destinations.md)。

## 导出的数据

要验证数据是否已成功导出到[!DNL Google Display & Video 360]目标，请检查您的[!DNL Google Display & Video 360]帐户。 如果激活成功，则帐户中会填充受众。
