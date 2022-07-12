---
keywords: 飞艇标签；飞艇目的地
title: Airship Tags连接
description: 将Adobe受众数据无缝地作为受众标记传递到Airship，以便在Airship中进行定位。
exl-id: 84cf5504-f0b5-48d8-8da1-ff91ee1dc171
source-git-commit: fd2019feb25b540612a278cbea5bf5efafe284dc
workflow-type: tm+mt
source-wordcount: '947'
ht-degree: 1%

---

# [!DNL Airship Tags] 连接 {#airship-tags-destination}

## 概述

[!DNL Airship] 是领先的客户参与平台，可帮助您在客户生命周期的每个阶段向用户提供有意义的个性化全方位消息。

此集成将Adobe Experience Platform区段数据传递到 [!DNL Airship] as [标记](https://docs.airship.com/guides/audience/tags/) 进行定位或触发。

详细了解 [!DNL Airship]，请参阅 [Airship文档](https://docs.airship.com).


>[!TIP]
>
>此文档页面由 [!DNL Airship] 团队。 如有任何查询或更新请求，请直接联系 [support.airship.com](https://support.airship.com/).

## 先决条件

在将Adobe Experience Platform区段发送到 [!DNL Airship]，您必须：

* 在 [!DNL Airship] 项目。
* 生成用于身份验证的载体令牌。

>[!TIP]
> 
>创建 [!DNL Airship] 帐户通过 [此注册链接](https://go.airship.eu/accounts/register/plan/starter/) 如果您尚未访问，请执行以下操作：

## 导出类型和频度 {#export-type-frequency}

有关目标导出类型和频率的信息，请参阅下表。

| 项目 | 类型 | 注释 |
---------|----------|---------|
| 导出类型 | **[!UICONTROL 区段导出]** | 您正在导出区段（受众）的所有成员，以及Airship Tags目标中使用的标识符。 |
| 导出频度 | **[!UICONTROL 流]** | 流目标“始终运行”基于API的连接。 在基于区段评估的Experience Platform中更新用户档案后，连接器会立即将更新发送到目标平台下游。 有关更多信息 [流目标](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## 标签组

Adobe Experience Platform中的区段概念与 [标记](https://docs.airship.com/guides/audience/tags/) 在飞艇上，执行情况略有差异。 此集成映射用户的状态 [Experience Platform区段的成员资格](../../../xdm/field-groups/profile/segmentation.md) 对于 [!DNL Airship] 标记。 例如，在 `xdm:status` 更改 `realized`，则会将标记添加到 [!DNL Airship] 此配置文件映射到的渠道用户或指定用户。 如果 `xdm:status` 更改 `exited`，则会删除标记。

要启用此集成，请创建 *标记组* in [!DNL Airship] 已命名 `adobe-segments`.

>[!IMPORTANT]
>
>创建新标签组时 **不检查** 单选按钮上写着“[!DNL Allow these tags to be set only from your server]&quot; 这样做会导致Adobe标记集成失败。

请参阅 [管理标签组](https://docs.airship.com/tutorials/manage-project/messaging/tag-groups) 以了解有关创建标签组的说明。

## 生成载体令牌

转到 **[!UICONTROL 设置]** &quot; **[!UICONTROL API和集成]** 在 [飞艇仪表板](https://go.airship.com) 选择 **[!UICONTROL 令牌]** 菜单中。

单击 **[!UICONTROL 创建令牌]**.

为令牌提供用户友好名称(例如“Adobe标记目标”)，然后为角色选择“全部访问”。

单击 **[!UICONTROL 创建令牌]** 并将细节保存为机密。

## 用例

为了帮助您更好地了解应如何以及何时应使用 [!DNL Airship Tags] 目标中，以下是Adobe Experience Platform客户可以使用此目标解决的示例用例。

### 用例#1

零售商或娱乐平台可以根据忠诚客户创建用户配置文件，并将这些区段传递到 [!DNL Airship] ，用于在移动设备促销活动上进行消息定位。

### 用例#2

当用户进入或退出Adobe Experience Platform中的特定区段时，会实时触发一对一消息。

例如，一家零售商在Platform中设置一个特定于牛仔裤品牌的区段。 现在，当某人将其牛仔裤首选项设置为特定品牌时，该零售商可以触发移动消息。

## 连接到目标 {#connect}

>[!IMPORTANT]
> 
>要连接到目标，您需要 **[!UICONTROL 管理目标]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或联系您的产品管理员以获取所需的权限。

要连接到此目标，请按照 [目标配置教程](../../ui/connect-destination.md). 在配置目标工作流中，填写下面两节中列出的字段。

### 对目标进行身份验证 {#authenticate}

要对目标进行身份验证，请填写必填字段并选择 **[!UICONTROL 连接到目标]**.

* **[!UICONTROL 载体令牌]**:您从 [!DNL Airship] 功能板。

### 填写目标详细信息 {#destination-details}

要配置目标的详细信息，请填写以下必填和可选字段。 UI中字段旁边的星号表示该字段为必填字段。

* **[!UICONTROL 名称]**:输入一个名称，以帮助您标识此目标。
* **[!UICONTROL 描述]**:输入此目标的描述。
* **[!UICONTROL 域]**:选择美国或欧盟的数据中心，具体取决于 [!DNL Airship] 数据中心适用于此目标。

### 启用警报 {#enable-alerts}

您可以启用警报以接收有关目标数据流状态的通知。 从列表中选择警报以订阅接收有关数据流状态的通知。 有关警报的更多信息，请参阅 [使用UI订阅目标警报](../../ui/alerts.md).

完成提供目标连接的详细信息后，请选择 **[!UICONTROL 下一个]**.

## 将区段激活到此目标 {#activate}

>[!IMPORTANT]
> 
>要激活数据，您需要 **[!UICONTROL 管理目标]**, **[!UICONTROL 激活目标]**, **[!UICONTROL 查看配置文件]**&#x200B;和 **[!UICONTROL 查看区段]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或联系您的产品管理员以获取所需的权限。

请参阅 [将受众数据激活到流区段导出目标](../../ui/activate-segment-streaming-destinations.md) 有关将受众区段激活到此目标的说明。

## 映射注意事项 {#mapping-considerations}

[!DNL Airship] 可以在渠道(表示设备实例，如iPhone)或指定用户（将用户的所有设备映射到通用标识符，如客户ID）上设置标记。 如果您的架构中将纯文本（未经过哈希处理）电子邮件地址作为主标识，请在 **[!UICONTROL 源属性]** 并映射到 [!DNL Airship] 右列下的指定用户 **[!UICONTROL Target标识]**，如下所示。

![命名用户映射](../../assets/catalog/mobile-engagement/airship-tags/mapping-option-2.png)

对于应映射到渠道（即设备）的标识符，请根据源映射到相应的渠道。 下图显示了如何将Google广告ID映射到 [!DNL Airship] Android渠道。

![连接到Airship Tags](../../assets/catalog/mobile-engagement/airship-tags/select-source-identity.png)
![连接到Airship Tags](../../assets/catalog/mobile-engagement/airship-tags/select-target-identity.png)
![渠道映射](../../assets/catalog/mobile-engagement/airship-tags/mapping-option.png)

## 数据使用和管理 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 目标在处理数据时与数据使用策略相兼容。 有关如何 [!DNL Adobe Experience Platform] 实施数据管理，请参阅 [数据管理概述](../../../data-governance/home.md).
