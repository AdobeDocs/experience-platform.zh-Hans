---
keywords: 移动设备；炫耀；消息传送；
title: 钎焊连接
description: Braze是一个全面的客户参与平台，可在客户和他们喜爱的品牌之间提供相关且令人难忘的体验。
exl-id: 508e79ee-7364-4553-b153-c2c00cc85a73
source-git-commit: 3f31a54c0cf329d374808dacce3fac597a72aa11
workflow-type: tm+mt
source-wordcount: '1041'
ht-degree: 1%

---

# [!DNL Braze] 连接

## 概述 {#overview}

此 [!DNL Braze] 目标可帮助您将配置文件数据发送到 [!DNL Braze].

[!DNL Braze] 是一个全面的客户参与平台，为客户和他们喜爱的品牌之间令人难忘的相关体验提供支持。

要将配置文件数据发送到 [!DNL Braze]，您必须先连接到目标。

## 目标详情 {#specifics}

请注意以下特定于的详细信息 [!DNL Braze] 目标：

* [!DNL Adobe Experience Platform] 受众将导出到 [!DNL Braze] 在 `AdobeExperiencePlatformSegments` 属性。

>[!NOTE]
>
>请记住，将其他自定义属性发送到 [!DNL Braze] 可能会导致您的帐户数量 [!DNL Braze] 数据点消耗。 请咨询您的 [!DNL Braze] 帐户管理器。

## 用例 {#use-cases}

作为营销人员，我希望在移动参与目标中定位用户，并内置受众 [!DNL Adobe Experience Platform]. 此外，我还希望根据用户体验中的属性，为他们提供个性化体验 [!DNL Adobe Experience Platform] 用户档案，当受众和用户档案在中更新时 [!DNL Adobe Experience Platform].

## 支持的身份 {#supported-identities}

[!DNL Braze] 支持激活下表中描述的标识。

| 目标身份 | 描述 | 注意事项 |
|---|---|---|
| external_id | 自定义 [!DNL Braze] 支持映射任何标识的标识符。 | 您可以发送任何 [身份](../../../identity-service/namespaces.md) 到 [!DNL Braze] 目标，只要将其映射到 [!DNL Braze] [`external_id`](https://www.braze.com/docs/api/basics/#external-user-id-explanation). |

{style="table-layout:auto"}

## 外部受众支持 {#external-audiences-support}

所有目标都支持激活通过Experience Platform生成的受众 [分段服务](../../../segmentation/home.md).

此外，此目标还支持激活下表中描述的外部受众。

| 外部受众类型 | 描述 |
---------|----------|
| 自定义上传 | 从CSV文件引入到Experience Platform中的受众。 |

{style="table-layout:auto"}

## 导出类型和频率 {#export-type-frequency}

有关目标导出类型和频率的信息，请参阅下表。

| 项目 | 类型 | 注释 |
---------|----------|---------|
| 导出类型 | **[!UICONTROL 基于配置文件]** | 您正在根据字段映射导出区段的所有成员，以及所需的架构字段（例如：电子邮件地址、电话号码、姓氏）和/或身份。[!DNL Adobe Experience Platform] 受众将导出到 [!DNL Braze] 在 `AdobeExperiencePlatformSegments` 属性。 |
| 导出频率 | **[!UICONTROL 流]** | 流目标为基于API的“始终运行”连接。 根据受众评估在Experience Platform中更新用户档案后，连接器会立即将更新发送到下游目标平台。 详细了解 [流式目标](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## 连接到目标 {#connect}

>[!IMPORTANT]
> 
>要连接到目标，您需要 **[!UICONTROL 管理目标]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或与产品管理员联系以获取所需的权限。

要连接到此目标，请按照 [目标配置教程](../../ui/connect-destination.md). 在配置目标工作流中，填写下面两节中列出的字段。

### 向目标进行身份验证 {#authenticate}

要向目标进行身份验证，请填写必填字段并选择 **[!UICONTROL 连接到目标]**.

* **[!UICONTROL Braze帐户令牌]**：这是您的 [!DNL Braze] [!DNL API] 键。 您可以找到有关如何获取 [!DNL API] 此处键入： [REST API密钥概述](https://www.braze.com/docs/api/api_key/).

### 填写目标详细信息 {#destination-details}

要配置目标的详细信息，请填写下面的必需和可选字段。 UI中字段旁边的星号表示该字段为必填字段。

* **[!UICONTROL 名称]**：输入将来识别此目标时所依据的名称。
* **[!UICONTROL 描述]**：输入可帮助您将来识别此目标的描述。
* **[!UICONTROL 端点实例]**：询问您的 [!DNL Braze] 表示您应使用的端点实例。

### 启用警报 {#enable-alerts}

您可以启用警报，以接收有关流向目标的数据流状态的通知。 从列表中选择警报以订阅接收有关数据流状态的通知。 有关警报的更多信息，请参阅以下指南中的 [使用UI订阅目标警报](../../ui/alerts.md).

完成提供目标连接的详细信息后，选择 **[!UICONTROL 下一个]**.

## 将受众激活到此目标 {#activate}

>[!IMPORTANT]
> 
>要激活数据，您需要 **[!UICONTROL 管理目标]**， **[!UICONTROL 激活目标]**， **[!UICONTROL 查看配置文件]**、和 **[!UICONTROL 查看区段]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或与产品管理员联系以获取所需的权限。

参见 [将受众数据激活到流式受众导出目标](../../ui/activate-segment-streaming-destinations.md) 有关将受众激活到此目标的说明。

## 映射注意事项 {#mapping-considerations}

要正确发送受众数据，请执行以下操作： [!DNL Adobe Experience Platform] 到 [!DNL Braze] 目标，您需要完成字段映射步骤。

映射包括在 [!DNL Experience Data Model] (XDM)架构字段 [!DNL Platform] 帐户以及它们与目标目标对应的对等项。

要将XDM字段正确映射到 [!DNL Braze] 目标字段，请执行以下步骤：

在 [!UICONTROL 映射] 步骤，单击 **[!UICONTROL 添加新映射]**.

![钎焊目标添加映射](../../assets/catalog/mobile-engagement/braze/mapping.png)

在 [!UICONTROL 源字段] 部分，单击空字段旁边的箭头按钮。

![钎焊目标源映射](../../assets/catalog/mobile-engagement/braze/mapping-source.png)

在 [!UICONTROL 选择源字段] 窗口中，您可以选择以下两种类别的XDM字段：
* [!UICONTROL 选择属性]：使用此选项将特定字段从XDM架构映射到 [!DNL Braze] 属性。

![钎焊目标映射源属性](../../assets/catalog/mobile-engagement/braze/mapping-attributes.png)

* [!UICONTROL 选择身份命名空间]：使用此选项映射 [!DNL Platform] 将身份命名空间更改为 [!DNL Braze] 命名空间。

![钎焊目标映射源命名空间](../../assets/catalog/mobile-engagement/braze/mapping-namespaces.png)

选择源字段，然后单击 **[!UICONTROL 选择]**.

在 [!UICONTROL 目标字段] 部分，单击字段右侧的映射图标。

![钎焊目标映射](../../assets/catalog/mobile-engagement/braze/mapping-target.png)

在 [!UICONTROL 选择目标字段] 窗口中，您可以选择以下两种类别的目标字段：
* [!UICONTROL 选择身份命名空间]：使用此选项进行映射 [!DNL Platform] 身份命名空间到 [!DNL Braze] 身份命名空间。
* [!UICONTROL 选择自定义属性]：使用此选项可将XDM属性映射到自定义 [!DNL Braze] 您在 [!DNL Braze] 帐户。 <br> 您还可以使用此选项将现有XDM属性重命名为 [!DNL Braze]. 例如，映射 `lastName` 自定义的XDM属性 `Last_Name` 中的属性 [!DNL Braze]，将创建 `Last_Name` 中的属性 [!DNL Braze]，如果它尚不存在，则映射 `lastName` XDM属性。

![钎焊目标映射字段](../../assets/catalog/mobile-engagement/braze/mapping-target-fields.png)

选择目标字段，然后单击 **[!UICONTROL 选择]**.

现在，您应该会在列表中看到字段映射。

![钎焊目标映射完成](../../assets/catalog/mobile-engagement/braze/mapping-complete.png)

要添加更多映射，请重复上述步骤。

## 映射示例 {#mapping-example}

比如您的XDM配置文件架构和 [!DNL Braze] 实例包含以下属性和身份：

|  | XDM配置文件架构 | [!DNL Braze] 实例 |
|---|---|---|
| 属性 | <ul><li><code>person.name.firstName</code></li><li><code>person.name.lastName</code></li><li><code>mobilePhone.number</code></li></ul> | <ul><li><code>名字</code></li><li><code>姓氏</code></li><li><code>电话号码</code></li></ul> |
| 标识 | <ul><li><code>电子邮件</code></li><li><code>Google Ad ID (GAID)</code></li><li><code>广告商的Apple ID (IDFA)</code></li></ul> | <ul><li><code>external_id</code></li></ul> |

正确的映射将如下所示：

![钎焊目标映射示例](../../assets/catalog/mobile-engagement/braze/mapping-example.png)

## 导出的数据 {#exported-data}

验证数据是否已成功导出到 [!DNL Braze] 目标，检查您的 [!DNL Braze] 帐户。 [!DNL Adobe Experience Platform] 受众将导出到 [!DNL Braze] 在 `AdobeExperiencePlatformSegments` 属性。

## 数据使用和管理 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 目标在处理您的数据时符合数据使用策略。 有关以下方面的详细信息： [!DNL Adobe Experience Platform] 强制执行数据管理，请参见 [数据治理概述](../../../data-governance/home.md).
