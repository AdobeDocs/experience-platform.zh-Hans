---
title: (API)OracleEloqua连接
description: 通过(API)OracleEloqua目标，您可以导出帐户数据，并在OracleEloqua中激活该数据，以满足您的业务需求。
last-substantial-update: 2023-03-14T00:00:00Z
exl-id: 97ff41a2-2edd-4608-9557-6b28e74c4480
source-git-commit: c3ef732ee82f6c0d56e89e421da0efc4fbea2c17
workflow-type: tm+mt
source-wordcount: '2042'
ht-degree: 4%

---


# [!DNL (API) Oracle Eloqua] 连接

[[!DNL Oracle Eloqua]](https://www.oracle.com/cx/marketing/automation/) 使营销人员能够规划和执行营销活动，同时为其潜在客户提供个性化的客户体验。 借助集成的商机管理和轻松的营销活动创建，它可帮助营销人员在其购买者的历程中在正确的时间吸引正确的受众，并进行优雅的扩展以跨渠道（包括电子邮件、显示搜索、视频和移动设备）触及受众。 销售团队能够以更快的速度完成更多交易，从而通过实时洞察提高营销投资回报率。

此 [!DNL Adobe Experience Platform] [目标](/help/destinations/home.md) 利用 [更新联系人](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/op-api-rest-1.0-data-contact-id-put.html) 来自的操作 [!DNL Oracle Eloqua] REST API，允许您 **更新身份** 在受众中进入 [!DNL Oracle Eloqua].

[!DNL Oracle Eloqua] 用途 [基本身份验证](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/Authentication_Basic.html) 以与 [!DNL Oracle Eloqua] REST API。 向您的验证的说明 [!DNL Oracle Eloqua] 实例位于 [向目标进行身份验证](#authenticate) 部分。

## 用例 {#use-cases}

在线平台的营销部门希望向策划的潜在客户受众广播基于电子邮件的营销活动。 该平台的营销团队可以通过Adobe Experience Platform更新现有的潜在客户信息，从受众自己的离线数据构建受众，并将这些受众发送至 [!DNL Oracle Eloqua]，然后将其用于发送营销活动电子邮件。

## 先决条件 {#prerequisites}

### Experience Platform先决条件 {#prerequisites-in-experience-platform}

将数据激活到之前 [!DNL Oracle Eloqua] 目标，您必须拥有 [架构](/help/xdm/schema/composition.md)， a [数据集](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html)、和 [区段](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html) 创建于 [!DNL Experience Platform].

请参阅Experience Platform文档，了解 [受众成员资格详细信息架构字段组](/help/xdm/field-groups/profile/segmentation.md) 如果您需要有关受众状态的指南。

### [!DNL Oracle Eloqua] 先决条件 {#prerequisites-destination}

为了将数据从Platform导出到 [!DNL Oracle Eloqua] 您需要拥有 [!DNL Oracle Eloqua] 帐户。

此外，您至少需要 *“高级用户 — 营销权限”* 您的 [!DNL Oracle Eloqua] 实例。 请参阅 *“安全组”* 部分，位于 [安全的用户访问](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-user/Help/SecurityOverview/SecuredUserAccess.htm) 页面获取指导。 目标需要访问才能以编程方式访问 [确定基本URL](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/DeterminingBaseURL.html) 调用时 [!DNL Oracle Eloqua] API。

#### 收集 [!DNL Oracle Eloqua] 凭据 {#gather-credentials}

在对进行身份验证之前，请记下以下各项 [!DNL Oracle Eloqua] 目标：

| 凭据 | 描述 |
| --- | --- |
| `Company Name` | 与您的关联的公司名称 [!DNL Oracle Eloqua] 帐户。 <br>您稍后将使用 `Company Name` 和 [!DNL Oracle Eloqua] `Username` 作为要用作 **[!UICONTROL 用户名]** 时间 [向目标进行身份验证](#authenticate). |
| `Username` | 您的用户名 [!DNL Oracle Eloqua] 帐户。 |
| `Password` | 您的密码 [!DNL Oracle Eloqua] 帐户。 |
| `Pod` | [!DNL Oracle Eloqua] 支持多个数据中心，每个数据中心具有唯一的域名。 [!DNL Oracle Eloqua] 这些称为“pods”，目前共有7个，分别为p01、p02、p03、p04、p06、p07和p08。 要获取您所在的POD，请登录 [!DNL Oracle Eloqua] 并记下成功登录后浏览器中的URL。 例如，如果您的浏览器URL为 `secure.p01.eloqua.com` 您的 `pod` 是 `p01`. 请参阅 [确定POD](https://community.oracle.com/topliners/discussion/4470225/determining-your-pod-number-for-oracle-eloqua) 页面以获取其他指导。 |

请参阅 [登录 [!DNL Oracle Eloqua]](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-user/Help/Administration/Tasks/SigningInToEloqua.htm#Signing) 作为指导。

## 护栏 {#guardrails}

>[!NOTE]
>
>* [!DNL Oracle Eloqua] 自定义联系人字段是使用以下期间选择的受众的名称自动创建的 **[!UICONTROL 选择区段]** 步骤。

* [!DNL Oracle Eloqua] 具有250个自定义联系人字段的最大限制。
* 在导出新受众之前，请确保包含的平台受众数量和现有受众数量 [!DNL Oracle Eloqua] 不要超过此限制。
* 如果超过此限制，您将在Experience Platform中遇到错误。 这是因为 [!DNL Oracle Eloqua] API无法验证请求，响应为 —  *400：存在验证错误*  — 描述问题的错误消息。
* 如果您已达到以上指定的限制，则需要从目标中删除现有映射，并删除中相应的自定义联系人字段。 [!DNL Oracle Eloqua] 帐户，然后才能导出更多区段。

* 请参阅 [[!DNL Oracle Eloqua] 创建联系人字段](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-user/Help/ContactFields/Tasks/CreatingContactFields.htm) 页面以了解有关其他限制的信息。

## 支持的身份 {#supported-identities}

[!DNL Oracle Eloqua] 支持更新下表中描述的标识。 了解有关 [身份](/help/identity-service/namespaces.md).

| 目标身份 | 描述 | 必需 |
|---|---|---|
| `EloquaId` | 联系人的唯一标识符。 | 是 |

## 导出类型和频率 {#export-type-frequency}

有关目标导出类型和频率的信息，请参阅下表。

| 项目 | 类型 | 注释 |
---------|----------|---------|
| 导出类型 | **[!UICONTROL 基于配置文件]** | <ul><li>您正在导出区段的所有成员以及所需的架构字段 *（例如：电子邮件地址、电话号码、姓氏）*，根据您的字段映射。</li><li> 对于Platform中的每个选定受众，将 [!DNL Oracle Eloqua] 区段状态将从Platform更新为受众状态。</li></ul> |
| 导出频率 | **[!UICONTROL 流]** | <ul><li>流目标为基于API的“始终运行”连接。 一旦根据受众评估在Experience Platform中更新了用户档案，连接器就会将更新发送到下游目标平台。 详细了解 [流目标](/help/destinations/destination-types.md#streaming-destinations).</li></ul> |

{style="table-layout:auto"}

## 连接到目标 {#connect}

>[!IMPORTANT]
>
>要连接到目标，您需要 **[!UICONTROL 查看目标]** 和 **[!UICONTROL 管理目标]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或与产品管理员联系以获取所需的权限。

要连接到此目标，请按照 [目标配置教程](../../ui/connect-destination.md). 在配置目标工作流中，填写下面两个部分中列出的字段。

范围 **[!UICONTROL 目标]** > **[!UICONTROL 目录]** 搜索 [!DNL (API) Oracle Eloqua]. 或者，您可以将其定位到 **[!UICONTROL 电子邮件营销]** 类别。

### 验证目标 {#authenticate}

>[!CONTEXTUALHELP]
>id="platform_destinations_apioracleeloqua_companyname_username"
>title="公司名称\用户名"
>abstract="在此字段中填写您的公司名称和来自 Oracle Eloqua 的用户名，格式为 `{COMPANY_NAME}\{USERNAME}`"

填写下面的必填字段。 请参阅 [收集 [!DNL Oracle Eloqua] 凭据](#gather-credentials) 部分获取任何指导。
* **[!UICONTROL 密码]**：您的密码 [!DNL Oracle Eloqua] 帐户。
* **[!UICONTROL 用户名]**：由以下各项组成的连接字符串： [!DNL Oracle Eloqua] 公司名称和 [!DNL Oracle Eloqua] 用户名。<br>连接的值采用以下形式 `{COMPANY_NAME}\{USERNAME}`.<br> 注意，请勿使用任何大括号或空格，并保留 `\`. <br>例如，如果您的 [!DNL Oracle Eloqua] 公司名称为 `MyCompany` 和 [!DNL Oracle Eloqua] 用户名是 `Username`，则您将在 **[!UICONTROL 用户名]** 字段为 `MyCompany\Username`.

要验证目标，请选择 **[!UICONTROL 连接到目标]**.
![显示如何进行身份验证的平台UI屏幕截图。](../../assets/catalog/email-marketing/oracle-eloqua-api/authenticate-destination.png)

如果提供的详细信息有效，UI将显示 **[!UICONTROL 已连接]** 带有绿色复选标记的状态。 然后，您可以继续执行下一步。

### 填写目标详细信息 {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_apioracleeloqua_pod"
>title="Pod"
>abstract="要查找您的 Pod 编号，请登录到 Oracle Eloqua。成功登录后，记下浏览器中的 URL。 "
>additional-url="https://support.oracle.com/knowledge/Oracle%20Cloud/2307176_1.html" text="Oracle 知识库 - 找出您的 Pod 编号"

要配置目标的详细信息，请填写下面的必需和可选字段。 UI中字段旁边的星号表示该字段为必填字段。
![显示目标详细信息的平台UI屏幕截图。](../../assets/catalog/email-marketing/oracle-eloqua-api/destination-details.png)

* **[!UICONTROL 名称]**：将来用于识别此目标的名称。
* **[!UICONTROL 描述]**：可帮助您将来识别此目标的描述。
* **[!UICONTROL Pod]**：要获取哪个 `pod` 您已登录，请登录 [!DNL Oracle Eloqua] 并记下成功登录后浏览器中的URL。 例如，如果您的浏览器URL为 `secure.p01.eloqua.com` 该 `pod` 您需要选择的值为 `p01`. 请参阅 [收集 [!DNL Oracle Eloqua] 凭据](#gather-credentials) 部分以获取其他指导。

### 启用警报 {#enable-alerts}

您可以启用警报，以接收有关发送到目标的数据流状态的通知。 从列表中选择警报以订阅接收有关数据流状态的通知。 有关警报的详细信息，请参阅以下内容中的指南： [使用UI订阅目标警报](../../ui/alerts.md).

完成提供目标连接的详细信息后，选择 **[!UICONTROL 下一个]**.

## 激活此目标的受众 {#activate}

>[!IMPORTANT]
> 
>* 要激活数据，您需要 **[!UICONTROL 查看目标]**， **[!UICONTROL 激活目标]**， **[!UICONTROL 查看配置文件]**、和 **[!UICONTROL 查看区段]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或与产品管理员联系以获取所需的权限。
>* 要导出 *身份*，您需要 **[!UICONTROL 查看身份图]** [访问控制权限](/help/access-control/home.md#permissions). <br> ![选择工作流中突出显示的身份命名空间以将受众激活到目标。](/help/destinations/assets/overview/export-identities-to-destination.png "选择工作流中突出显示的身份命名空间以将受众激活到目标。"){width="100" zoomable="yes"}

读取 [将用户档案和受众激活到流式受众导出目标](/help/destinations/ui/activate-segment-streaming-destinations.md) 有关将受众激活到此目标的说明。

### 映射注意事项和示例 {#mapping-considerations-example}

要正确地将受众数据从Adobe Experience Platform发送到 [!DNL Oracle Eloqua] 目标，您需要执行字段映射步骤。 映射包括在您的Platform帐户中的Experience Data Model (XDM)架构字段与其在目标目标中的相应等效字段之间创建链接。

要将XDM字段映射到 [!DNL Oracle Eloqua] 目标字段，请执行以下步骤：

1. 在 **[!UICONTROL 映射]** 步骤，选择 **[!UICONTROL 添加新映射]**. 您将在屏幕上看到一个新映射行。
1. 在 **[!UICONTROL 选择源字段]** 窗口中，选择 **[!UICONTROL 选择属性]** 类别并选择XDM属性或选择 **[!UICONTROL 选择身份命名空间]** 并选择身份。
1. 在 **[!UICONTROL 选择目标字段]** 窗口，选择 **[!UICONTROL 选择身份命名空间]** 并选择一个身份，或选择 **[!UICONTROL 选择自定义属性]** 并在中键入所需的属性名称 **[!UICONTROL 属性名称]** 字段。 您提供的属性名称应与中的现有联系人属性匹配 [!DNL Oracle Eloqua]. 请参阅 [[!DNL create a contact]](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/op-api-rest-1.0-data-contact-post.html) 中可以使用的确切属性名称 [!DNL Oracle Eloqua].
   * 重复这些步骤以在XDM配置文件架构和之间添加所需的和任何所需的属性映射。 [!DNL Oracle Eloqua]： | 源字段 | 目标字段 | 必需 | |—|—|—| |`IdentityMap: Eid`|`Identity: EloquaId`| 是 | |`xdm: personalEmail.address`|`Attribute: emailAddress`| 是 | |`xdm: personName.firstName`|`Attribute: firstName`| | |`xdm: personName.lastName`|`Attribute: lastName`| | |`xdm: workAddress.street1`|`Attribute: address1`| | |`xdm: workAddress.street2`|`Attribute: address2`| | |`xdm: workAddress.street3`|`Attribute: address3`| | |`xdm: workAddress.postalCode`|`Attribute: postalCode`| | |`xdm: workAddress.country`|`Attribute: country`| | |`xdm: workAddress.city`|`Attribute: city`| |

   * 下面显示了具有上述映射的示例：
     ![具有属性映射的平台UI屏幕快照示例。](../../assets/catalog/email-marketing/oracle-eloqua-api/mappings.png)

>[!IMPORTANT]
>
>* 中指定的属性 **[!UICONTROL 目标字段]** 应完全按照 [[!DNL Create a contact]](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/op-api-rest-1.0-data-contact-post.html) 因为这些属性将构成请求正文。
>* 中指定的属性 **[!UICONTROL 源字段]** 请勿遵循任何此类限制。 您可以根据需要进行映射，但是，如果数据格式在推送到时不正确 [!DNL Oracle Eloqua] 这将导致出现错误。 例如，您可以映射 **[!UICONTROL 源字段]** 身份命名空间 `contact key`， `ABC ID` 等等。 到 **[!UICONTROL 目标字段]** ： `EloquaId` 在确保ID值与接受的格式匹配之后 [!DNL Oracle Eloqua].
>* 此 `EloquaID` 必须执行映射才能更新与标识对应的属性。
>* 此 `emailAddress` 需要映射。 如果不使用这项调用，API将引发如下所示的错误：
>
>```json
>{
>     "type":"ObjectValidationError",
>     "container":{
>           "type":"ObjectKey",
>           "objectType":"Contact"
>     },
>     "property":"emailAddress",
>     "requirement":{
>           "type":"EmailAddressRequirement"
>     },
>     "value":"<null>"
>}
>```

完成提供目标连接的映射后，选择 **[!UICONTROL 下一个]**.

>[!NOTE]
>
>在将联系人字段信息发送到时，目标会在每次执行时自动为所选受众名称添加唯一标识符的后缀 [!DNL Oracle Eloqua]. 这可确保与受众名称对应的联系人字段名称不重叠。 请参阅 [验证数据导出](#exported-data) 部分屏幕快照示例 [!DNL Oracle Eloqua] “联系人详细信息”页面，其中包含使用受众名称创建的自定义联系人字段。

## 验证数据导出 {#exported-data}

要验证您是否正确设置了目标，请执行以下步骤：

1. 选择 **[!UICONTROL 目标]** > **[!UICONTROL 浏览]** 并导航到目标列表。
1. 接下来，选择目标并切换到 **[!UICONTROL 激活数据]** 选项卡，然后选择受众名称。
   ![显示目标激活数据的平台UI屏幕截图示例。](../../assets/catalog/email-marketing/oracle-eloqua-api/destinations-activation-data.png)

1. 监控受众摘要，并确保用户档案计数对应于区段中的计数。
   ![显示区段的平台UI屏幕截图示例。](../../assets/catalog/email-marketing/oracle-eloqua-api/segment.png)

1. 登录到 [!DNL Oracle Eloqua] 网站，然后导航到 **[!UICONTROL 联系人概述]** 页面检查是否已添加受众的用户档案。 要查看受众状态，请深入了解 **[!UICONTROL 联系人详细信息]** 页面，并检查是否已创建具有选定受众名称作为其前缀的联系人字段。

![oracleEloqua UI屏幕截图，其中显示了“联系人详细信息”页面，以及使用“受众”名称创建的自定义联系人字段。](../../assets/catalog/email-marketing/oracle-eloqua-api/contact.png)

## 数据使用和治理 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 目标在处理您的数据时符合数据使用策略。 有关如何执行操作的详细信息 [!DNL Adobe Experience Platform] 强制执行数据管理，请参见 [数据管理概述](/help/data-governance/home.md).

## 错误和故障排除 {#errors-and-troubleshooting}

在创建目标时，您可能会收到以下错误消息之一： `400: There was a validation error` 或 `400 BAD_REQUEST`. 当超过250个自定义联系人字段限制时，会发生这种情况，如 [护栏](#guardrails) 部分。 要修复此错误，请确保不超过 [!DNL Oracle Eloqua].
![平台UI屏幕截图显示错误。](../../assets/catalog/email-marketing/oracle-eloqua-api/error.png)

请参阅 [[!DNL Oracle Eloqua] HTTP状态代码](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/APIRequests_HTTPStatusCodes.html) 和 [[!DNL Oracle Eloqua] 验证错误](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/APIRequests_HTTPValidationErrors.html) 页面以获取状态和错误代码的完整列表及其说明。

## 其他资源 {#additional-resources}

欲知更多详情，请参见 [!DNL Oracle Eloqua] 文档：

* [oracleEloqua Marketing Automation](https://docs.oracle.com/en/cloud/saas/marketing/eloqua.html)
* [用于OracleEloquaMarketing Cloud服务的REST API](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/rest-endpoints.html)

### Changelog

此部分捕获此目标连接器的功能和重要文档更新。

+++ 查看更改日志

| 发行月份 | 更新类型 | 描述 |
|---|---|---|
| 2023 年 4 月 | 文档更新 | <ul><li>我们更新了 [用例](#use-cases) 部分中提供了客户何时将从使用此目标中受益的更清晰示例。</li> <li>我们更新了 [映射](#mapping-considerations-example) 部分，其中包含强制映射和可选映射的明确示例。</li> <li>我们更新了 [连接到目标](#connect) 部分中有关如何构造连接的值的示例 **[!UICONTROL 用户名]** 字段使用的 [!DNL Oracle Eloqua] 公司名称和 [!DNL Oracle Eloqua] 用户名。 (PLATIR-28343)</li><li>我们更新了 [收集 [!DNL Oracle Eloqua] 凭据](#gather-credentials) 和 [填写目标详细信息](#destination-details) 包含相关指导的部分 [!DNL Oracle Eloqua] **[!UICONTROL Pod]** 选择。 此 *&quot;Pod&quot;* 值由目标用来构建API调用的基本URL。 此 [[!DNL Oracle Eloqua] 先决条件](#prerequisites-destination) 此外，还更新了章节，提供了关于分配方案的指导 *“高级用户 — 营销权限”* 作为必需 *“安全组”* 您的 [!DNL Oracle Eloqua] 实例。</li></ul> |
| 2023 年 3 月 | 初始版本 | 初始目标版本和文档发布。 |

{style="table-layout:auto"}

+++