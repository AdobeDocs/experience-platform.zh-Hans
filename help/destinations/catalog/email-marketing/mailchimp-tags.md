---
title: Mailchimp标记
description: 通过Mailchimp标记目标，可导出帐户数据并在Mailchimp中激活以与联系人接洽。
last-substantial-update: 2024-02-20T00:00:00Z
exl-id: 0f278ca8-4fcf-4c47-b538-9cffa45a3d90
source-git-commit: c35b43654d31f0f112258e577a1bb95e72f0a971
workflow-type: tm+mt
source-wordcount: '1646'
ht-degree: 2%

---

# [!DNL Mailchimp Tags] 连接

[[!DNL Mailchimp]](https://mailchimp.com) *(也称为 [!DNL Intuit Mailchimp])* 是一个流行的营销自动化平台和电子邮件营销服务，企业使用它来管理和联系联系人 *（客户、客户或其他利益关系方）* 使用邮件列表和电子邮件营销活动。

[!DNL Mailchimp Tags] 用途 [受众](https://mailchimp.com/help/getting-started-audience/) 和 [标记](https://mailchimp.com/help/getting-started-tags/) 以管理您的联系信息。 标记是一种标签，您可以使用它来组织联系人，并在中标记以进行内部分类 [!DNL Mailchimp].

比较对象 [!DNL Mailchimp Interest Categories] 根据您的联系人的兴趣和喜好对联系人进行排序， [!DNL Mailchimp Tags] 用于管理您的联系人可能感兴趣的主题的订阅。 *请注意，Experience Platform还连接了 [!DNL Mailchimp Interest Categories]，您可以在 [[!DNL Mailchimp Interest Categories]](/help/destinations/catalog/email-marketing/mailchimp-interest-categories.md) 页面。*

此 [!DNL Adobe Experience Platform] [目标](/help/destinations/home.md) 利用 [[!DNL Mailchimp batch subscribe or unsubscribe API]](https://mailchimp.com/developer/marketing/api/lists/batch-subscribe-or-unsubscribe/) 端点。 您可以 **添加新联系人** 或 **更新现有标记 [!DNL Mailchimp] 联系人** 在现有 [!DNL Mailchimp] 在新的受众中激活它们后的受众。 [!DNL Mailchimp Tags] 将来自Platform的选定受众名称用作中的标记名称 [!DNL Mailchimp].

## 用例 {#use-cases}

为了帮助您更好地了解您应该如何以及何时使用 [!DNL Mailchimp Tags] 目标，以下是Adobe Experience Platform客户可以使用此目标解决的示例用例。

### 向营销活动的联系人发送电子邮件 {#use-case-send-emails}

组织的销售部门希望向精心策划的联系人列表广播基于电子邮件的营销活动。 联系人列表是从不同的离线来源批量接收的，因此需要对其进行跟踪。 团队发现现有的 [!DNL Mailchimp] ，并开始构建Experience Platform受众，每个列表中的联系人将添加到这些受众中。 将这些受众发送至 [!DNL Mailchimp Tags]，如果所选中不存在任何联系人 [!DNL Mailchimp] 受众时，将会添加一个关联的标记，其中包含联系人所属的受众名称。 如果有任何联系人已存在于 [!DNL Mailchimp] 受众将添加一个名为受众的新标记。 由于标签在中可见 [!DNL Mailchimp] 可以轻松识别离线源。 在将数据发送到之后 [!DNL Mailchimp] 他们向受众发送营销活动电子邮件。

## 先决条件 {#prerequisites}

请参阅以下部分，以了解需要在Experience Platform中设置的任何先决条件， [!DNL Mailchimp] ，以了解在使用之前需要收集的信息 [!DNL Mailchimp Tags] 目标。

### Experience Platform中的先决条件 {#prerequisites-in-experience-platform}

将数据激活到之前 [!DNL Mailchimp Tags] 目标，您必须拥有 [架构](/help/xdm/schema/composition.md)， a [数据集](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=en)、和 [受众](https://experienceleague.adobe.com/docs/platform-learn/tutorials/audiences/create-audiences.html) 创建于 [!DNL Experience Platform].

### 的先决条件 [!DNL Mailchimp Tags] 目标 {#prerequisites-destination}

请注意以下先决条件，以便将数据从Platform导出到 [!DNL Mailchimp Tags] 帐户：

#### 您需要拥有 [!DNL Mailchimp] 帐户 {#prerequisites-account}

在创建之前 [!DNL Mailchimp Tags] 目标，您必须首先确保 [!DNL Mailchimp] 帐户。 如果您还没有客户，请访问 [[!DNL Mailchimp] 注册页面](https://login.mailchimp.com/signup/) 注册并创建您的帐户。

#### 收集 [!DNL Mailchimp] API密钥 {#gather-credentials}

您需要您的 [!DNL Mailchimp] **API密钥** 验证 [!DNL Mailchimp Interest Categories] 针对您的目标 [!DNL Mailchimp] 帐户。 此 **API密钥** 将用作 **密码** 当您 [验证目标](#authenticate).

如果您没有 **API密钥**，登录到您的 [!DNL Mailchimp] ，请参阅 [!DNL Mailchimp] 文档 [如何生成API密钥](https://mailchimp.com/developer/marketing/guides/quick-start/#generate-your-api-key).

API密钥的示例如下 `0123456789abcdef0123456789abcde-us14`.

>[!IMPORTANT]
>
>如果您生成 **API密钥**，请记下它，因为一代一代人之后您将无法访问它。

#### 识别您的 [!DNL Mailchimp] 数据中心 {#identify-data-center}

接下来，您必须识别您的 [!DNL Mailchimp] 数据中心。 为此，请登录 [!DNL Mailchimp] 帐户并导航到 **API密钥部分** 您的帐户的。

数据中心ID是您在浏览器中看到的URL的第一部分。 如果URL为 *https://`us14`.mailchimp.com/account/api/*，则数据中心为 `us14`.

数据中心ID还会附加到表单中的API密钥中 *key-dc*；例如，如果您的API密钥为 `0123456789abcdef0123456789abcde-us14`，则数据中心为 `us14`.

写下数据中心的价值 *(`us14` 在此示例中)*. 您需要此值 [填写目标详细信息](#destination-details).

如果您需要进一步指导，请参阅 [[!DNL Mailchimp] 基础知识文档](https://mailchimp.com/developer/marketing/docs/fundamentals/#api-structure).

### 护栏 {#guardrails}

请参阅 [!DNL Mailchimp] [速率限制](https://mailchimp.com/developer/marketing/docs/fundamentals/#api-limits) 欲详细了解 [!DNL Mailchimp] API。

## 支持的身份 {#supported-identities}

[!DNL Mailchimp] 支持激活下表中描述的标识。 了解有关 [身份](/help/identity-service/features/namespaces.md).

| 目标身份 | 描述 | 注意事项 |
|---|---|---|
| 电子邮件 | 联系人的电子邮件地址。 | 必需 |

{style="table-layout:auto"}

## 支持的受众 {#supported-audiences}

此部分介绍可将哪种类型的受众导出到此目标。

| 受众来源 | 支持 | 描述 |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ {\f13 } | 通过Experience Platform生成的受众 [分段服务](../../../segmentation/home.md). |
| 自定义上传 | ✓ {\f13 } | 受众 [已导入](../../../segmentation/ui/audience-portal.md#import-audience) 从CSV文件Experience Platform到。 |

{style="table-layout:auto"}

## 导出类型和频率 {#export-type-frequency}

有关目标导出类型和频率的信息，请参阅下表。

| 项目 | 类型 | 注释 |
---------|----------|---------|
| 导出类型 | **[!UICONTROL 基于配置文件]** | <ul><li>您正在导出受众的所有成员以及所需的架构字段 *（例如：电子邮件地址、电话号码、姓氏）*，根据您的字段映射。</li><li> 对于在Platform中选择的每个受众，对应的 [!DNL Mailchimp Tags] 区段状态将通过Platform中的受众状态进行更新。</li></ul> |
| 导出频率 | **[!UICONTROL 流]** | 流目标为基于API的“始终运行”连接。 一旦根据受众评估在Experience Platform中更新了用户档案，连接器就会将更新发送到下游目标平台。 详细了解 [流目标](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## 连接到目标 {#connect}

>[!IMPORTANT]
>
>要连接到目标，您需要 **[!UICONTROL 管理目标]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或与产品管理员联系以获取所需的权限。

要连接到此目标，请按照 [目标配置教程](../../ui/connect-destination.md). 在配置目标工作流中，填写下面两个部分中列出的字段。

范围 **[!UICONTROL 目标]** > **[!UICONTROL 目录]**，搜索 [!DNL Mailchimp Tags]. 或者，您可以将其定位到 **[!UICONTROL 电子邮件营销]** 类别。

### 验证目标 {#authenticate}

要向目标进行身份验证，请填写以下必填字段并选择 **[!UICONTROL 连接到目标]**.

| 字段 | 描述 |
| --- | --- |
| **[!UICONTROL 用户名]** | 您的 [!DNL Mailchimp] 用户名。 |
| **[!UICONTROL 密码]** | 您的 [!DNL Mailchimp] **API密钥**，您已在 [收集 [!DNL Mailchimp] 凭据](#gather-credentials) 部分。<br> 您的API密钥采用以下形式 `{KEY}-{DC}`，其中 `{KEY}` 部分指 [[!DNL Mailchimp] API密钥](#gather-credentials) 部分和 `{DC}` 部分是指 [[!DNL Mailchimp] 数据中心](#identify-data-center). <br>您可以提供 `{KEY}` 部分或整个表单。<br> 例如，如果您的API密钥为 <br>*`0123456789abcdef0123456789abcde-us14`*，<br> 您可以提供&#x200B;*`0123456789abcdef0123456789abcde`*或&#x200B;*`0123456789abcdef0123456789abcde-us14`*作为值。 |

{style="table-layout:auto"}

![显示如何进行身份验证的平台UI屏幕截图。](../../assets/catalog/email-marketing/mailchimp-tags/authenticate-destination.png)

如果提供的详细信息有效，UI将显示 **[!UICONTROL 已连接]** 带有绿色复选标记的状态。 然后，您可以继续执行下一步。

### 填写目标详细信息 {#destination-details}

要配置目标的详细信息，请填写下面的必需和可选字段。 UI中字段旁边的星号表示该字段为必填字段。

![显示目标详细信息的平台UI屏幕截图。](../../assets/catalog/email-marketing/mailchimp-tags/destination-details.png)

| 字段 | 描述 |
| --- | --- |
| **[!UICONTROL 名称]** | 将来用于识别此目标的名称。 |
| **[!UICONTROL 描述]** | 可帮助您以后识别此目标的描述。 |
| **[!UICONTROL 数据中心]** | 您的 [!DNL Mailchimp] 帐户 `data center`. 请参阅 [识别 [!DNL Mailchimp] 数据中心](#identify-data-center) 部分获取任何指导。 |
| **[!UICONTROL 受众名称（请先输入数据中心）]** | 输入您的 **[!UICONTROL 数据中心]**，此下拉列表中自动填充您的 [!DNL Mailchimp] 帐户。 选择要使用Platform中的数据更新的受众。 |

{style="table-layout:auto"}

### 启用警报 {#enable-alerts}

您可以启用警报，以接收有关发送到目标的数据流状态的通知。 从列表中选择警报以订阅接收有关数据流状态的通知。 有关警报的详细信息，请参阅以下内容中的指南： [使用UI订阅目标警报](../../ui/alerts.md).

完成提供目标连接的详细信息后，选择 **[!UICONTROL 下一个]**.

## 激活此目标的受众 {#activate}

>[!IMPORTANT]
> 
>* 要激活数据，您需要 **[!UICONTROL 查看目标]**， **[!UICONTROL 激活目标]**， **[!UICONTROL 查看配置文件]**、和 **[!UICONTROL 查看区段]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或与产品管理员联系以获取所需的权限。
>* 要导出 *身份*，您需要 **[!UICONTROL 查看身份图]** [访问控制权限](/help/access-control/home.md#permissions). <br> ![选择工作流中突出显示的身份命名空间以将受众激活到目标。](/help/destinations/assets/overview/export-identities-to-destination.png "选择工作流中突出显示的身份命名空间以将受众激活到目标。"){width="100" zoomable="yes"}

读取 [将受众激活到流目标](/help/destinations/ui/activate-segment-streaming-destinations.md) 有关将受众激活到此目标的说明。

### 映射注意事项和示例 {#mapping-considerations-example}

要正确地将受众数据从Adobe Experience Platform发送到 [!DNL Mailchimp Tags] 目标，您需要执行字段映射步骤。 映射包括在您的Platform帐户中的Experience Data Model (XDM)架构字段与其在目标目标中的相应等效字段之间创建链接。

要将XDM字段正确映射到 [!DNL Mailchimp Tags] 目标字段，请执行以下步骤：

1. 在 **[!UICONTROL 映射]** 步骤，选择 **[!UICONTROL 添加新映射]**. 您将在屏幕上看到一个新映射行。
1. 在 **[!UICONTROL 选择源字段]** 窗口，选择 **[!UICONTROL 选择身份命名空间]** 并选择 `Email` 身份命名空间。

   ![Source字段作为来自身份命名空间的电子邮件的平台UI屏幕截图。](../../assets/catalog/email-marketing/mailchimp-tags/source-field.png)

1. 在 **[!UICONTROL 选择目标字段]** 窗口，选择 **[!UICONTROL 选择身份命名空间]** 并选择 `Email` 身份命名空间。

   ![Platform UI屏幕截图，其中Target字段为来自身份命名空间的电子邮件。](../../assets/catalog/email-marketing/mailchimp-tags/target-field.png)

   XDM配置文件架构与 [!DNL Mailchimp Tags] 将如下所示： | Source字段 | 目标字段 | 必需 | | — | — | — | |`IdentityMap: Email`|`Identity: Email`| 是 |

   下面显示了具有已完成映射的示例：
   ![显示字段映射的平台UI屏幕快照示例。](../../assets/catalog/email-marketing/mailchimp-tags/mappings.png)

完成提供目标连接的映射后，选择 **[!UICONTROL 下一个]**.

## 验证数据导出 {#exported-data}

要验证您是否正确设置了目标，请执行以下步骤：

1. 登录 [[!DNL Mailchimp]](https://login.mailchimp.com/) 帐户。 然后导航到 **[!DNL Audience]** > **[!DNL All Contacts]** 页面，并检查受众中的联系人是否已添加，以及受众中的联系人是否已使用受众名称进行更新。
   ![显示“受众”页面的Mailchimp UI屏幕截图。](../../assets/catalog/email-marketing/mailchimp-tags/contacts.png)

## 数据使用和治理 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 目标在处理您的数据时符合数据使用策略。 有关如何执行操作的详细信息 [!DNL Adobe Experience Platform] 强制执行数据管理，请参见 [数据管理概述](/help/data-governance/home.md).

## 错误和故障排除 {#errors-and-troubleshooting}

请参阅 [[!DNL Mailchimp] 错误页面](https://mailchimp.com/developer/marketing/docs/errors/) 以获取状态和错误代码的完整列表及其说明。

## 其他资源 {#additional-resources}

其他有用信息来自 [!DNL Mailchimp] 文档如下所示：
* [快速入门 [!DNL Mailchimp]](https://mailchimp.com/help/getting-started-with-mailchimp/)
* [受众快速入门](https://mailchimp.com/help/getting-started-audience/)
* [创建受众](https://mailchimp.com/help/create-audience/)
* [标记快速入门](https://mailchimp.com/help/getting-started-tags/)
* [营销API](https://mailchimp.com/developer/marketing/api/)
