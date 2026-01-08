---
keywords: 移动设备；炫耀；消息传送；
title: 钎焊连接
description: Braze是一个全面的客户参与平台，可为客户与他们所喜爱的品牌之间提供相关且令人难忘的体验。
last-substantial-update: 2024-08-20T00:00:00Z
exl-id: 508e79ee-7364-4553-b153-c2c00cc85a73
source-git-commit: cc97efec5fba090378ceaf73441d0b4bd7fbf51f
workflow-type: tm+mt
source-wordcount: '1078'
ht-degree: 2%

---

# [!DNL Braze]连接

## 概述 {#overview}

[!DNL Braze]目标可帮助您将配置文件数据发送至[!DNL Braze]。

[!DNL Braze]是一个全面的客户参与平台，可为客户和他们喜爱的品牌之间提供相关且令人难忘的体验。

若要将配置文件数据发送到[!DNL Braze]，您必须先连接到目标。

## 目标详情 {#specifics}

请注意以下特定于[!DNL Braze]目标的详细信息：

* [!DNL Adobe Experience Platform]受众导出到[!DNL Braze]属性下的`AdobeExperiencePlatformSegments`。

>[!NOTE]
>
>请记住，向[!DNL Braze]发送其他自定义属性可能会导致您的[!DNL Braze]数据点使用量增加。 在发送其他自定义属性之前，请咨询您的[!DNL Braze]帐户管理员。

## 用例 {#use-cases}

作为营销人员，我希望在移动参与目标中定位用户，并在[!DNL Adobe Experience Platform]中内置受众。 此外，我希望在[!DNL Adobe Experience Platform]中更新受众和配置文件后，根据其[!DNL Adobe Experience Platform]配置文件中的属性，向他们提供个性化体验。

## 支持的身份 {#supported-identities}

[!DNL Braze]支持激活下表中描述的标识。

| 目标身份 | 描述 | 注意事项 |
|---|---|---|
| external_id | 支持映射任何标识的自定义[!DNL Braze]标识符。 | 只要将任何[标识](../../../identity-service/features/namespaces.md)映射到[!DNL Braze] [!DNL Braze][`external_id`，就可以将其发送到](https://www.braze.com/docs/api/basics/#external-user-id-explanation)目标。 |

{style="table-layout:auto"}

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
| 导出类型 | **[!UICONTROL Profile-based]** | 您正在导出区段的所有成员，以及所需的架构字段（例如：电子邮件地址、电话号码、姓氏）和/或身份（根据字段映射）。[!DNL Adobe Experience Platform]受众导出到[!DNL Braze]属性下的`AdobeExperiencePlatformSegments`。 |
| 导出频率 | **[!UICONTROL Streaming]** | 流目标为基于API的“始终运行”连接。 根据受众评估在Experience Platform中更新用户档案后，连接器会立即将更新发送到下游目标平台。 阅读有关[流式目标](/help/destinations/destination-types.md#streaming-destinations)的更多信息。 |

{style="table-layout:auto"}

## 连接到目标 {#connect}

>[!IMPORTANT]
> 
>若要连接到目标，您需要&#x200B;**[!UICONTROL View Destinations]**&#x200B;和&#x200B;**[!UICONTROL Manage Destinations]** [访问控制权限](/help/access-control/home.md#permissions)。 阅读[访问控制概述](/help/access-control/ui/overview.md)或联系您的产品管理员以获取所需的权限。

要连接到此目标，请按照[目标配置教程](../../ui/connect-destination.md)中描述的步骤操作。 在配置目标工作流中，填写下面两个部分中列出的字段。

### 验证目标 {#authenticate}

要验证目标，请填写必填字段并选择&#x200B;**[!UICONTROL Connect to destination]**。

* **[!UICONTROL Braze account token]**：这是您的[!DNL Braze] [!DNL API]密钥。 您可以在此处找到有关如何获取[!DNL API]密钥的详细说明： [REST API密钥概述](https://www.braze.com/docs/api/api_key/)。

### 填写目标详细信息 {#destination-details}

要配置目标的详细信息，请填写下面的必需和可选字段。 UI中字段旁边的星号表示该字段为必填字段。

* **[!UICONTROL Name]**：输入一个名称，您以后将通过该名称识别此目标。
* **[!UICONTROL Description]**：输入可帮助您将来识别此目标的描述。
* **[!UICONTROL Endpoint Instance]**： [支持的所有](https://www.braze.com/docs/user_guide/administrative/access_braze/sdk_endpoints)区域特定的端点[!DNL Braze]均可供选择。 询问您的[!DNL Braze]代表您应使用哪个端点实例。

### 启用警报 {#enable-alerts}

您可以启用警报，以接收有关发送到目标的数据流状态的通知。 从列表中选择警报以订阅接收有关数据流状态的通知。 有关警报的详细信息，请参阅[使用UI订阅目标警报的指南](../../ui/alerts.md)。

完成提供目标连接的详细信息后，选择&#x200B;**[!UICONTROL Next]**。

## 激活此目标的受众 {#activate}

>[!IMPORTANT]
> 
>* 若要激活数据，您需要&#x200B;**[!UICONTROL View Destinations]**、**[!UICONTROL Activate Destinations]**、**[!UICONTROL View Profiles]**&#x200B;和&#x200B;**[!UICONTROL View Segments]** [访问控制权限](/help/access-control/home.md#permissions)。 阅读[访问控制概述](/help/access-control/ui/overview.md)或联系您的产品管理员以获取所需的权限。
>* 要导出&#x200B;*标识*，您需要&#x200B;**[!UICONTROL View Identity Graph]** [访问控制权限](/help/access-control/home.md#permissions)。<br> ![选择工作流中突出显示的身份命名空间以将受众激活到目标。](/help/destinations/assets/overview/export-identities-to-destination.png "选择工作流中突出显示的身份命名空间以将受众激活到目标。"){width="100" zoomable="yes"}

有关将受众激活到此目标的说明，请参阅[将受众数据激活到流式受众导出目标](../../ui/activate-segment-streaming-destinations.md)。

## 映射注意事项 {#mapping-considerations}

要将受众数据从[!DNL Adobe Experience Platform]正确发送到[!DNL Braze]目标，您需要执行字段映射步骤。

映射包括在[!DNL Experience Data Model]帐户中的[!DNL Experience Platform] (XDM)架构字段及其来自目标目标的对应项之间创建链接。

要将XDM字段正确映射到[!DNL Braze]目标字段，请执行以下步骤：

在[!UICONTROL Mapping]步骤中，单击&#x200B;**[!UICONTROL Add new mapping]**。

![钎焊目标添加映射](../../assets/catalog/mobile-engagement/braze/mapping.png)

在[!UICONTROL Source Field]部分中，单击空字段旁边的箭头按钮。

![钎焊目标Source映射](../../assets/catalog/mobile-engagement/braze/mapping-source.png)

在[!UICONTROL Select source field]窗口中，您可以选择以下两种类别的XDM字段：

* [!UICONTROL Select attributes]：使用此选项将XDM架构中的特定字段映射到[!DNL Braze]属性。

![钎焊目标映射Source属性](../../assets/catalog/mobile-engagement/braze/mapping-attributes.png)

* [!UICONTROL Select identity namespace]：使用此选项将[!DNL Experience Platform]身份命名空间映射到[!DNL Braze]命名空间。

![钎焊目标映射Source命名空间](../../assets/catalog/mobile-engagement/braze/mapping-namespaces.png)

选择源字段，然后单击&#x200B;**[!UICONTROL Select]**。

在[!UICONTROL Target Field]部分中，单击字段右侧的映射图标。

![钎焊目标映射](../../assets/catalog/mobile-engagement/braze/mapping-target.png)

在[!UICONTROL Select target field]窗口中，您可以选择以下两种目标字段类别：

* [!UICONTROL Select identity namespace]：使用此选项将[!DNL Experience Platform]身份命名空间映射到[!DNL Braze]身份命名空间。
* [!UICONTROL Select custom attributes]：使用此选项将XDM属性映射到您在[!DNL Braze]帐户中定义的自定义[!DNL Braze]属性。 <br>您还可以使用此选项将现有XDM属性重命名为[!DNL Braze]。 例如，将`lastName` XDM属性映射到`Last_Name`中的自定义[!DNL Braze]属性，将在`Last_Name`中创建[!DNL Braze]属性（如果该属性不存在），并将`lastName` XDM属性映射到它。

![钎焊目标映射字段](../../assets/catalog/mobile-engagement/braze/mapping-target-fields.png)

选择您的目标字段，然后单击&#x200B;**[!UICONTROL Select]**。

您现在应在列表中看到字段映射。

![钎焊目标映射完成](../../assets/catalog/mobile-engagement/braze/mapping-complete.png)

要添加更多映射，请重复上述步骤。

## 映射示例 {#mapping-example}

假设您的XDM配置文件架构和[!DNL Braze]实例包含以下属性和身份：

|  | XDM配置文件架构 | [!DNL Braze]实例 |
|---|---|---|
| 属性 | <ul><li><code>人员。姓名。名字</code></li><li><code>person.name.lastName</code></li><li><code>手机号码</code></li></ul> | <ul><li><code>名字</code></li><li><code>姓氏</code></li><li><code>电话号码</code></li></ul> |
| 身份标识 | <ul><li><code>电子邮件</code></li><li><code>Google广告ID (GAID)</code></li><li>广告商的<code>Apple ID (IDFA)</code></li></ul> | <ul><li><code>external_id</code></li></ul> |

正确的映射将如下所示：

![钎焊目标映射示例](../../assets/catalog/mobile-engagement/braze/mapping-example.png)

## 导出的数据 {#exported-data}

要验证数据是否已成功导出到[!DNL Braze]目标，请检查您的[!DNL Braze]帐户。 [!DNL Adobe Experience Platform]受众导出到[!DNL Braze]属性下的`AdobeExperiencePlatformSegments`。

## 故障排除 {#troubleshooting}

将受众激活到此目标时，**我收到超时错误。 我应该怎么做？**

有时，激活此目标的受众可能会导致超时错误。 此错误并不表示存在激活问题。

如果收到超时错误，请检查目标平台中的受众大小。 如果受众规模正确，则集成可按预期运行。

## 数据使用和治理 {#data-usage-governance}

在处理您的数据时，所有[!DNL Adobe Experience Platform]目标都符合数据使用策略。 有关[!DNL Adobe Experience Platform]如何实施数据治理的详细信息，请参阅[数据治理概述](../../../data-governance/home.md)。
