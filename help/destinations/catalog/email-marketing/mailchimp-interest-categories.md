---
title: Mailchimp 兴趣类别
description: Mailchimp（也称为Intuit Mailchimp）是一种流行的营销自动化平台和电子邮件营销服务，企业使用它来管理和与联系人（客户、客户或其他利益相关方）交谈，使用邮件列表和电子邮件营销活动。 使用此连接器可以根据联系人的兴趣和偏好对他们进行排序。
last-substantial-update: 2023-05-24T00:00:00Z
source-git-commit: a293df660a9b959d12bdc170d1cb69f3543a30f1
workflow-type: tm+mt
source-wordcount: '2356'
ht-degree: 2%

---

# [!DNL Mailchimp Interest Categories] 连接

[[!DNL Mailchimp]](https://mailchimp.com) 是一个流行的营销自动化平台和电子邮件营销服务，企业使用该平台管理和联系信息 *（客户、客户或其他利益关系方）* 使用邮件列表和电子邮件营销活动。 使用此连接器可以根据联系人的兴趣和偏好对他们进行排序。

[!DNL Mailchimp Interest Categories] 用途 [受众](https://mailchimp.com/help/getting-started-audience/)， [组](https://mailchimp.com/help/getting-started-with-groups/)和兴趣类别 *（也称为组名或组标题）*. 每个 [!DNL Mailchimp] 组是兴趣类别的列表。 当联系人通过您网站上的注册表单订阅一个或多个兴趣类别时，他们与兴趣类别相关联。 在受众中，您还可以将联系人组织到组中，并将其与兴趣类别相关联，然后可以使用这些组来创建区段。 您可以使用这些受众向订阅的联系人广播定向的活动电子邮件。

<!--
Compared to [!DNL Mailchimp Tags] which you would use for internal classification, [!DNL Mailchimp Interest Categories] is meant to manage subscriptions to topics of interest that your contacts might be interested in. *Note, Experience Platform also has a connection for [!DNL Mailchimp Tags], you can check it out on the [[!DNL Mailchimp Tags]](/help/destinations/catalog/email-marketing/mailchimp-tags.md) page.*
-->

此 [!DNL Adobe Experience Platform] [目标](/help/destinations/home.md) 使用 [[!DNL Mailchimp batch subscribe or unsubscribe API]](https://mailchimp.com/developer/marketing/api/lists/batch-subscribe-or-unsubscribe/) 要创建的API [兴趣类别](https://mailchimp.com/developer/marketing/api/interest-categories/) 然后，将来自每个选定平台受众的联系人添加到相应的兴趣类别中。 您可以 **添加新联系人** 或 **更新现有的信息 [!DNL Mailchimp] 联系人**，则 **添加或从所需组中删除它们** 在现有 [!DNL Mailchimp] 受众在新区段中激活后，发送电子邮件给访客。 [!DNL Mailchimp Interest Groups] 将来自Platform的选定受众名称用作中的兴趣类别 [!DNL Mailchimp].

## 用例 {#use-cases}

为了帮助您更好地了解应该如何以及何时使用 [!DNL Mailchimp Interest Categories] 目标，以下是Adobe Experience Platform客户可以使用此目标解决的示例用例。

### 向营销活动的联系人发送电子邮件 {#use-case-send-emails}

一家体育用品网站的销售部门希望向一连串自称对足球感兴趣的熟人广播一个基于电子邮件的营销活动。 联系人列表在从网站开发团队收到的数据导出中分批显示，因此需要对其进行跟踪。 该团队标识一个现有的 [!DNL Mailchimp] ，并开始构建Experience Platform受众，每个列表中的联系人都会添加到这些受众中。 将这些受众发送至 [!DNL Mailchimp Interest Categories]，如果选定联系人中不存在任何联系人 [!DNL Mailchimp] 使用联系人所属受众名称将他们添加到群组。 如果有任何联系人已存在于 [!DNL Mailchimp] 随后将更新其信息。 一旦将数据发送到 [!DNL Mailchimp Interest Categories]，销售团队可以选择营销活动电子邮件并将其发送到中的足球兴趣组 [!DNL Mailchimp] 受众。

## 先决条件 {#prerequisites}

请参阅以下部分，了解需要在Experience Platform中设置的任何先决条件，并且 [!DNL Mailchimp] ，以了解在使用之前必须收集的信息 [!DNL Mailchimp Interest Categories] 目标。

### Experience Platform中的先决条件 {#prerequisites-in-experience-platform}

将数据激活到之前 [!DNL Mailchimp Interest Categories] 目标，您必须拥有 [架构](/help/xdm/schema/composition.md)， a [数据集](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=en)、和 [区段](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=en) 创建于 [!DNL Experience Platform].

### 的先决条件 [!DNL Mailchimp Interest Categories] 目标 {#prerequisites-destination}

请注意以下先决条件，以便将数据从Platform导出到 [!DNL Mailchimp] 帐户：

#### 您必须拥有 [!DNL Mailchimp] 帐户 {#prerequisites-account}

在创建 [!DNL Mailchimp Interest Categories] 目标，您必须首先确保 [!DNL Mailchimp] 帐户。 如果您还没有这样的网站，请访问 [[!DNL Mailchimp] 注册页面](https://login.mailchimp.com/signup/) 注册并创建您的帐户。

#### 收集 [!DNL Mailchimp] API密钥 {#gather-credentials}

您需要您的 [!DNL Mailchimp] **API密钥** 验证 [!DNL Mailchimp Interest Categories] 针对您的目标 [!DNL Mailchimp] 帐户。 此 **API密钥** 将用作 **密码** 当您 [验证目标](#authenticate).

如果您没有 **API密钥**，登录到您的帐户并参阅 [[!DNL Mailchimp] 生成API密钥](https://mailchimp.com/developer/marketing/guides/quick-start/#generate-your-api-key) 文档以创建一个。

API密钥的示例如下 `0123456789abcdef0123456789abcde-us14`.

>[!IMPORTANT]
>
>如果您生成 **API密钥**，请记下它，因为您无法在世代之后访问它。

#### 识别 [!DNL Mailchimp] 数据中心 {#identify-data-center}

接下来，您必须识别您的 [!DNL Mailchimp] 数据中心。 为此，请登录 [!DNL Mailchimp] 帐户并导航到 **API密钥部分** ，而不是您的帐户。

值是您在浏览器中看到的URL的第一部分。 如果URL为 *https://`us14`.mailchimp.com/account/api/*，则数据中心为 `us14`.

它还以表单形式附加到您的API密钥中 *key-dc*；如果您的API密钥为 `0123456789abcdef0123456789abcde-us14`，则数据中心为 `us14`.

写下数据中心的价值 *(`us14` 在此示例中)*，则您需要使用此值，但前提是 [填写目标详细信息](#destination-details).

如果您需要进一步指导，请参阅 [[!DNL Mailchimp] 基础知识文档](https://mailchimp.com/developer/marketing/docs/fundamentals/#api-structure).

### 护栏 {#guardrails}

您的 [!DNL Mailchimp] 受众可以在一个群组中或在同一个受众内的多个群组中包含最多60个群组名称（或兴趣类别）。 请参阅 [!DNL Mailchimp] [组](https://mailchimp.com/help/getting-started-with-groups/) 以取得任何澄清。 达到此限制后，您将 `400 BAD_REQUEST Cannot have more than 60 interests per list (Across all categories)` 作为错误响应的消息 [!DNL Mailchimp] API。

此外，请参阅 [!DNL Mailchimp] [速率限制](https://mailchimp.com/developer/marketing/docs/fundamentals/#api-limits) 详细了解CJA对 [!DNL Mailchimp] API。

## 支持的身份 {#supported-identities}

[!DNL Mailchimp] 支持激活下表中描述的标识。 详细了解 [身份](/help/identity-service/namespaces.md).

| 目标身份 | 描述 | 注意事项 |
|---|---|---|
| 电子邮件 | 联系人电子邮件地址 | 必需 |

{style="table-layout:auto"}

## 导出类型和频率 {#export-type-frequency}

有关目标导出类型和频率的信息，请参阅下表。

| 项目 | 类型 | 注释 |
---------|----------|---------|
| 导出类型 | **[!UICONTROL 基于配置文件]** | <ul><li>您正在导出区段的所有成员以及所需的架构字段 *（例如：电子邮件地址、电话号码、姓氏）*，根据您的字段映射。</li><li> 对于Platform中的每个选定受众，将 [!DNL Mailchimp Interest Categories] 区段状态通过Platform中的受众状态进行更新。</li></ul> |
| 导出频率 | **[!UICONTROL 流]** | 流目标为基于API的“始终运行”连接。 当基于受众评估在Experience Platform中更新用户档案时，连接器将更新向下发送到目标平台。 详细了解 [流式目标](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## 连接到目标 {#connect}

>[!IMPORTANT]
>
>要连接到目标，您需要 **[!UICONTROL 管理目标]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或与产品管理员联系以获取所需的权限。

要连接到此目标，请按照 [目标配置教程](../../ui/connect-destination.md). 在配置目标工作流中，填写下面两节中列出的字段。

范围 **[!UICONTROL 目标]** > **[!UICONTROL 目录]**，搜索 [!DNL Mailchimp Interest Categories]. 或者，您也可以在 **[!UICONTROL 电子邮件营销]** 类别。

### 向目标进行身份验证 {#authenticate}

要向目标进行身份验证，请填写以下必填字段并选择 **[!UICONTROL 连接到目标]**.

| 字段 | 描述 |
| --- | --- |
| **[!UICONTROL 用户名]** | 您的 [!DNL Mailchimp Interest Categories] 用户名。 |
| **[!UICONTROL 密码]** | 您的 [!DNL Mailchimp] **API密钥**，您已在 [收集 [!DNL Mailchimp] 凭据](#gather-credentials) 部分。<br> 您的API密钥采用以下形式 `{KEY}-{DC}`，其中 `{KEY}` 部分指 [[!DNL Mailchimp] API密钥](#gather-credentials) 部分和 `{DC}` 部分是指 [[!DNL Mailchimp] 数据中心](#identify-data-center). <br>您可以提供 `{KEY}` 部分或整个表单。<br> 例如，如果您的API密钥为 <br>*`0123456789abcdef0123456789abcde-us14`*，<br> 您可以提供&#x200B;*`0123456789abcdef0123456789abcde`*或&#x200B;*`0123456789abcdef0123456789abcde-us14`*作为值。 |

{style="table-layout:auto"}

![显示如何进行身份验证的Platform UI屏幕快照。](../../assets/catalog/email-marketing/mailchimp-interest-categories/authenticate-destination.png)

如果提供的详细信息有效，则UI将显示 **[!UICONTROL 已连接]** 带有绿色复选标记的状态。 然后，您可以继续执行下一步。

### 填写目标详细信息 {#destination-details}

要配置目标的详细信息，请填写下面的必需和可选字段。 UI中字段旁边的星号表示该字段为必填字段。

![显示目标详细信息的Platform UI屏幕快照。](../../assets/catalog/email-marketing/mailchimp-interest-categories/destination-details.png)

| 字段 | 描述 |
| --- | --- |
| **[!UICONTROL 名称]** | 将来用于识别此目标的名称。 |
| **[!UICONTROL 描述]** | 可帮助您将来标识此目标的描述。 |
| **[!UICONTROL 数据中心]** | 您的 [!DNL Mailchimp] 帐户 `data center`. 请参阅 [识别 [!DNL Mailchimp] 数据中心](#identify-data-center) 部分获取任何指导。 |
| **[!UICONTROL 受众名称（请先选择数据中心）]** | 选择您的 **[!UICONTROL 数据中心]**，此下拉列表中将自动填充 [!DNL Mailchimp] 帐户。 选择要使用Platform中的数据更新的受众。 |
| **[!UICONTROL 兴趣类别（请先选择数据中心和受众名称）]** | 选择您的 **[!UICONTROL 受众名称]**，此下拉列表中自动填充您的中的兴趣组类别名称， [!DNL Mailchimp] 帐户。 选择要使用来自Platform的数据更新的类别名称。 |

{style="table-layout:auto"}

>[!TIP]
>
> 如果您提供的API密钥 **[!UICONTROL 密码]** 字段或 **[!UICONTROL 数据中心]** 值不正确，UI显示 [!DNL Mailchimp] API错误响应： *`No options are available. Please verify the values selected for the following dependent fields: dataCenter`* 如下所示。 在这种情况下，您无法从 **[!UICONTROL 受众名称（请先选择数据中心）]** 字段。 要修复此错误，请提供正确的值。

### 启用警报 {#enable-alerts}

您可以启用警报，以接收有关流向目标的数据流状态的通知。 从列表中选择警报以订阅接收有关数据流状态的通知。 有关警报的更多信息，请参阅以下指南中的 [使用UI订阅目标警报](../../ui/alerts.md).

完成提供目标连接的详细信息后，选择 **[!UICONTROL 下一个]**.

## 将受众激活到此目标 {#activate}

>[!IMPORTANT]
>
>要激活数据，您需要 **[!UICONTROL 管理目标]**， **[!UICONTROL 激活目标]**， **[!UICONTROL 查看配置文件]**、和 **[!UICONTROL 查看区段]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或与产品管理员联系以获取所需的权限。

读取 [将用户档案和受众激活到流式受众导出目标](/help/destinations/ui/activate-segment-streaming-destinations.md) 有关将受众激活到此目标的说明。

### 映射注意事项和示例 {#mapping-considerations-example}

要正确地将受众数据从Adobe Experience Platform发送到 [!DNL Mailchimp Interest Categories] 目标，您必须完成字段映射步骤。 映射包括在Platform帐户中的Experience Data Model (XDM)架构字段与其与目标目标中的相应等效字段之间创建链接。

要将XDM字段正确映射到 [!DNL Mailchimp Interest Categories] 目标字段，请执行以下步骤：

1. 在 **[!UICONTROL 映射]** 步骤，选择 **[!UICONTROL 添加新映射]**. 您现在可以在屏幕上看到新的映射行。
1. 在 **[!UICONTROL 选择源字段]** 窗口中，选择 **[!UICONTROL 选择属性]** 类别并选择XDM属性或选择 **[!UICONTROL 选择身份命名空间]** 并选择身份。
1. 在 **[!UICONTROL 选择目标字段]** 窗口中，选择 **[!UICONTROL 选择身份命名空间]** 并选择身份或选择 **[!UICONTROL 选择属性]** 类别并从填充自 [!DNL Mailchimp] API。 *已添加到所选内容的任何自定义属性 [!DNL Mailchimp] 受众也可用作目标字段供选择。*

   XDM配置文件架构与之间的可用映射 [!DNL Mailchimp Interest Categories] 如下所示： |源字段 |目标字段 |注释 | | — | — | — | |`IdentityMap: Email`|`Identity: email`|必需：是 | |`xdm: person.name.firstName`|`Attribute: FNAME`| | |`xdm: person.name.lastName`|`Attribute: LNAME`| | |`xdm: person.birthDayAndMonth`|`Attribute: BIRTHDAY`| |

   此外， `ADDRESS` 是一个特殊的目标字段，称为 `merge field` 在您的 [!DNL Mailchimp] 受众。 此 [[!DNL Mailchimp] 文档](https://mailchimp.com/developer/marketing/docs/merge-fields/) 将所需的键定义为 `addr1`， `city`， `state`、和 `zip`和可选键 `addr2` 和 `country`. 这些字段的值必须为字符串。 如果任意 `ADDRESS` 字段映射存在，目标传递 `ADDRESS` 对象 [!DNL Mailchimp] API更新。 任意 `ADDRESS` 未映射的字段其值默认为 `NULL` 除默认的国家/地区之外 `US`.

   可用于的映射 `ADDRESS` 字段如下所示：

   | 源字段 | 目标字段 |
   | --- | --- |
   | `xdm: workAddress.street1` | `Attribute: ADDRESS.addr1` |
   | `xdm: workAddress.street2` | `Attribute: ADDRESS.addr2` |
   | `xdm: workAddress.city` | `Attribute: ADDRESS.city` |
   | `xdm: workAddress.state` | `Attribute: ADDRESS.state` |
   | `xdm: workAddress.postalCode` | `Attribute: ADDRESS.zip` |
   | `xdm: workAddress.country` | `Attribute: ADDRESS.country` |

   例如，要更新以下项的值： `country` 使用联系人的现有地址字段 `addr1`， `city`， `state`、和 `zip` 值 `132, My Street, Kingston`， `New York`， `New York` 和 `12401`. 要更新 `country` 您必须传递包含更改的现有值 *（如果有）* 以及国家的新价值。 因此，数据集中的值应为 `132, My Street, Kingston`， `New York`， `New York`， `12401`、和 `US`. 再次重申，如果您只通过 `country` 并且不提供值 `addr1`， `city`， `state`、和 `zip` 它们将被覆盖 `NULL`.

   下面显示了具有已完成映射的示例：
   ![显示字段映射的平台UI屏幕快照示例。](../../assets/catalog/email-marketing/mailchimp-interest-categories/mappings.png)

完成提供目标连接的映射后，选择 **[!UICONTROL 下一个]**.

## 验证数据导出 {#exported-data}

要验证您是否正确设置了目标，请执行以下步骤：

* 登录 [[!DNL Mailchimp]](https://login.mailchimp.com/) 帐户。 然后，导航到 **[!DNL Audience]** 页面。 接下来，展开 **[!DNL Manage Contacts]** 菜单并选择 **[!DNL Groups]**.

![显示“受众”组页面的Mailchimp UI屏幕截图。](../../assets/catalog/email-marketing/mailchimp-interest-categories/audience-groups.png)

* 选择组，然后检查所选受众是否被创建为类别，且类别后跟一个自动生成的后缀。
   * 此目标使用所选区段的名称通过使用 [[!DNL Mailchimp] 添加兴趣类别API](https://mailchimp.com/developer/marketing/api/interest-categories/add-interest-category/). 如果您创建新目标并再次激活相同的受众， [!DNL Mailchimp] 添加后缀以区分现有区段和新区段。
* 群组中不存在其电子邮件的联系人会添加到新创建的类别中。
* 对于组中已存在的联系人，属性字段数据将更新，联系人将添加到新创建的类别。

![显示“受众”组类别的Mailchimp UI屏幕截图。](../../assets/catalog/email-marketing/mailchimp-interest-categories/audience-groups-category.png)

## 数据使用和管理 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 目标在处理您的数据时符合数据使用策略。 有关以下方面的详细信息： [!DNL Adobe Experience Platform] 强制执行数据管理，请参见 [数据治理概述](/help/data-governance/home.md).

## 错误和疑难解答 {#errors-and-troubleshooting}

### 在以下情况下遇到错误： [!DNL Mailchimp] API密钥或数据中心值不正确 {#incorrect-credentials-error}

如果您提供的API密钥 **[!UICONTROL 密码]** 字段或 **[!UICONTROL 数据中心]** 值不正确，UI显示 [!DNL Mailchimp] API错误响应： *`No options are available. Please verify the values selected for the following dependent fields: dataCenter`* 如下所示。 在这种情况下，您无法从 **[!UICONTROL 受众名称（请先选择数据中心）]** 字段。

![Platform UI屏幕截图显示如果您的Mailchimp API密钥或数据中心值不正确，则会出现错误。](../../assets/catalog/email-marketing/mailchimp-interest-categories/error.png)

要修复此错误并继续进行下一步，您必须提供正确的值。 请参阅 [识别 [!DNL Mailchimp] 数据中心](#identify-data-center) 和
[收集 [!DNL Mailchimp] API密钥](#gather-credentials) 需要指导的区域。

### 在以下情况下遇到错误： [!DNL Mailchimp] 超过组名称限制 {#group-name-limits-error}

在创建目标时，您可能会收到以下错误消息： *`Cannot have more than 60 interests per list (Across all categories)`* 或 *`400 BAD_REQUEST`*. 当单个组中或同一受众限制内跨多个组超过60个组名称（或兴趣类别）时(如 [护栏](#guardrails) 部分。 要修复此错误，请确保未超过中的组名称限制 [!DNL Mailchimp].

### [!DNL Mailchimp] 状态和错误代码

请参阅 [[!DNL Mailchimp] 错误页面](https://mailchimp.com/developer/marketing/docs/errors/) 以获取状态和错误代码的完整列表及其说明。

## 其他资源 {#additional-resources}

其他有用信息来自 [!DNL Mailchimp] 文档如下所示：
* [快速入门 [!DNL Mailchimp]](https://mailchimp.com/help/getting-started-with-mailchimp/)
* [Audiences入门](https://mailchimp.com/help/getting-started-audience/)
* [创建受众](https://mailchimp.com/help/create-audience/)
* [组快速入门](https://mailchimp.com/help/getting-started-with-groups/)
* [创建新的受众组](https://mailchimp.com/help/create-new-audience-group/)
* [兴趣类别](https://mailchimp.com/developer/marketing/api/interest-categories/)
* [营销API](https://mailchimp.com/developer/marketing/api/)
