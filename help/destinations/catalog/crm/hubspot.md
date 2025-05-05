---
title: HubSpot连接
description: HubSpot目标允许您管理HubSpot帐户中的联系人记录。
last-substantial-update: 2023-09-28T00:00:00Z
exl-id: e2114bde-b7c3-43da-9f3a-919322000ef4
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1557'
ht-degree: 3%

---

# [!DNL HubSpot]连接

[[!DNL HubSpot]](https://www.hubspot.com)是一个CRM平台，其中包含连接营销、销售、内容管理和客户服务所需的所有软件、集成和资源。 它允许您在一个CRM平台上连接数据、团队和客户。

此[!DNL Adobe Experience Platform] [目标](/help/destinations/home.md)利用[[!DNL HubSpot] 联系人API](https://developers.hubspot.com/docs/api/crm/contacts)，在激活后从现有Experience Platform受众更新[!DNL HubSpot]中的联系人。

下面的[向目标身份验证](#authenticate)部分中进一步提供了向您的[!DNL HubSpot]实例进行身份验证的说明。

## 用例 {#use-cases}

为了帮助您更好地了解您应如何以及何时使用[!DNL HubSpot]目标，以下是Adobe Experience Platform客户可以使用此目标解决的示例用例。

[!DNL HubSpot]联系人存储与您的业务交互的个人的相关信息。 您的团队使用[!DNL HubSpot]中存在的联系人来构建Experience Platform受众。 将这些受众发送至[!DNL HubSpot]后，其信息会更新，并且会为每个联系人分配一个属性，其值作为受众名称，指示该联系人属于哪个受众。

## 先决条件 {#prerequisites}

请参阅以下部分，了解需要在Experience Platform和[!DNL HubSpot]中设置的任何先决条件，以及在使用[!DNL HubSpot]目标之前必须收集的信息。

### Experience Platform先决条件 {#prerequisites-in-experience-platform}

在将数据激活到[!DNL HubSpot]目标之前，您必须在[!DNL Experience Platform]中创建一个[架构](/help/xdm/schema/composition.md)、[数据集](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html)和[受众](https://experienceleague.adobe.com/docs/platform-learn/tutorials/audiences/create-audiences.html)。

如果您需要有关受众状态的指导，请参阅Experience Platform文档，了解[受众成员资格详细信息架构字段组](/help/xdm/field-groups/profile/segmentation.md)。

### [!DNL HubSpot]目标的先决条件 {#prerequisites-destination}

请注意以下先决条件，以便将数据从Experience Platform导出到您的[!DNL HubSpot]帐户：

#### 您必须拥有[!DNL HubSpot]帐户 {#prerequisites-account}

要将数据从Experience Platform导出到您的[!DNL Hubspot]帐户，您需要拥有[!DNL HubSpot]帐户。 如果您还没有帐户，请访问[设置HubSpot帐户](https://knowledge.hubspot.com/get-started/set-up-your-account)页面，然后按照指南注册和创建帐户。

#### 收集[!DNL HubSpot]私有应用程序访问令牌 {#gather-credentials}

您需要您的[!DNL HubSpot] `Access token`允许[!DNL HubSpot]目标通过您[!DNL HubSpot]帐户中的[!DNL HubSpot]私人应用进行API调用。 当您[对目标](#authenticate)进行身份验证时，`Access token`将用作`Bearer token`。

如果您没有专用应用，请按照文档中的说明[在 [!DNL HubSpot]](https://developers.hubspot.com/docs/api/private-apps)中创建专用应用。

>[!IMPORTANT]
>
> 应为专用应用程序分配以下范围：
> `crm.objects.contacts.write`，`crm.objects.contacts.read`
> `crm.schemas.contacts.write`，`crm.schemas.contacts.read`

| 凭据 | 描述 | 示例 |
| --- | --- | --- |
| `Bearer token` | [!DNL HubSpot]私有应用的`Access token`。 <br>要获取您的[!DNL HubSpot] `Access token`，请按照[!DNL HubSpot]文档中的说明，使用您应用程序的访问令牌[&#128279;](https://developers.hubspot.com/docs/api/private-apps#make-api-calls-with-your-app-s-access-token)进行API调用。 | `pat-na1-11223344-abcde-12345-9876-1234a1b23456` |

## 护栏 {#guardrails}

[!DNL HubSpot]私有应用受[速率限制](https://developers.hubspot.com/docs/api/usage-details)的约束。 您的私人应用可拨打的次数取决于您的[!DNL HubSpot]帐户订阅以及您是否购买了API加载项。 另请参阅[其他限制](https://developers.hubspot.com/docs/api/usage-details#other-limits)。

## 支持的身份 {#supported-identities}

[!DNL HubSpot]支持更新下表中描述的标识。 了解有关[标识](/help/identity-service/features/namespaces.md)的更多信息。

| 目标身份 | 示例 | 描述 | 注意事项 |
|---|---|---|---|
| `email` | `test@test.com` | 联系人的电子邮件地址。 | 必需 |

## 支持的受众 {#supported-audiences}

此部分介绍可导出到此目标的所有受众。

此目标支持激活通过Experience Platform [分段服务](../../../segmentation/home.md)生成的所有受众。

此目标还支持激活下表所述的受众。

| 受众类型 | 描述 |
|---------|----------|
| 自定义上传 | 受众[已从CSV文件将](../../../segmentation/ui/audience-portal.md#import-audience)导入Experience Platform。 |

{style="table-layout:auto"}

## 导出类型和频率 {#export-type-frequency}

有关目标导出类型和频率的信息，请参阅下表。

| 项目 | 类型 | 注释 |
---------|----------|---------|
| 导出类型 | **[!UICONTROL 基于配置文件]** | <ul><li>您正在导出受众的所有成员，以及所需的架构字段&#x200B;*（例如：电子邮件地址、电话号码、姓氏）*（根据字段映射）。</li><li> 此外，在[!DNL HubSpot]中使用受众名称创建一个新属性，对于每个所选受众，其值与Experience Platform中的相应受众状态相同。</li></ul> |
| 导出频率 | **[!UICONTROL 正在流式传输]** | <ul><li>流目标为基于API的“始终运行”连接。 根据受众评估在Experience Platform中更新用户档案后，连接器会立即将更新发送到下游目标平台。 阅读有关[流式目标](/help/destinations/destination-types.md#streaming-destinations)的更多信息。</li></ul> |

{style="table-layout:auto"}

## 连接到目标 {#connect}

>[!IMPORTANT]
>
>若要连接到目标，您需要&#x200B;**[!UICONTROL 查看目标]**&#x200B;和&#x200B;**[!UICONTROL 管理目标]** [访问控制权限](/help/access-control/home.md#permissions)。 阅读[访问控制概述](/help/access-control/ui/overview.md)或联系您的产品管理员以获取所需的权限。

要连接到此目标，请按照[目标配置教程](../../ui/connect-destination.md)中描述的步骤操作。 在配置目标工作流中，填写下面两个部分中列出的字段。

在&#x200B;**[!UICONTROL 目标]** > **[!UICONTROL 目录]**&#x200B;中，搜索[!DNL HubSpot]。 或者，您可以在&#x200B;**[!UICONTROL CRM]**&#x200B;类别下找到它。

### 验证目标 {#authenticate}

填写下面的必填字段。 有关任何指导，请参阅[收集 [!DNL HubSpot] 私有应用程序访问令牌](#gather-credentials)部分。
* **[!UICONTROL 持有者令牌]**： [!DNL HubSpot]私有应用程序的访问令牌。

要验证到目标，请选择&#x200B;**[!UICONTROL 连接到目标]**。
![Experience Platform UI屏幕截图显示如何进行身份验证。](../../assets/catalog/crm/hubspot/authenticate-destination.png)

如果提供的详细信息有效，则UI会显示&#x200B;**[!UICONTROL 已连接]**&#x200B;状态，并带有绿色复选标记。 然后，您可以继续执行下一步。

### 填写目标详细信息 {#destination-details}

要配置目标的详细信息，请填写下面的必需和可选字段。 UI中字段旁边的星号表示该字段为必填字段。
![Experience Platform UI屏幕截图显示目标详细信息。](../../assets/catalog/crm/hubspot/destination-details.png)

* **[!UICONTROL 名称]**：将来用于识别此目标的名称。
* **[!UICONTROL 描述]**：可帮助您将来识别此目标的描述。

### 启用警报 {#enable-alerts}

您可以启用警报，以接收有关发送到目标的数据流状态的通知。 从列表中选择警报以订阅接收有关数据流状态的通知。 有关警报的详细信息，请参阅[使用UI订阅目标警报的指南](../../ui/alerts.md)。

完成提供目标连接的详细信息后，选择&#x200B;**[!UICONTROL 下一步]**。

## 激活此目标的受众 {#activate}

>[!IMPORTANT]
>
>若要激活数据，您需要&#x200B;**[!UICONTROL 查看目标]**、**[!UICONTROL 激活目标]**、**[!UICONTROL 查看配置文件]**&#x200B;和&#x200B;**[!UICONTROL 查看区段]** [访问控制权限](/help/access-control/home.md#permissions)。 阅读[访问控制概述](/help/access-control/ui/overview.md)或联系您的产品管理员以获取所需的权限。

有关将受众激活到此目标的说明，请阅读[将配置文件和受众激活到流式受众导出目标](/help/destinations/ui/activate-segment-streaming-destinations.md)。

### 映射属性和身份 {#map}

要将受众数据从Adobe Experience Platform正确发送到[!DNL HubSpot]目标，您必须完成字段映射步骤。 映射包括在Experience Platform帐户中的Experience Data Model (XDM)架构字段与其与目标中的相应等效字段之间创建链接。

要将XDM字段正确映射到[!DNL HubSpot]目标字段，请执行以下步骤：

#### 映射`Email`标识

`Email`标识是此目标的必需映射。 请按照以下步骤对其进行映射：
1. 在&#x200B;**[!UICONTROL 映射]**&#x200B;步骤中，选择&#x200B;**[!UICONTROL 添加新映射]**。 您现在可以在屏幕上看到新的映射行。
   ![突出显示了“添加新映射”按钮的Experience Platform UI屏幕截图。](../../assets/catalog/crm/hubspot/mapping-add-new-mapping.png)
1. 在&#x200B;**[!UICONTROL 选择源字段]**&#x200B;窗口中，选择&#x200B;**[!UICONTROL 选择身份命名空间]**&#x200B;并选择身份。
   ![Experience Platform UI屏幕截图选择电子邮件作为要映射为标识的源属性。](../../assets/catalog/crm/hubspot/mapping-select-source-identity.png)
1. 在&#x200B;**[!UICONTROL 选择目标字段]**&#x200B;窗口中，选择&#x200B;**[!UICONTROL 选择属性]**&#x200B;并选择`email`。
   ![Experience Platform UI屏幕截图选择电子邮件作为要映射为身份的目标属性。](../../assets/catalog/crm/hubspot/mapping-select-target-identity.png)

| 源字段 | 目标字段 | 必需 |
| --- | --- | --- |
| `IdentityMap: Email` | `Identity: email` | 是 |

下面显示了具有标识映射的示例：
![具有电子邮件标识映射的Experience Platform UI屏幕快照示例。](../../assets/catalog/crm/hubspot/mapping-identities.png)

#### 映射&#x200B;**可选**&#x200B;属性

要添加任何其他要在XDM配置文件架构和[!DNL HubSpot]帐户之间更新的属性，请重复以下步骤：
1. 在&#x200B;**[!UICONTROL 映射]**&#x200B;步骤中，选择&#x200B;**[!UICONTROL 添加新映射]**。 您现在可以在屏幕上看到新的映射行。
   ![突出显示了“添加新映射”按钮的Experience Platform UI屏幕截图。](../../assets/catalog/crm/hubspot/mapping-add-new-mapping.png)
1. 在&#x200B;**[!UICONTROL 选择源字段]**&#x200B;窗口中，选择&#x200B;**[!UICONTROL 选择属性]**&#x200B;类别并选择XDM属性。
   ![选择“名字”作为源属性的Experience Platform UI屏幕截图。](../../assets/catalog/crm/hubspot/mapping-select-source-attribute.png)
1. 在&#x200B;**[!UICONTROL 选择目标字段]**&#x200B;窗口中，选择&#x200B;**[!UICONTROL 选择属性]**&#x200B;类别，然后从自动从[!DNL HubSpot]帐户填充的属性列表中进行选择。 目标使用[[!DNL HubSpot] 属性](https://developers.hubspot.com/docs/api/crm/properties) API检索此信息。 已检索[!DNL HubSpot] [默认属性](https://knowledge.hubspot.com/contacts/hubspots-default-contact-properties)和任何自定义属性，以便选择它们作为目标字段。
   ![选择“名字”作为Target属性的Experience Platform UI屏幕截图。](../../assets/catalog/crm/hubspot/mapping-select-target-attribute.png)

下面显示了XDM配置文件架构和[!DNL Hubspot]之间的一些可用映射：

| 源字段 | 目标字段 |
| --- | --- |
| `xdm: person.name.firstName` | `Attribute: firstname` |
| `xdm: person.name.lastName` | `Attribute: lastname` |
| `xdm: workAddress.street1` | `Attribute: address` |
| `xdm: workAddress.city` | `Attribute: city` |
| `xdm: workAddress.country` | `Attribute: country` |

以下显示了使用这些属性映射的示例：
![具有属性映射的Experience Platform UI屏幕快照示例。](../../assets/catalog/crm/hubspot/mapping-attributes.png)

完成提供目标连接的映射后，请选择&#x200B;**[!UICONTROL 下一步]**。

## 验证数据导出 {#exported-data}

要验证您是否正确设置了目标，请执行以下步骤：

1. 登录到[!DNL HubSpot]网站，然后导航到&#x200B;**[!UICONTROL 联系人]**&#x200B;页面以检查受众状态。 此列表可以配置为显示使用受众名称创建的自定义属性的列，其值是受众状态。
   ![HubSpot UI屏幕截图显示“联系人”页面，该页面带有列标题，其中显示受众名称和单元格受众状态](../../assets/catalog/crm/hubspot/contacts.png)

1. 或者，您可以向下钻取到单个&#x200B;**[!UICONTROL 人员]**&#x200B;页面，并导航到显示受众名称和受众状态的属性。
   ![HubSpot UI屏幕截图显示“联系人”页面，该页面具有显示受众名称和受众状态的自定义属性。](../../assets/catalog/crm/hubspot/contact.png)

## 数据使用和治理 {#data-usage-governance}

在处理您的数据时，所有[!DNL Adobe Experience Platform]目标都符合数据使用策略。 有关[!DNL Adobe Experience Platform]如何实施数据治理的详细信息，请参阅[数据治理概述](/help/data-governance/home.md)。

## 其他资源 {#additional-resources}

[!DNL HubSpot]文档中的其他有用信息如下：
* HubSpot上的[身份验证方法](https://developers.hubspot.com/docs/api/intro-to-auth)
* [联系人](https://developers.hubspot.com/docs/api/crm/contacts)和[属性](https://developers.hubspot.com/docs/api/crm/properties) API的[!DNL HubSpot] API引用。

### Changelog

此部分捕获此目标连接器的功能和重要文档更新。

+++ 查看更改日志

| 发行月份 | 更新类型 | 描述 |
|---|---|---|
| 2023 年 9 月 | 初始版本 | 初始目标版本和文档发布。 |

{style="table-layout:auto"}

+++
