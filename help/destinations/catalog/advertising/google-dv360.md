---
keywords: 双击竞价管理器；双击竞价管理器；双击；显示和视频360；显示360；视频360；视频360；显示360；显示360；显示360；显示360；显示
title: Google Display & Video 360连接
description: 显示和视频360（以前称为“双击竞价管理器”）是一种工具，用于在显示、视频和移动设备库存源中执行重定位和受众定位的数字促销活动。
exl-id: bdd3b3fd-891f-44ec-bd47-daf7f3289f92
source-git-commit: 802b1844bec1e577e978da5d5a69de87278c04b9
workflow-type: tm+mt
source-wordcount: '671'
ht-degree: 2%

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

## 支持的身份 {#supported-identities}

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

## 连接到目标 {#connect}

要连接到此目标，请按照[目标配置教程](../../ui/connect-destination.md)中描述的步骤操作。

### 连接参数 {#parameters}

在[设置](../../ui/connect-destination.md)此目标时，必须提供以下信息：

* **[!UICONTROL 名称]**:填写此目标的首选名称。
* **[!UICONTROL 描述]**:可选。例如，您可以提及您使用此目标的促销活动。
* **[!UICONTROL 帐户类型]**:根据您在Google上的帐户选择一个选项：
   * 使用`Invite Advertiser`可仅将受众共享到您的Display &amp; Video 360帐户中的特定品牌。
   * 使用`Invite Partner`可允许将受众共享到您的Display &amp; Video 360帐户中的所有品牌。
* **[!UICONTROL 帐户ID]**:使用Google填 **[!DNL Invite partner]** 写您 **[!DNL Invite advertiser]** 的或帐户ID。通常是一个六位或七位数的ID。

>[!NOTE]
>
>设置[!DNL Google Display & Video 360]目标时，请与您的[!DNL Google Account Manager]或Adobe代表合作，了解您拥有的帐户类型。

## 将区段激活到此目标 {#activate}

有关将受众区段激活到目标的说明，请参阅[将配置文件和区段激活到目标](../../ui/activate-destinations.md)。

## 导出的数据

要验证数据是否已成功导出到[!DNL Google Display & Video 360]目标，请检查您的[!DNL Google Display & Video 360]帐户。 如果激活成功，则帐户中会填充受众。
