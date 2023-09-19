---
title: LiveRamp — 分发连接
description: 了解如何使用LiveRamp - Distribution连接器将之前载入LiveRamp的受众激活到其他广告目标。
hide: true
hidefromtoc: true
source-git-commit: 324f662dcc9718df6c81c47874c6b30235a74601
workflow-type: tm+mt
source-wordcount: '1469'
ht-degree: 40%

---


# [!DNL LiveRamp - Distribution] 连接 {#liveramp-onboarding}

此 [!DNL LiveRamp - Distribution] 通过connection，您可以激活移动设备、Web、显示和连接的电视媒体中的受众，从Experience Platform到高级发布者。

>[!IMPORTANT]
>
>此目标连接器和文档页面由LiveRamp创建和维护。 如有任何查询或更新请求，请直接联系LiveRamp [此处](mailto:example@email.com).

## 支持的目标 {#supported-destinations}

[!DNL LiveRamp - Distribution] 当前支持对以下平台进行受众激活：

* [!DNL 4C Insights]
* [!DNL Acast]
* [!DNL Amobee]
* [!DNL Ampersand.tv]
* [!DNL Captify]
* [!DNL Cardlytics]
* [[!DNL Disney (Hulu/ESPN/ABC)]](#disney)
* [!DNL iHeartMedia]
* [!DNL Index Exchange]
* [!DNL Magnite CTV Platform]
* [!DNL Magnite DV+ (Rubicon Project)]
* [!DNL One Fox]
* [!DNL Pandora]
* [!DNL Reddit]
* [[!DNL Roku]](#roku)
* [!DNL Spotify]
* [!DNL Taboola]
* [!DNL TargetSpot]
* [!DNL Teads]
* [!DNL WB Discovery]

## 用例 {#use-cases}

为了帮助您更好地了解您应该如何以及何时使用 [!DNL LiveRamp - Distribution] 目标，以下是Adobe Experience Platform客户可以使用此目标解决的示例用例。

一家运动服装零售商的营销团队使用了 [LiveRamp — 入门](liveramp-onboarding.md) 用于将受众从Experience Platform发送到其LiveRamp帐户的连接。

通过 [!DNL LiveRamp - Distribution] 连接：他们现在可以触发将已载入受众激活到本页面顶部提到的目标，以便他们可以在移动设备、打开Web、社交和网站中定位用户。 [!DNL CTV] 平台。

## 将受众载入LiveRamp {#onboarding}

在通过激活受众之前 [!DNL LiveRamp - Distribution] connection，使用 [LiveRamp — 入门](liveramp-onboarding.md) 用于将Experience Platform受众导出到LiveRamp的连接。

将受众载入LiveRamp后，请从继续激活工作流 [连接到目标](#connect) 步骤。

## 连接到目标 {#connect}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_identifier_settings"
>title="标识符设置"
>abstract="选择您的目标支持的标识符。有关每个目标支持的标识符的完整列表，请参阅相关文档。"

>[!IMPORTANT]
> 
>要连接到目标，您需要 **[!UICONTROL 管理目标]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或与产品管理员联系以获取所需的权限。

要连接到此目标，请按照 [目标配置教程](../../ui/connect-destination.md). 在配置目标工作流中，填写下面两个部分中列出的字段。

### 向LiveRamp进行身份验证 {#authenticate}

要向目标进行身份验证，请填写必填字段并选择 **[!UICONTROL 连接到目标]**.

![显示目标连接屏幕的Platform UI图像。l](../../assets/catalog/advertising/liveramp-distribution/liveramp-distribution-new-connection.png)

* **[!UICONTROL 令牌URL]**：您的LiveRamp令牌网址。
* **[!UICONTROL LiveRamp组织ID]**：LiveRamp帐户的组织ID。
* **[!UICONTROL 用户名]**：您的LiveRamp帐户用户名。
* **[!UICONTROL 密码]**：您的LiveRamp帐户密码。

### 配置目标详细信息 {#destination-details}

成功连接到LiveRamp帐户后，输入所需信息以连接到要将受众激活到的目标。

![显示目标详细信息屏幕的Platform UI图像。l](../../assets/catalog/advertising/liveramp-distribution/liveramp-distribution-destination-details.png)

* **[!UICONTROL 名称]**：填写目标连接的首选名称。
* **[!UICONTROL 描述]**：输入目标的描述。 使用有助于您轻松识别此目标用途的描述。
* **[!UICONTROL 目标]**：使用下拉菜单选择要将受众激活到的目标。 您在此处选择的目标将直接影响您在 [目标特定的设置](#destination-settings) 屏幕。
* **[!UICONTROL 集成]**：选择要用于目标的集成帐户。
* **[!UICONTROL 标识符]**：选择目标支持的标识符。 目前，下拉菜单中预先填充了所有目标所支持的标识符。

## 目标特定的设置 {#destination-settings}

每个目标 [支持](#supported-destinations) 按 [!DNL LiveRamp - Onboarding] 需要您填写特定的配置选项。

有关如何配置每个目标的详细指导，请参阅以下部分。

### [!DNL 4C Insights] {#insights}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_4cinsights_profile_id"
>title="4C 品牌配置文件 ID"
>abstract="输入与您的 4C 品牌配置文件关联的数字 ID。如果您没有此 ID，请联系您的 4C 客户服务代表。"

要配置目标的详细信息，请填写下面的必需和可选字段。 UI中字段旁边的星号表示该字段为必填字段。

### [!DNL Acast] {#acast}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_acast_client"
>title="客户名称"
>abstract="您希望向目标合作伙伴显示的广告商帐户名称。使用您的公司名称。请勿使用空格或特殊字符。"

### [!DNL Amobee] {#amobee}

### [!DNL Ampersand.tv] {#ampersand-tv}

### [!DNL Captify] {#captify}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_captify_client"
>title="客户名称"
>abstract="您希望向目标合作伙伴显示的广告商帐户名称。使用您的公司名称。请勿使用空格或特殊字符。"

### [!DNL Cardlytics] {#cardlytics}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_cardlytics_client"
>title="客户名称"
>abstract="您希望向目标合作伙伴显示的广告商帐户名称。使用您的公司名称。请勿使用空格或特殊字符。"

### [!DNL Disney (Hulu/ESPN/ABC)] {#disney}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_agreement"
>title="广告商数据目标条款协议"
>abstract="键入 `I AGREE` 以确认认可并同意迪士尼广告商数据条款。"

<!-- 
>additional-url="https://www.disneyadvertising.com/ADVERTISER-DATA-DESTINATION-TERMS/" text="Read the agreement" -->

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_disney_client"
>title="客户名称"
>abstract="您希望向目标合作伙伴显示的广告商帐户名称。使用您的公司名称。请勿使用空格或特殊字符。"

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_disney_email"
>title="您的电子邮件地址"
>abstract="输入与个人关联的电子邮件地址。该电子邮件地址用作广告商数据条款协议的签名。如果需要，该电子邮件地址还将用于与您联系。"

要配置目标的详细信息，请填写以下字段。

![显示迪士尼目的地的客户数据字段的平台UI图像。](../../assets/catalog/advertising/liveramp-distribution/liveramp-distribution-disney-fields.png)

* **[!UICONTROL 广告商数据目标条款协议]**：键入 `I AGREE` 确认对迪士尼广告商数据条款的确认和同意。
* **[!UICONTROL 客户端名称]**：输入您希望向目标合作伙伴显示的公司名称。
* **[!UICONTROL 电子邮件地址]**：输入与个人关联的电子邮件地址。 该电子邮件地址用作广告商数据条款协议的签名。

### [!DNL iHeartMedia] {#iheartmedia}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_iheartmedia_client"
>title="客户名称"
>abstract="您希望向目标合作伙伴显示的广告商帐户名称。使用您的公司名称。请勿使用空格或特殊字符。"

### [!DNL Index Exchange] {#index-exchange}

### [!DNL Magnite CTV Platform] {#magnite}

### [!DNL Magnite DV+ (Rubicon Project)] {#magnite-dv}

### [!DNL One Fox] {#fox}

### [!DNL Pandora] {#pandora}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_pandora_data_provider_name"
>title="数据提供者名称"
>abstract="您希望向 Pandora 显示的公司名称。该名称最多可以包含 40 个小写字母和字母数字字符（例如 My_Company）。"

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_pandora_rep_email"
>title="客户代表电子邮件地址"
>abstract="您的 Pandora 客户代表的电子邮件地址。该地址用于发送分类更新。要输入多个地址，请用逗号分隔它们。"

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_email"
>title="电子邮件地址"
>abstract="该地址用于发送分类更新。要输入多个地址，请用逗号分隔它们。"

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_pandora_account_name"
>title="帐户名称"
>abstract="Pandora 帐户的名称。如果您不确定您的帐户名称是什么，请联系您的 Pandora 客户代表。请勿使用空格或特殊字符。"

### [!DNL Reddit] {#reddit}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_reddit_advertiser_id"
>title="Reddit 广告商 ID"
>abstract="您的 Reddit 广告商 ID。必须以“t2_”或“a2_”开头。如果您不知道自己的广告商 ID，请联系您的 Reddit 代表。"

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_reddit_advertiser_name"
>title="Reddit 广告商名称"
>abstract="您的 Reddit 广告商名称。请勿使用空格或特殊字符。"

### Roku {#roku}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_roku_email"
>title="Roku 帐户电子邮件地址"
>abstract="输入与您的 Roku 帐户关联的电子邮件地址。"

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_roku_representative_email"
>title="Roku 客户代表电子邮件地址"
>abstract="输入您的 Roku 客户代表的电子邮件地址。该地址用于发送分类更新。要输入多个地址，请用逗号分隔它们。"

要配置目标的详细信息，请填写以下字段。

![显示Roku目标所支持标识符的Platform UI图像。](../../assets/catalog/advertising/liveramp-distribution/liveramp-distribution-roku-fields.png)

* **[!UICONTROL Roku帐户电子邮件地址]**：输入与Roku帐户关联的电子邮件地址。
* **[!UICONTROL Roku客户代表电子邮件地址]**：输入您的Roku客户代表的电子邮件地址。 要输入多个地址，请用逗号分隔它们。

### [!DNL Spotify] {#spotify}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_spotify_client"
>title="客户名称"
>abstract="您希望向目标合作伙伴显示的广告商帐户名称。使用您的公司名称。请勿使用空格或特殊字符。"

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_spotify_account_token"
>title="帐户令牌"
>abstract="一个字母数字标识符，此标识符通知 Spotify 将数据移植到何处以及您已通过验证并可以使用此工作流。请联系您的 Spotify 客户经理以获取此令牌。"

### [!DNL Taboola] {#taboola}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_taboola_rep_email"
>title="客户经理电子邮件地址"
>abstract="您的 Taboola 客户经理的电子邮件地址。"

### [!DNL TargetSpot] {#targetspot}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_targetspot_client"
>title="客户名称"
>abstract="您希望向目标合作伙伴显示的广告商帐户名称。使用您的公司名称。请勿使用空格或特殊字符。"

### [!DNL Teads] {#teads}

### [!DNL WB Discovery] {#wb-discovery}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_wb_client"
>title="客户名称"
>abstract="您希望向目标合作伙伴显示的广告商帐户名称。使用您的公司名称。请勿使用空格或特殊字符。"

### 启用警报 {#enable-alerts}

您可以启用警报，以接收有关发送到目标的数据流状态的通知。 从列表中选择警报以订阅接收有关数据流状态的通知。 有关警报的详细信息，请阅读以下指南： [使用UI订阅目标警报](../../ui/alerts.md).

完成提供目标连接的详细信息后，选择 **[!UICONTROL 下一个]**.

## 将受众激活到此目标 {#activate}

>[!IMPORTANT]
> 
>要激活数据，您需要 **[!UICONTROL 管理目标]**， **[!UICONTROL 激活目标]**， **[!UICONTROL 查看配置文件]**、和 **[!UICONTROL 查看区段]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或与产品管理员联系以获取所需的权限。

此 [!DNL LiveRamp - Distribution] connection激活已通过LiveRamp帐户载入的受众 [LiveRamp — 入门](liveramp-onboarding.md) 连接。

要成功激活受众，在此步骤中，您必须选择 **相同受众** 您之前已登记到LiveRamp的用户。

>[!IMPORTANT]
>
>选择之前未载入到LiveRamp的受众，不会触发新受众的载入。

## 导出的数据/验证数据导出 {#exported-data}

要验证和监控受众的激活情况，请登录到您的LiveRamp帐户并检查激活指标。

如果您对Audience Activation存有任何疑问，请联系您的LiveRamp客户代表。

## 数据使用和治理 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 目标在处理您的数据时符合数据使用策略。 有关如何执行操作的详细信息 [!DNL Adobe Experience Platform] 实施数据管理，请阅读 [数据管理概述](/help/data-governance/home.md).

## 其他资源 {#additional-resources}

有关如何配置 [!DNL LiveRamp - Onboarding] 存储，请参见 [官方文档](https://docs.liveramp.com/connect/en/upload-a-file-via-liveramp-s-sftp.html).
