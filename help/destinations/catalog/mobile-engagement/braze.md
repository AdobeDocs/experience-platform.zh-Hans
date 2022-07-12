---
keywords: 移动设备；布雷；报文传送；
title: Braze连接
description: Braze是一个全面的客户参与平台，可为客户和他们喜爱的品牌之间提供相关且令人难忘的体验。
exl-id: 508e79ee-7364-4553-b153-c2c00cc85a73
source-git-commit: fd2019feb25b540612a278cbea5bf5efafe284dc
workflow-type: tm+mt
source-wordcount: '1001'
ht-degree: 1%

---

# [!DNL Braze] 连接

## 概述 {#overview}

的 [!DNL Braze] 目标可帮助您将用户档案数据发送到 [!DNL Braze].

[!DNL Braze] 是一个全面的客户参与平台，可为客户和他们喜爱的品牌之间提供相关且难忘的体验。

将用户档案数据发送到 [!DNL Braze]，则必须先连接到目标。

## 目标详情 {#specifics}

请注意以下特定于 [!DNL Braze] 目标：

* [!DNL Adobe Experience Platform] 区段导出到 [!DNL Braze] 下 `AdobeExperiencePlatformSegments` 属性。

>[!NOTE]
>
>请记住，将其他自定义属性发送到 [!DNL Braze] 可能会导致 [!DNL Braze] 数据点使用情况。 请咨询您的 [!DNL Braze] 帐户管理器。

## 用例 {#use-cases}

作为营销人员，我希望在移动设备参与目标中定位用户，并内置区段 [!DNL Adobe Experience Platform]. 此外，我还希望根据访客的属性为他们提供个性化体验 [!DNL Adobe Experience Platform] 用户档案，在 [!DNL Adobe Experience Platform].

## 支持的身份 {#supported-identities}

[!DNL Braze] 支持激活下表所述的身份。

| Target标识 | 描述 | 注意事项 |
|---|---|---|
| external_id | 自定义 [!DNL Braze] 支持映射任何标识的标识符。 | 您可以发送任何 [身份](../../../identity-service/namespaces.md) 到 [!DNL Braze] 目标位置，只要您将其映射到 [!DNL Braze] [`external_id`](https://www.braze.com/docs/api/basics/#external-user-id-explanation). |

{style=&quot;table-layout:auto&quot;}

## 导出类型和频度 {#export-type-frequency}

有关目标导出类型和频率的信息，请参阅下表。

| 项目 | 类型 | 注释 |
---------|----------|---------|
| 导出类型 | **[!UICONTROL 基于用户档案]** | 您要导出区段的所有成员，以及所需的架构字段(例如：电子邮件地址、电话号码、姓氏)和/或身份，具体取决于字段映射。[!DNL Adobe Experience Platform] 区段导出到 [!DNL Braze] 下 `AdobeExperiencePlatformSegments` 属性。 |
| 导出频度 | **[!UICONTROL 流]** | 流目标“始终运行”基于API的连接。 在基于区段评估的Experience Platform中更新用户档案后，连接器会立即将更新发送到目标平台下游。 有关更多信息 [流目标](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## 连接到目标 {#connect}

>[!IMPORTANT]
> 
>要连接到目标，您需要 **[!UICONTROL 管理目标]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或联系您的产品管理员以获取所需的权限。

要连接到此目标，请按照 [目标配置教程](../../ui/connect-destination.md). 在配置目标工作流中，填写下面两节中列出的字段。

### 对目标进行身份验证 {#authenticate}

要对目标进行身份验证，请填写必填字段并选择 **[!UICONTROL 连接到目标]**.

* **[!UICONTROL Braze帐户令牌]**:这是您的 [!DNL Braze] [!DNL API] 键。 您可以找到有关如何获取 [!DNL API] 键： [REST API密钥概述](https://www.braze.com/docs/api/api_key/).

### 填写目标详细信息 {#destination-details}

要配置目标的详细信息，请填写以下必填和可选字段。 UI中字段旁边的星号表示该字段为必填字段。

* **[!UICONTROL 名称]**:输入一个名称，在将来，您将通过该名称来识别此目标。
* **[!UICONTROL 描述]**:输入描述，以帮助您在将来标识此目标。
* **[!UICONTROL 端点实例]**:询问 [!DNL Braze] 代表您应使用的端点实例。

### 启用警报 {#enable-alerts}

您可以启用警报以接收有关目标数据流状态的通知。 从列表中选择警报以订阅接收有关数据流状态的通知。 有关警报的更多信息，请参阅 [使用UI订阅目标警报](../../ui/alerts.md).

完成提供目标连接的详细信息后，请选择 **[!UICONTROL 下一个]**.

## 将区段激活到此目标 {#activate}

>[!IMPORTANT]
> 
>要激活数据，您需要 **[!UICONTROL 管理目标]**, **[!UICONTROL 激活目标]**, **[!UICONTROL 查看配置文件]**&#x200B;和 **[!UICONTROL 查看区段]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或联系您的产品管理员以获取所需的权限。

请参阅 [将受众数据激活到流区段导出目标](../../ui/activate-segment-streaming-destinations.md) 有关将受众区段激活到此目标的说明。

## 映射注意事项 {#mapping-considerations}

要正确发送受众数据，请执行以下操作 [!DNL Adobe Experience Platform] 到 [!DNL Braze] 目标，您需要完成字段映射步骤。

映射包括在 [!DNL Experience Data Model] (XDM)架构字段 [!DNL Platform] 帐户，以及目标目标中的相应对等项。

要将XDM字段正确映射到 [!DNL Braze] 目标字段，请执行以下步骤：

在 [!UICONTROL 映射] 步骤，单击 **[!UICONTROL 添加新映射]**.

![制作目标添加映射](../../assets/catalog/mobile-engagement/braze/mapping.png)

在 [!UICONTROL 源字段] 中，单击空字段旁边的箭头按钮。

![Braze目标源映射](../../assets/catalog/mobile-engagement/braze/mapping-source.png)

在 [!UICONTROL 选择源字段] 窗口中，您可以选择以下两类XDM字段：
* [!UICONTROL 选择属性]:使用此选项可将XDM架构中的特定字段映射到 [!DNL Braze] 属性。

![Braze目标映射源属性](../../assets/catalog/mobile-engagement/braze/mapping-attributes.png)

* [!UICONTROL 选择身份命名空间]:使用此选项可映射 [!DNL Platform] 标识命名空间 [!DNL Braze] 命名空间。

![Braze目标映射源命名空间](../../assets/catalog/mobile-engagement/braze/mapping-namespaces.png)

选择源字段，然后单击 **[!UICONTROL 选择]**.

在 [!UICONTROL 目标字段] ，请单击字段右侧的映射图标。

![制作目标映射](../../assets/catalog/mobile-engagement/braze/mapping-target.png)

在 [!UICONTROL 选择目标字段] 窗口中，您可以选择以下两类目标字段：
* [!UICONTROL 选择身份命名空间]:使用此选项可映射 [!DNL Platform] 标识命名空间 [!DNL Braze] 身份命名空间。
* [!UICONTROL 选择自定义属性]:使用此选项可将XDM属性映射到自定义 [!DNL Braze] 您在 [!DNL Braze] 帐户。 <br> 您还可以使用此选项将现有XDM属性重命名为 [!DNL Braze]. 例如，映射 `lastName` 自定义的XDM属性 `Last_Name` 属性 [!DNL Braze]，将创建 `Last_Name` 属性 [!DNL Braze]，如果它不存在，则映射 `lastName` XDM属性。

![标记目标映射字段](../../assets/catalog/mobile-engagement/braze/mapping-target-fields.png)

选择目标字段，然后单击 **[!UICONTROL 选择]**.

此时，您应会在列表中看到字段映射。

![制作目标映射完成](../../assets/catalog/mobile-engagement/braze/mapping-complete.png)

要添加更多映射，请重复上述步骤。

## 映射示例 {#mapping-example}

假设您的XDM配置文件架构和 [!DNL Braze] 实例包含以下属性和标识：

|  | XDM配置文件架构 | [!DNL Braze] 实例 |
|---|---|---|
| 属性 | <ul><li>person.name.firstName</code></li><li>person.name.lastName</code></li><li>mobilePhone.number</code></li></ul> | <ul><li>名字</code></li><li>LastName</code></li><li>电话号码</code></li></ul> |
| 标识 | <ul><li>电子邮件</code></li><li>Google广告ID(GAID)</code></li><li>Apple Id For Advertisers(IDFA)</code></li></ul> | <ul><li>external_id</code></li></ul> |

正确的映射将如下所示：

![布雷兹目标映射示例](../../assets/catalog/mobile-engagement/braze/mapping-example.png)

## 导出的数据 {#exported-data}

验证数据是否已成功导出到 [!DNL Braze] 目标位置，检查 [!DNL Braze] 帐户。 [!DNL Adobe Experience Platform] 区段导出到 [!DNL Braze] 下 `AdobeExperiencePlatformSegments` 属性。

## 数据使用和管理 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 目标在处理数据时与数据使用策略相兼容。 有关如何 [!DNL Adobe Experience Platform] 实施数据管理，请参阅 [数据管理概述](../../../data-governance/home.md).
