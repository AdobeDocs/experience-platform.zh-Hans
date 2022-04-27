---
keywords: Google广告；Google广告；Google AdWords;Google AdWords;Google Adwords
title: Google Ads连接
description: Google Ads(以前称为Google AdWords)是一种在线广告服务，允许企业通过基于文本的搜索、图形显示、YouTube视频和应用程序内移动显示，按点击量付费广告。
exl-id: 7143f476-49a8-42aa-bfb4-b11fc2b8f5c3
source-git-commit: 0006c498cd33d9deb66f1d052b4771ec7504457d
workflow-type: tm+mt
source-wordcount: '835'
ht-degree: 3%

---

# [!DNL Google Ads] 连接

## 概述 {#overview}

[!DNL Google Ads]，以前称为 [!DNL Google AdWords]，是一项在线广告服务，允许企业通过基于文本的搜索、图形显示等方式，按点击量付费广告， [!DNL YouTube] 显示视频和应用程序内移动设备。

## 目标详情 {#specifics}

请注意以下特定于 [!DNL Google Ads] 目标：

* 激活的受众是在 [!DNL Google] 平台。
* [!DNL Platform] 当前不包括用于验证激活是否成功的测量量度。 请参阅Google中的受众计数，以验证集成并了解受众定位大小。

>[!IMPORTANT]
>
>如果您希望通过 [!DNL Google Ads] 尚未启用 [ID同步功能](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html) 在过去的Experience CloudID服务(使用Audience Manager或其他应用程序)中，请联系Adobe咨询或客户关怀团队以启用ID同步。 如果您之前在Audience Manager中设置了Google集成，则您设置的ID同步会传递到Platform。

## 支持的身份 {#supported-identities}

[!DNL Google Ad Manager] 支持激活下表所述的身份。

| Target标识 | 描述 | 注意事项 |
|---|---|---|
| GAID | [!DNL Google Advertising ID] | 如果源标识是GAID命名空间，请选择此目标标识。 |
| IDFA | [!DNL Apple ID for Advertisers] | 如果源标识是IDFA命名空间，请选择此目标标识。 |
| AAM UUID | [Adobe Audience Manager [!DNL Unique User ID]](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html)，也称为 [!DNL Device ID]. 一个38位数的数字设备ID，Audience Manager会将其与之交互的每个设备相关联。 | Google使用 [AAM UUID](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html?lang=en) 来定位加利福尼亚州的用户，以及所有其他用户的Google Cookie ID。 |
| [!DNL Google] Cookie ID | [!DNL Google] Cookie ID | [!DNL Google] 会使用此ID来定位加州以外的用户。 |
| RIDA | 用于广告的Roku ID。 此ID唯一标识Roku设备。 |  |
| 女佣 | Microsoft广告ID。 此ID唯一标识运行Windows 10的设备。 |  |
| Amazon Fire TV ID | 此ID可唯一标识Amazon Fire TV。 |  |

{style=&quot;table-layout:auto&quot;}

## 导出类型和频度 {#export-type-frequency}

有关目标导出类型和频率的信息，请参阅下表。

| 项目 | 类型 | 注释 |
---------|----------|---------|
| 导出类型 | **[!UICONTROL 区段导出]** | 您将区段（受众）的所有成员导出到Google目标。 |
| 导出频度 | **[!UICONTROL 流]** | 流目标“始终运行”基于API的连接。 在基于区段评估的Experience Platform中更新用户档案后，连接器会立即将更新发送到目标平台下游。 有关更多信息 [流目标](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## 先决条件 {#prerequisites}

### 现有 [!DNL Google Ads] 帐户

>[!IMPORTANT]
>
> [!DNL Google] 已弃用新 [!DNL Google Ads] 与第三方供应商的cookie集成。 要执行下一节中的允许列表步骤，您必须与 [!DNL Google Ads]. 因此，建议使用 [!DNL Google Ads] 正在设置 [!DNL Google Customer Match] 集成。 有关创建 [!DNL Google Customer Match] 集成，请阅读有关创建 [[!DNL Google Customer Match]](./google-customer-match.md) 连接。

### 允许列表 {#allow-listing}

>[!NOTE]
>
>允许列表在设置第一个 [!DNL Google Ads] 目标。 请确保已完成下述允许列表流程 [!DNL Google] 创建目标之前。

在创建 [!DNL Google Ads] 目标，您必须联系 [!DNL Google] Adobe添加到允许的数据提供程序列表，以及将帐户添加到允许列表。 联系人 [!DNL Google] 并提供以下信息：

* **帐户ID**:Adobe的帐户ID与Google。 帐户ID:87933855。
* **客户ID**:Adobe的客户帐户ID和Google。 客户ID:89690775。
* 您的帐户类型： **AdWords**
* **Google AdWords ID**:这是您的ID [!DNL Google]. ID格式通常为123-456-7890。

## 连接到目标 {#connect}

>[!IMPORTANT]
> 
>要连接到目标，您需要 **[!UICONTROL 管理目标]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或联系您的产品管理员以获取所需的权限。

要连接到此目标，请按照 [目标配置教程](../../ui/connect-destination.md).

### 连接参数 {#parameters}

While [设置](../../ui/connect-destination.md) 此目标中，您必须提供以下信息：

* **[!UICONTROL 名称]**:填写此目标的首选名称。
* **[!UICONTROL 描述]**:可选。 例如，您可以提及您使用此目标的促销活动。
* **[!UICONTROL 帐户类型]**:AdWords是唯一可用的选项。
* **[!UICONTROL 帐户ID]**:使用 [!DNL Google Ads]. ID格式通常为123-456-7890。

## 将区段激活到此目标 {#activate}

>[!IMPORTANT]
> 
>要激活数据，您需要 **[!UICONTROL 管理目标]**, **[!UICONTROL 激活目标]**, **[!UICONTROL 查看配置文件]**&#x200B;和 **[!UICONTROL 查看区段]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或联系您的产品管理员以获取所需的权限。

请参阅 [将受众数据激活到流区段导出目标](../../ui/activate-segment-streaming-destinations.md) 有关将受众区段激活到此目标的说明。

## 导出的数据

验证数据是否已成功导出到 [!DNL Google Ads] 目标位置，检查 [!DNL Google Ads] 帐户。 如果激活成功，则帐户中会填充受众。

## 故障排除 {#troubleshooting}

### 400错误请求错误消息 {#bad-request}

配置此目标时，您可能会收到以下错误：

`{"message":"Google Error: AuthorizationError.USER_PERMISSION_DENIED","code":"400 BAD_REQUEST"}`

当客户帐户不符合 [先决条件](#prerequisites) 或者，当客户尝试配置目标时，没有现有 [!DNL Google Ads] 帐户。

[!DNL Google] 已弃用新 [!DNL Google Ads] 与第三方供应商的cookie集成。 要执行 [允许列表](#allow-listing) 步骤中，您必须与 [!DNL Google Ads].

建议的使用方法 [!DNL Google Ads] 正在设置 [[!DNL Google Customer Match]](google-customer-match.md) 集成。
