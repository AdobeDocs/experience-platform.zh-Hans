---
keywords: 飞艇属性；飞艇目标
title: 飞艇属性连接
description: 将Adobe受众数据作为受众属性无缝传递到飞艇，以便在飞艇中进行定位。
exl-id: bfc1b52f-2d68-40d6-9052-c2ee1e877961
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1153'
ht-degree: 3%

---

# [!DNL Airship Attributes]连接 {#airship-attributes-destination}

>[!IMPORTANT]
>
>* 从2025年3月25日开始，您可以在目标目录中并排看到两张[!DNL Airship Attributes]信息卡。 这是由于目标服务内部升级造成的。现有[!DNL Airship Attributes]目标连接器已重命名为&#x200B;**[!UICONTROL （已弃用）飞艇属性]**，现在您可以使用名为&#x200B;**[!UICONTROL 飞艇属性]**&#x200B;的新信息卡。
>* 使用目录中的&#x200B;**[!UICONTROL 飞艇属性]**&#x200B;连接获取新的激活数据流。 如果您有任何到&#x200B;**[!UICONTROL （已弃用）飞艇属性]**&#x200B;目标的活动数据流，它们会自动更新，因此您无需执行任何操作。
>* 如果您是通过[流服务API](https://developer.adobe.com/experience-platform-apis/references/destinations/)创建数据流，则必须将[!DNL flow spec ID]和[!DNL connection spec ID]更新为以下值：
>   * 流量规范 ID：`a862e0be-966e-4e5a-80d3-1bb566461986`
>   * 连接规范 ID：`594bc002-4a47-49b7-8a98-ac0d21045502`

## 概述 {#overview}

[!DNL Airship]是领先的客户参与Experience Platform，帮助您在客户生命周期的每个阶段都向用户传递有意义、个性化的全渠道消息。

此集成将Adobe配置文件数据作为[属性](https://docs.airship.com/guides/audience/attributes/)传递到[!DNL Airship]，以进行定位或触发。

若要了解有关[!DNL Airship]的更多信息，请参阅[飞艇文档](https://docs.airship.com)。

>[!TIP]
>
>此目标连接器和文档页面由[!DNL Airship]团队创建和维护。 如有任何查询或更新请求，请直接通过[support.airship.com](https://support.airship.com/)联系他们。

## 先决条件 {#prerequisites}

在将受众发送到[!DNL Airship]之前，您必须：

* 在[!DNL Airship]项目中启用属性。
* 生成持有者令牌以进行身份验证。

>[!TIP]
>
>通过[此注册链接](https://go.airship.eu/accounts/register/plan/starter/)创建一个[!DNL Airship]帐户（如果尚未创建）。

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
---------|----------|---------|
| 导出类型 | **[!UICONTROL 基于配置文件]** | 您正在导出区段的所有成员，以及所需的架构字段（例如：电子邮件地址、电话号码、姓氏）和/或身份（根据字段映射）。 |
| 导出频率 | **[!UICONTROL 正在流式传输]** | 流目标为基于API的“始终运行”连接。 根据受众评估在Experience Platform中更新用户档案后，连接器会立即将更新发送到下游目标平台。 阅读有关[流式目标](/help/destinations/destination-types.md#streaming-destinations)的更多信息。 |

{style="table-layout:auto"}

## 启用属性 {#enable-attributes}

Adobe Experience Platform配置文件属性与[!DNL Airship]属性类似，可以使用本页下面进一步演示的映射工具在Experience Platform中轻松相互映射。

[!DNL Airship]项目具有几个预定义属性和默认属性。 如果您有自定义属性，则必须先在[!DNL Airship]中定义它。 有关详细信息，请参阅[设置和管理属性](https://docs.airship.com/tutorials/audience/attributes/)。

## 生成持有者令牌 {#bearer-token}

转到[飞艇仪表板](https://go.airship.com)中的&#x200B;**[!UICONTROL 设置]** &quot; **[!UICONTROL API和集成]**，然后在左侧菜单中选择&#x200B;**[!UICONTROL 令牌]**。

单击&#x200B;**[!UICONTROL 创建令牌]**。

为您的令牌提供一个用户友好的名称，例如“Adobe属性目标”，然后为角色选择“所有访问权限”。

单击&#x200B;**[!UICONTROL 创建令牌]**&#x200B;并将详细信息保存为机密。

## 用例 {#use-cases}

为了帮助您更好地了解您应如何以及何时使用[!DNL Airship Attributes]目标，以下是Adobe Experience Platform客户可以使用此目标解决的示例用例。

### 用例#1

利用Adobe Experience Platform中收集的配置文件数据，在[!DNL Airship]的任意渠道中个性化邮件和丰富内容。 例如，利用[!DNL Experience Platform]配置文件数据设置[!DNL Airship]中的位置属性。 这样一来，酒店品牌就能为每位用户显示最近酒店位置的图像。

### 用例#2

利用Adobe Experience Platform中的属性进一步扩充[!DNL Airship]配置文件，并将其与SDK或[!DNL Airship]预测数据相结合。 例如，retailer可以创建具有忠诚度状态和位置数据(来自Experience Platform的属性)的受众，并且[!DNL Airship]预计会流失数据，以将极具针对性的消息发送给居住在内华达州拉斯维加斯且具有高流失率的金会员状态用户。

## 连接到目标 {#connect}

>[!IMPORTANT]
> 
>若要连接到目标，您需要&#x200B;**[!UICONTROL 查看目标]**&#x200B;和&#x200B;**[!UICONTROL 管理目标]** [访问控制权限](/help/access-control/home.md#permissions)。 阅读[访问控制概述](/help/access-control/ui/overview.md)或联系您的产品管理员以获取所需的权限。

要连接到此目标，请按照[目标配置教程](../../ui/connect-destination.md)中描述的步骤操作。 在配置目标工作流中，填写下面两个部分中列出的字段。

### 验证目标 {#authenticate}

要验证到目标，请填写必填字段并选择&#x200B;**[!UICONTROL 连接到目标]**。

* **[!UICONTROL 持有者令牌]**：从[!DNL Airship]仪表板生成的持有者令牌。

### 填写目标详细信息 {#destination-details}

要配置目标的详细信息，请填写下面的必需和可选字段。 UI中字段旁边的星号表示该字段为必填字段。

* **[!UICONTROL 名称]**：输入有助于识别此目标的名称。
* **[!UICONTROL 描述]**：输入此目标的描述。
* **[!UICONTROL 域]**：选择美国或欧盟数据中心，具体取决于哪个[!DNL Airship]数据中心适用于此目标。

### 启用警报 {#enable-alerts}

您可以启用警报，以接收有关发送到目标的数据流状态的通知。 从列表中选择警报以订阅接收有关数据流状态的通知。 有关警报的详细信息，请参阅[使用UI订阅目标警报的指南](../../ui/alerts.md)。

完成提供目标连接的详细信息后，选择&#x200B;**[!UICONTROL 下一步]**。

## 激活此目标的受众 {#activate}

>[!IMPORTANT]
> 
>* 若要激活数据，您需要&#x200B;**[!UICONTROL 查看目标]**、**[!UICONTROL 激活目标]**、**[!UICONTROL 查看配置文件]**&#x200B;和&#x200B;**[!UICONTROL 查看区段]** [访问控制权限](/help/access-control/home.md#permissions)。 阅读[访问控制概述](/help/access-control/ui/overview.md)或联系您的产品管理员以获取所需的权限。
>* 要导出&#x200B;*标识*，您需要&#x200B;**[!UICONTROL 查看标识图形]** [访问控制权限](/help/access-control/home.md#permissions)。<br> ![选择工作流中突出显示的身份命名空间以将受众激活到目标。](/help/destinations/assets/overview/export-identities-to-destination.png "选择工作流中突出显示的身份命名空间以将受众激活到目标。"){width="100" zoomable="yes"}

有关将受众激活到此目标的说明，请参阅[将受众数据激活到流式受众导出目标](../../ui/activate-segment-streaming-destinations.md)。

## 映射注意事项 {#mapping-considerations}

[!DNL Airship]属性可以在渠道上设置，该渠道表示设备实例，如iPhone，也可以设置命名用户，该渠道可将用户的所有设备映射到通用标识符，如客户ID。 如果您的架构中将纯文本（未散列）电子邮件地址作为主标识，请选择&#x200B;**[!UICONTROL Source属性]**&#x200B;中的电子邮件字段，并映射到&#x200B;**[!UICONTROL Target标识]**&#x200B;下右列中的[!DNL Airship]指定用户，如下所示。

![命名用户映射](../../assets/catalog/mobile-engagement/airship/mapping.png)

对于应映射到通道（即设备）的标识符，请根据源映射到相应的通道。 下图显示了如何创建两个映射：

* 将IDFA iOS Advertising ID用于[!DNL Airship] iOS渠道
* Adobe `fullName`属性到[!DNL Airship]“全名”属性

>[!NOTE]
>
>为属性映射选择目标字段时，请使用显示在[!DNL Airship]仪表板中的用户友好名称。

**映射身份**

选择源字段：

![连接到飞艇属性](../../assets/catalog/mobile-engagement/airship/select-source-identity.png)

选择目标字段：

![连接到飞艇属性](../../assets/catalog/mobile-engagement/airship/select-target-identity.png)

**映射属性**

选择源属性：

![选择源字段](../../assets/catalog/mobile-engagement/airship/select-source-attributes.png)

选择目标属性：

![选择目标字段](../../assets/catalog/mobile-engagement/airship/select-target-attribute.png)

验证映射：

![渠道映射](../../assets/catalog/mobile-engagement/airship/mapping.png)


## 数据使用和治理 {#data-usage-governance}

在处理您的数据时，所有[!DNL Adobe Experience Platform]目标都符合数据使用策略。 有关[!DNL Adobe Experience Platform]如何实施数据治理的详细信息，请参阅[数据治理概述](../../../data-governance/home.md)。
