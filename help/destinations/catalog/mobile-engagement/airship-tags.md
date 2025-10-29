---
keywords: 飞艇标签；飞艇目标
title: 飞艇标记连接
description: 将Adobe受众数据作为受众标记无缝传递到飞艇，以便在飞艇中进行定位。
exl-id: 84cf5504-f0b5-48d8-8da1-ff91ee1dc171
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '934'
ht-degree: 2%

---

# [!DNL Airship Tags]连接 {#airship-tags-destination}

## 概述

[!DNL Airship]是领先的客户参与平台，帮助您在客户生命周期的每个阶段都向用户传递有意义、个性化的全渠道信息。

此集成将Adobe Experience Platform受众数据作为[!DNL Airship]标记[传递到](https://docs.airship.com/guides/audience/tags/)中，以进行定位或触发。

若要了解有关[!DNL Airship]的更多信息，请参阅[飞艇文档](https://docs.airship.com)。


>[!TIP]
>
>此目标连接器和文档页面由[!DNL Airship]团队创建和维护。 如有任何查询或更新请求，请直接通过[support.airship.com](https://support.airship.com/)联系他们。

## 先决条件

在将Adobe Experience Platform受众发送到[!DNL Airship]之前，您必须：

* 在您的[!DNL Airship]项目中创建标记组。
* 生成持有者令牌以进行身份验证。

>[!TIP]
> 
>通过[!DNL Airship]此注册链接[创建一个](https://go.airship.eu/accounts/register/plan/starter/)帐户（如果尚未创建）。

## 支持的受众 {#supported-audiences}

此部分介绍哪些类型的受众可以导出到此目标。

| 受众来源 | 支持 | 描述 |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | 通过Experience Platform [分段服务](../../../segmentation/home.md)生成的受众。 |
| 自定义上传 | ✓ | 受众[已从CSV文件将](../../../segmentation/ui/audience-portal.md#import-audience)导入Experience Platform。 |

{style="table-layout:auto"}

## 导出类型和频率 {#export-type-frequency}

有关目标导出类型和频率的信息，请参阅下表。

| 项目 | 类型 | 注释 |
|---------|----------|---------|
| 导出类型 | **[!UICONTROL Audience export]** | 您正在导出具有飞艇标记目标中所用标识符的受众的所有成员。 |
| 导出频率 | **[!UICONTROL Streaming]** | 流目标为基于API的“始终运行”连接。 根据受众评估在Experience Platform中更新用户档案后，连接器会立即将更新发送到下游目标平台。 阅读有关[流式目标](/help/destinations/destination-types.md#streaming-destinations)的更多信息。 |

{style="table-layout:auto"}

## 标记组

Adobe Experience Platform中的受众概念与Airship中的[标记](https://docs.airship.com/guides/audience/tags/)类似，在实施上略有差异。 此集成将用户在Experience Platform区段[中的](../../../xdm/field-groups/profile/segmentation.md)成员资格状态映射到[!DNL Airship]标记的存在或不存在。 例如，在`xdm:status`更改为`realized`的Experience Platform受众中，标记已添加到此配置文件映射到的[!DNL Airship]渠道或命名用户。 如果`xdm:status`更改为`exited`，则标记将被删除。

要启用此集成，请在&#x200B;*中创建名为*&#x200B;的[!DNL Airship]标记组`adobe-segments`。

>[!IMPORTANT]
>
>创建新标记组时&#x200B;**请勿选中**&#x200B;显示“[!DNL Allow these tags to be set only from your server]”的单选按钮。 这样做会导致Adobe标记集成失败。

有关创建标记组的说明，请参阅[管理标记组](https://docs.airship.com/tutorials/manage-project/messaging/tag-groups)。

## 生成持有者令牌

转到&#x200B;**[!UICONTROL Settings]**&#x200B;飞艇仪表板&#x200B;**[!UICONTROL APIs & Integrations]**&#x200B;中的[&#x200B; &#39;&#39; &#x200B;](https://go.airship.com)，然后在左侧菜单中选择&#x200B;**[!UICONTROL Tokens]**。

单击 **[!UICONTROL Create Token]**。

为您的令牌提供一个用户友好的名称，例如“Adobe标记目标”，并为该角色选择“完全访问”。

单击&#x200B;**[!UICONTROL Create Token]**&#x200B;并将详细信息保存为机密。

## 用例

为了帮助您更好地了解您应如何以及何时使用[!DNL Airship Tags]目标，以下是Adobe Experience Platform客户可以使用此目标解决的示例用例。

### 用例#1

零售商或娱乐平台可以创建其忠诚度客户的用户配置文件，并将这些受众传递到[!DNL Airship]中以针对移动营销活动进行消息定位。

### 用例#2

当用户归属或退出Adobe Experience Platform中的特定受众时，实时触发一对一消息。

例如，retailer在Experience Platform中设置特定于牛仔裤品牌的受众。 retailer现在可以在用户将其牛仔裤首选项设置为特定品牌后立即触发移动消息。

## 连接到目标 {#connect}

>[!IMPORTANT]
> 
>若要连接到目标，您需要&#x200B;**[!UICONTROL View Destinations]**&#x200B;和&#x200B;**[!UICONTROL Manage Destinations]** [访问控制权限](/help/access-control/home.md#permissions)。 阅读[访问控制概述](/help/access-control/ui/overview.md)或联系您的产品管理员以获取所需的权限。

要连接到此目标，请按照[目标配置教程](../../ui/connect-destination.md)中描述的步骤操作。 在配置目标工作流中，填写下面两个部分中列出的字段。

### 验证目标 {#authenticate}

要验证目标，请填写必填字段并选择&#x200B;**[!UICONTROL Connect to destination]**。

* **[!UICONTROL Bearer token]**：您从[!DNL Airship]仪表板生成的持有者令牌。

### 填写目标详细信息 {#destination-details}

要配置目标的详细信息，请填写下面的必需和可选字段。 UI中字段旁边的星号表示该字段为必填字段。

* **[!UICONTROL Name]**：输入有助于识别此目标的名称。
* **[!UICONTROL Description]**：输入此目标的描述。
* **[!UICONTROL Domain]**：选择美国或欧盟数据中心，具体取决于哪个[!DNL Airship]数据中心适用于此目标。

### 启用警报 {#enable-alerts}

您可以启用警报，以接收有关发送到目标的数据流状态的通知。 从列表中选择警报以订阅接收有关数据流状态的通知。 有关警报的详细信息，请参阅[使用UI订阅目标警报的指南](../../ui/alerts.md)。

完成提供目标连接的详细信息后，选择&#x200B;**[!UICONTROL Next]**。

## 激活此目标的受众 {#activate}

>[!IMPORTANT]
> 
>若要激活数据，您需要&#x200B;**[!UICONTROL View Destinations]**、**[!UICONTROL Activate Destinations]**、**[!UICONTROL View Profiles]**&#x200B;和&#x200B;**[!UICONTROL View Segments]** [访问控制权限](/help/access-control/home.md#permissions)。 阅读[访问控制概述](/help/access-control/ui/overview.md)或联系您的产品管理员以获取所需的权限。

有关将受众激活到此目标的说明，请参阅[将受众数据激活到流式受众导出目标](../../ui/activate-segment-streaming-destinations.md)。

## 映射注意事项 {#mapping-considerations}

[!DNL Airship]标记可以在渠道上设置，该渠道表示设备实例，如iPhone，也可以设置指定用户，该指定用户将用户的所有设备映射到通用标识符，如客户ID。 如果您的架构中将纯文本（未散列）电子邮件地址作为主标识，请选择&#x200B;**[!UICONTROL Source Attributes]**&#x200B;中的电子邮件字段，并映射到[!DNL Airship]下右列的&#x200B;**[!UICONTROL Target Identities]**&#x200B;指定用户，如下所示。

![命名用户映射](../../assets/catalog/mobile-engagement/airship-tags/mapping-option-2.png)

对于应映射到通道（即设备）的标识符，请根据源映射到相应的通道。 下图显示了如何将Google Advertising ID映射到[!DNL Airship] Android渠道。

![连接到飞艇标签](../../assets/catalog/mobile-engagement/airship-tags/select-source-identity.png)
![连接到飞艇标签](../../assets/catalog/mobile-engagement/airship-tags/select-target-identity.png)
![渠道映射](../../assets/catalog/mobile-engagement/airship-tags/mapping-option.png)

## 数据使用和治理 {#data-usage-governance}

在处理您的数据时，所有[!DNL Adobe Experience Platform]目标都符合数据使用策略。 有关[!DNL Adobe Experience Platform]如何实施数据治理的详细信息，请参阅[数据治理概述](../../../data-governance/home.md)。
