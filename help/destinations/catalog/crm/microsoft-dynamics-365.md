---
keywords: crm；CRM；CRM目标；Microsoft Dynamics 365；Microsoft Dynamics 365 crm目标
title: Microsoft Dynamics 365连接
description: Microsoft Dynamics 365目标允许您导出帐户数据，并在Microsoft Dynamics 365中激活该数据，以满足您的业务需求。
last-substantial-update: 2022-11-08T00:00:00Z
exl-id: 49bb5c95-f4b7-42e1-9aae-45143bbb1d73
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '2154'
ht-degree: 1%

---

# [!DNL Microsoft Dynamics 365] 连接

## 概述 {#overview}

[[!DNL Microsoft Dynamics 365]](https://dynamics.microsoft.com/en-us/) 是一个基于云的业务应用程序平台，它将企业资源规划(ERP)、客户关系管理(CRM)与生产效率应用程序和AI工具相结合，以实现端到端更顺畅、更可控的运营、更好的增长潜力和更低的成本。

此 [!DNL Adobe Experience Platform] [目标](/help/destinations/home.md) 利用 [[!DNL Contact Entity Reference API]](https://docs.microsoft.com/en-us/dynamics365/customerengagement/on-premises/developer/entities/contact?view=op-9-1)，可让您将受众中的身份更新为 [!DNL Dynamics 365].

[!DNL Dynamics 365] 使用具有授权授予的OAuth 2作为身份验证机制以与 [!DNL Contact Entity Reference API]. 向您的验证的说明 [!DNL Dynamics 365] 实例位于 [向目标进行身份验证](#authenticate) 部分。

## 用例 {#use-cases}

作为营销人员，您可以根据用户的Adobe Experience Platform配置文件中的属性，为其提供个性化体验。 您可以从离线数据构建受众并将这些受众发送到 [!DNL Dynamics 365]，以便在Adobe Experience Platform中更新受众和配置文件后立即显示在用户的信息源中。

## 先决条件 {#prerequisites}

### Experience Platform先决条件 {#prerequisites-in-experience-platform}

将数据激活到之前 [!DNL Dynamics 365] 目标，您必须拥有 [架构](/help/xdm/schema/composition.md)， a [数据集](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html)、和 [受众](https://experienceleague.adobe.com/docs/platform-learn/tutorials/audiences/create-audiences.html) 创建于 [!DNL Experience Platform].

请参阅Adobe的文档，了解 [受众成员资格详细信息架构字段组](/help/xdm/field-groups/profile/segmentation.md) 如果您需要有关受众状态的指南。

### [!DNL Microsoft Dynamics 365] 先决条件 {#prerequisites-destination}

请注意中的以下先决条件 [!DNL Dynamics 365]，以便将数据从Platform导出到 [!DNL Dynamics 365] 帐户：

#### 您需要拥有 [!DNL Microsoft Dynamics 365] 帐户 {#prerequisites-account}

转到 [!DNL Dynamics 365] [试用版](https://dynamics.microsoft.com/en-us/dynamics-365-free-trial/) 页面注册并创建帐户（如果尚未注册）。

#### 在中创建字段 [!DNL Dynamics 365] {#prerequisites-custom-field}

创建类型的自定义字段 `Simple` 字段数据类型为 `Single Line of Text` 使用哪个Experience Platform来更新中的受众状态 [!DNL Dynamics 365].

请参阅 [!DNL Dynamics 365] [创建或编辑字段（属性）](https://docs.microsoft.com/en-us/dynamics365/customerengagement/on-premises/customize/create-edit-fields?view=op-9-1) 文档（如果您需要其他指导）。

记下 **[!UICONTROL 自定义前缀]** 中创建的自定义字段的 [!DNL Dynamics 365]. 在以下时段中，您将需要此前缀： [填写目标详细信息](#destination-details) 步骤。 请参阅 [创建和编辑字段](https://learn.microsoft.com/en-us/dynamics365/customerengagement/on-premises/customize/create-edit-fields?view=op-9-1#create-and-edit-fields) 的部分 [!DNL Dynamics 365] 文档，以了解更多详细信息。
![显示自定义前缀的Dynamics 365 UI屏幕截图。](../../assets/catalog/crm/microsoft-dynamics-365/dynamics-365-customization-prefix.png)

中的设置示例 [!DNL Dynamics 365] 如下所示：
![显示自定义字段的Dynamics 365 UI屏幕截图。](../../assets/catalog/crm/microsoft-dynamics-365/dynamics-365-fields.png)

#### 在Azure Active Directory中注册应用程序和应用程序用户 {#prerequisites-app-user}

要启用 [!DNL Dynamics 365] 要访问资源，您需要使用 [!DNL Azure Account] 到 [[!DNL Azure Active Directory]](https://docs.microsoft.com/en-us/azure/active-directory/develop/howto-create-service-principal-portal#register-an-application-with-azure-ad-and-create-a-service-principal) 并创建以下内容：
* An [!DNL Azure Active Directory] 应用程序
* 服务主体
* 应用程序密码

您还需要 [创建应用程序用户](https://docs.microsoft.com/en-us/power-platform/admin/manage-application-users#create-an-application-user) 在 [!DNL Azure Active Directory] 并将其与新创建的应用程序关联。

#### 收集 [!DNL Dynamics 365] 凭据 {#gather-credentials}

在对进行身份验证之前，请记下以下各项 [!DNL Dynamics 365] CRM目标：

| 凭据 | 描述 | 示例 |
| --- | --- | --- |
| `Client ID` | 此 [!DNL Dynamics 365] 您的客户端ID [!DNL Azure Active Directory] 应用程序。 请参阅 [[!DNL Dynamics 365] 文档](https://docs.microsoft.com/en-us/azure/active-directory/develop/howto-create-service-principal-portal#get-tenant-and-app-id-values-for-signing-in) 作为指导。 | `ababbaba-abab-baba-acac-acacacacacac` |
| `Client Secret` | 此 [!DNL Dynamics 365] 您的客户端密钥 [!DNL Azure Active Directory] 应用程序。 您应使用#2 [[!DNL Dynamics 365] 文档](https://docs.microsoft.com/en-us/azure/active-directory/develop/howto-create-service-principal-portal#authentication-two-options). | `abcde~abcdefghijklmnopqrstuvwxyz12345678` 作为指导。 |
| `Tenant ID` | 此 [!DNL Dynamics 365] 您的租户ID [!DNL Azure Active Directory] 应用程序。 请参阅 [[!DNL Dynamics 365] 文档](https://docs.microsoft.com/en-us/azure/active-directory/develop/howto-create-service-principal-portal#get-tenant-and-app-id-values-for-signing-in) 作为指导。 | `1234567-aaaa-12ab-ba21-1234567890` |
| `Region` | 与环境URL关联的Microsoft区域。<br> 请参阅 [[!DNL Dynamics 365] 文档](https://learn.microsoft.com/en-us/power-platform/admin/new-datacenter-regions) 作为指导。 | 如果您的域如下所示，在对进行身份验证时，您需要在下拉选择器中为CRM字段提供突出显示的值 [目标](#authenticate).<br> *org57771b33。`crm`.dynamics.com*<br>  例如：如果您的公司是在北美(NAM)地区配置的，则您的URL将是 `crm.dynamics.com` 您需要选择 `crm`. 如果您的公司位于加拿大(CAN)地区，则您的URL应为 `crm3.dynamics.com` 您需要选择 `crm3`. |
| `Environment URL` | 请参阅 [[!DNL Dynamics 365] 文档](https://docs.microsoft.com/en-us/dynamics365/customerengagement/on-premises/developer/org-service/discover-url-organization-organization-service?view=op-9-1) 作为指导。 | 如果您的 [!DNL Dynamics 365] 域如下所示，您需要高亮显示的值。<br> *`org57771b33`.crm.dynamics.com* |

{style="table-layout:auto"}

## 护栏 {#guardrails}

此 [请求限制和分配](https://docs.microsoft.com/en-us/power-platform/admin/api-request-limits-allocations) 页面详细信息 [!DNL Dynamics 365] 与您的 [!DNL Dynamics 365] 许可证。 您需要确保数据和有效负载均在这些限制之内。

## 支持的身份 {#supported-identities}

[!DNL Dynamics 365] 支持更新下表中描述的标识。 了解有关 [身份](/help/identity-service/namespaces.md).

| 目标身份 | 示例 | 描述 | 注意事项 |
|---|---|---|---|
| `contactId` | 7eb682f1-ca75-e511-80d4-00155d2a68d1 | 联系人的唯一标识符。 | **必需**. 请参阅 [[!DNL Dynamics 365] 文档](https://docs.microsoft.com/en-us/dynamics365/customerengagement/on-premises/developer/entities/contact?view=op-9-1) 以了解更多详细信息。 |

{style="table-layout:auto"}

## 支持的受众 {#supported-audiences}

此部分介绍可导出到此目标的所有受众。

此目标支持激活通过Experience Platform生成的所有受众 [分段服务](../../../segmentation/home.md).

## 导出类型和频率 {#export-type-frequency}

有关目标导出类型和频率的信息，请参阅下表。

| 项目 | 类型 | 注释 |
---------|----------|---------|
| 导出类型 | **[!UICONTROL 基于配置文件]** | <ul><li>您正在导出受众的所有成员以及所需的架构字段 *（例如：电子邮件地址、电话号码、姓氏）*，根据您的字段映射。</li><li> 中的每个受众状态 [!DNL Dynamics 365] 将根据 **[!UICONTROL 映射Id]** 值在 [受众调度](#schedule-audience-export-example) 步骤。</li></ul> |
| 导出频率 | **[!UICONTROL 流]** | <ul><li>流目标为基于API的“始终运行”连接。 一旦根据受众评估在Experience Platform中更新了用户档案，连接器就会将更新发送到下游目标平台。 详细了解 [流目标](/help/destinations/destination-types.md#streaming-destinations).</li></ul> |

{style="table-layout:auto"}

## 连接到目标 {#connect}

>[!IMPORTANT]
>
>要连接到目标，您需要 **[!UICONTROL 管理目标]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或与产品管理员联系以获取所需的权限。

要连接到此目标，请按照 [目标配置教程](../../ui/connect-destination.md). 在配置目标工作流中，填写下面两个部分中列出的字段。

范围 **[!UICONTROL 目标]** > **[!UICONTROL 目录]** 搜索 [!DNL Dynamics 365]. 或者，您可以将其定位到 **[!UICONTROL CRM]** 类别。

### 向目标进行身份验证 {#authenticate}

要验证目标，请选择 **[!UICONTROL 连接到目标]**.
![显示如何进行身份验证的平台UI屏幕截图。](../../assets/catalog/crm/microsoft-dynamics-365/authenticate-destination.png)

填写下面的必填字段。 请参阅 [收集Dynamics 365凭据](#gather-credentials) 部分获取任何指导。
* **[!UICONTROL 客户端ID]**：和 [!DNL Dynamics 365] 您的客户端ID [!DNL Azure Active Directory] 应用程序。
* **[!UICONTROL 租户ID]**：和 [!DNL Dynamics 365] 您的租户ID [!DNL Azure Active Directory] 应用程序。
* **[!UICONTROL 客户端密码]**：和 [!DNL Dynamics 365] 您的客户端密钥 [!DNL Azure Active Directory] 应用程序。
* **[!UICONTROL 区域]**：您的 [[!DNL Dynamics 365]](https://learn.microsoft.com/en-us/power-platform/admin/new-datacenter-regions) 区域。 例如：如果您的公司是在北美(NAM)地区配置的，则您的URL将是 `crm.dynamics.com` 您需要选择 `crm`. 如果您的公司位于加拿大(CAN)地区，则您的URL应为 `crm3.dynamics.com` 您需要选择 `crm3`.
* **[!UICONTROL 环境URL]**：您的 [!DNL Dynamics 365] 环境URL。

如果提供的详细信息有效，UI将显示 **[!UICONTROL 已连接]** 带有绿色复选标记的状态。 然后，您可以继续执行下一步。

### 填写目标详细信息 {#destination-details}

要配置目标的详细信息，请填写下面的必需和可选字段。 UI中字段旁边的星号表示该字段为必填字段。
![显示目标详细信息的平台UI屏幕截图。](../../assets/catalog/crm/microsoft-dynamics-365/destination-details.png)

* **[!UICONTROL 名称]**：将来用于识别此目标的名称。
* **[!UICONTROL 描述]**：可帮助您将来识别此目标的描述。
* **[!UICONTROL 自定义前缀]**：和 `Customization prefix` 您在中创建的自定义字段的 [!DNL Dynamics 365]. 请参阅 [创建和编辑字段](https://learn.microsoft.com/en-us/dynamics365/customerengagement/on-premises/customize/create-edit-fields?view=op-9-1#create-and-edit-fields) 的部分 [!DNL Dynamics 365] 文档，以了解更多详细信息。

### 启用警报 {#enable-alerts}

您可以启用警报，以接收有关发送到目标的数据流状态的通知。 从列表中选择警报以订阅接收有关数据流状态的通知。 有关警报的详细信息，请参阅以下内容中的指南： [使用UI订阅目标警报](../../ui/alerts.md).

完成提供目标连接的详细信息后，选择 **[!UICONTROL 下一个]**.

## 将受众激活到此目标 {#activate}

>[!IMPORTANT]
> 
>* 要激活数据，您需要 **[!UICONTROL 管理目标]**， **[!UICONTROL 激活目标]**， **[!UICONTROL 查看配置文件]**、和 **[!UICONTROL 查看区段]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或与产品管理员联系以获取所需的权限。
>* 要导出 *身份*，您需要 **[!UICONTROL 查看身份图]** [访问控制权限](/help/access-control/home.md#permissions). <br> ![选择工作流中突出显示的身份命名空间以将受众激活到目标。](/help/destinations/assets/overview/export-identities-to-destination.png "选择工作流中突出显示的身份命名空间以将受众激活到目标。"){width="100" zoomable="yes"}

读取 [将用户档案和受众激活到流式受众导出目标](/help/destinations/ui/activate-segment-streaming-destinations.md) 有关将受众激活到此目标的说明。

### 映射注意事项和示例 {#mapping-considerations-example}

要正确地将受众数据从Adobe Experience Platform发送到 [!DNL Dynamics 365] 目标，您需要执行字段映射步骤。 映射包括在您的Platform帐户中的Experience Data Model (XDM)架构字段与其在目标目标中的相应等效字段之间创建链接。 要将XDM字段正确映射到 [!DNL Dynamics 365] 目标字段，请执行以下步骤：

1. 在 **[!UICONTROL 映射]** 步骤，选择 **[!UICONTROL 添加新映射]**. 您将在屏幕上看到一个新映射行。
   ![用于添加新映射的平台UI屏幕快照示例。](../../assets/catalog/crm/microsoft-dynamics-365/add-new-mapping.png)

1. 在 **[!UICONTROL 选择源字段]** 窗口中，选择 **[!UICONTROL 选择身份命名空间]** 类别并选择 `contactId`.
   ![源映射的平台UI屏幕截图示例。](../../assets/catalog/crm/microsoft-dynamics-365/source-mapping.png)

1. 在 **[!UICONTROL 选择目标字段]** 窗口中，选择要将源字段映射到的目标字段类型。
   * **[!UICONTROL 选择身份命名空间]**：选择此选项可从列表中将源字段映射到身份命名空间。
     ![平台UI屏幕截图显示了contactId的Target映射。](../../assets/catalog/crm/microsoft-dynamics-365/target-mapping-contactid.png)

   * 在XDM配置文件架构与您的配置文件架构之间添加以下映射 [!DNL Dynamics 365] 实例： |XDM配置文件架构|[!DNL Dynamics 365] 实例|必需| |—|—|—| |`contactId`|`contactId`|是 |

   * **[!UICONTROL 选择自定义属性]**：选择此选项可将源字段映射到您在中定义的自定义属性 **[!UICONTROL 属性名称]** 字段。 请参阅 [[!DNL Dynamics 365] 文档](https://docs.microsoft.com/en-us/dynamics365/customerengagement/on-premises/developer/entities/contact?view=op-9-1#entity-properties) 以获取支持的属性的完整列表。
     ![显示LastName的Target映射的平台UI屏幕截图。](../../assets/catalog/crm/microsoft-dynamics-365/target-mapping-lastname.png)

     >[!IMPORTANT]
     >
     >如果您有一个日期或时间戳源字段被映射到 [!DNL Dynamics 365] [日期或时间戳](https://docs.microsoft.com/en-us/power-apps/developer/data-platform/webapi/reference/timestampdatemapping?view=dataverse-latest) 目标字段，请确保映射的值不为空。 如果传递的值为空，您将遇到 *`Bad request reported while pushing events to the destination. Please contact the administrator and try again.`* 错误消息和数据将不更新。 这是 [!DNL Dynamics 365] 限制。

   * 例如，根据要更新的值，在XDM配置文件架构和之间添加以下映射 [!DNL Dynamics 365] 实例： |XDM配置文件架构|[!DNL Dynamics 365] 实例| |—|—| |`person.name.firstName`|`FirstName`| |`person.name.lastName`|`LastName`| |`personalEmail.address`|`Email`|

   * 下面显示了使用这些映射的示例：
     ![显示Target映射的平台UI屏幕截图示例。](../../assets/catalog/crm/microsoft-dynamics-365/mappings.png)

### 计划受众导出和示例 {#schedule-audience-export-example}

在 [[!UICONTROL 计划受众导出]](/help/destinations/ui/activate-segment-streaming-destinations.md#scheduling) 在激活工作流的步骤中，您必须手动将Platform受众映射到中的自定义字段属性 [!DNL Dynamics 365].

为此，请选择每个受众，然后从中输入相应的自定义字段属性 [!DNL Dynamics 365] 在 **[!UICONTROL 映射Id]** 字段。

>[!IMPORTANT]
>
>用于 **[!UICONTROL 映射Id]** 应与在中创建的自定义字段属性的名称完全匹配 [!DNL Dynamics 365]. 请参阅 [[!DNL Dynamics 365] 文档](https://docs.microsoft.com/en-us/dynamics365/customerengagement/on-premises/customize/create-edit-fields?view=op-9-1) 如果您需要有关查找自定义字段属性的指南。

下面显示了一个示例：
![显示计划受众导出的平台UI屏幕截图示例。](../../assets/catalog/crm/microsoft-dynamics-365/schedule-segment-export.png)

## 验证数据导出 {#exported-data}

要验证您是否正确设置了目标，请执行以下步骤：

1. 选择 **[!UICONTROL 目标]** > **[!UICONTROL 浏览]** 导航到目标列表。
   ![显示浏览目标的平台UI屏幕截图。](../../assets/catalog/crm/microsoft-dynamics-365/browse-destinations.png)

1. 选择目标并验证状态为 **[!UICONTROL 已启用]**.
   ![显示目标数据流运行的平台UI屏幕快照。](../../assets/catalog/crm/microsoft-dynamics-365/destination-dataflow-run.png)

1. 切换到 **[!DNL Activation data]** 选项卡，然后选择受众名称。
   ![显示目标激活数据的平台UI屏幕截图示例。](../../assets/catalog/crm/microsoft-dynamics-365/destinations-activation-data.png)

1. 监控受众摘要，并确保用户档案计数对应于在受众中创建的计数。
   ![显示受众的平台UI屏幕截图示例。](../../assets/catalog/crm/microsoft-dynamics-365/segment.png)

1. 登录到 [!DNL Dynamics 365] 网站，然后导航到 [!DNL Customers] > [!DNL Contacts] 页面，并检查是否已添加受众中的配置文件。 您可以在中看到每个受众状态 [!DNL Dynamics 365] 已根据，从Platform更新了相应的受众状态 **[!UICONTROL 映射Id]** 值在 [受众调度](#schedule-audience-export-example) 步骤。
   ![显示“联系人”页面且受众状态已更新的Dynamics 365 UI屏幕截图。](../../assets/catalog/crm/microsoft-dynamics-365/contacts.png)

## 数据使用和治理 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 目标在处理您的数据时符合数据使用策略。 有关如何执行操作的详细信息 [!DNL Adobe Experience Platform] 强制执行数据管理，请参见 [数据管理概述](/help/data-governance/home.md).

## 错误和故障排除 {#errors-and-troubleshooting}

### 将事件推送到目标时报告了未知错误 {#unknown-errors}

检查数据流运行时，如果收到以下错误消息： `Bad request reported while pushing events to the destination. Please contact the administrator and try again.`

![平台UI屏幕截图显示错误请求错误。](../../assets/catalog/crm/microsoft-dynamics-365/error.png)

要修复此错误，请验证 **[!UICONTROL 映射Id]** 您提供于 [!DNL Dynamics 365] 的有效受众，并且存在于中 [!DNL Dynamics 365].

## 其他资源 {#additional-resources}

其他有用信息来自 [[!DNL Dynamics 365] 文档](https://docs.microsoft.com/en-us/dynamics365/) 如下所示：
* [IOrorganizationService.Update(Entity)方法](https://docs.microsoft.com/en-us/dotnet/api/microsoft.xrm.sdk.iorganizationservice.update?view=dataverse-sdk-latest)
* [使用Web API更新和删除表行](https://docs.microsoft.com/en-us/power-apps/developer/data-platform/webapi/update-delete-entities-using-web-api#basic-update)

### Changelog

此部分捕获此目标连接器的功能和重要文档更新。

+++ 查看更改日志

| 发行月份 | 更新类型 | 描述 |
|---|---|---|
| 2023 年 8 月 | 功能和文档更新 | 添加了对的支持 [!DNL Dynamics 365] 未在的默认解决方案中创建的自定义字段的自定义字段前缀 [!DNL Dynamics 365]. 新的输入字段， **[!UICONTROL 自定义前缀]**，已添加在 [填写目标详细信息](#destination-details) 步骤。 (PLATIR-31602)。 |
| 2022年11月 | 初始版本 | 初始目标版本和文档发布。 |

{style="table-layout:auto"}

+++