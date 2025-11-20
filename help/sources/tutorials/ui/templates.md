---
description: 了解如何在Adobe Experience Platform UI中使用模板来加速B2B数据的数据摄取过程。
title: 在 UI 中使用模板创建源数据流
badge1: Beta 版
exl-id: 48aa36ca-656d-4b9d-954c-48c8da9df1e9
source-git-commit: f9e3c19fdfd4ca0e03fdf3b3a7b5e82b72490dbc
workflow-type: tm+mt
source-wordcount: '2271'
ht-degree: 10%

---

# 在 UI 中使用模板创建源数据流 {#create-a-sources-dataflow-using-templates-in-the-ui}

>[!CONTEXTUALHELP]
>id="platform_sources_marketo_mapping"
>title="Experience Platform UI 中各种来源的模板"
>abstract="模板包括在将数据从来源引入到 Experience Platform 时可使用的自动生成的资源，如架构、数据集、身份标识、映射规则、身份标识命名空间和数据流。可更新自动生成的资源，以使自定义适合您的用例。"

>[!IMPORTANT]
>
>模板处于测试版，以下源支持这些模板：
>
>* [[!DNL Marketo Engage]](../../connectors/adobe-applications/marketo/marketo.md)
>* [[!DNL Microsoft Dynamics]](../../connectors/crm/ms-dynamics.md)
>* [[!DNL Salesforce]](../../connectors/crm/salesforce.md)
>
>文档和功能可能会发生更改。

Adobe Experience Platform提供了预配置的模板，您可以使用这些模板加快数据摄取过程。 模板包括自动生成的资源，例如架构、数据集、身份、映射规则、身份命名空间以及可在将数据从源引入Experience Platform时使用的数据流。

使用模板，您可以：

* 通过加快模板化资产的创建，减少引入的价值实现时间。
* 最大程度地减少手动数据摄取过程中可能发生的错误。
* 随时更新自动生成的资源以符合您的用例。

以下教程提供了有关如何在Experience Platform UI中使用模板的步骤。

## 开始使用

本教程需要对以下Experience Platform组件有一定的了解：

* [源](../../home.md)： Experience Platform允许从各种源摄取数据，同时让您能够使用Experience Platform服务来构建、标记和增强传入数据。
* [[!DNL Experience Data Model (XDM)] 系统](../../../xdm/home.md)： Experience Platform用于组织客户体验数据的标准化框架。
* [沙盒](../../../sandboxes/home.md)： Experience Platform提供了将单个Experience Platform实例划分为多个单独的虚拟环境的虚拟沙盒，以帮助开发和改进数字体验应用程序。

## 在 Experience Platform UI 中使用模板 {#use-templates-in-the-platform-ui}

>[!CONTEXTUALHELP]
>id="platform_sources_templates_accounttype"
>title="选择业务类型"
>abstract="为您的用例选择适当的业务类型。您的访问权限可能因 Real-Time Customer Data Platform 订阅帐户而异。"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html#" text="Real-Time CDP 概述"

在Experience Platform UI中，从左侧导航中选择&#x200B;**[!UICONTROL Sources]**&#x200B;以访问[!UICONTROL Sources]工作区，并查看Experience Platform中可用的源目录。

使用&#x200B;*[!UICONTROL Categories]*&#x200B;菜单按类别筛选源。 或者，在搜索栏中输入源名称，以从目录查找特定源。

转到[!UICONTROL Adobe applications]类别以查看[!DNL Marketo Engage]源卡，然后选择[!UICONTROL Add data]以开始。

![突出显示Marketo Engage源的源工作区的目录。](../../images/tutorials/templates/catalog.png)

此时会显示一个弹出窗口，为您提供浏览模板或使用现有架构和数据集的选项。

* **浏览模板**：源模板为您自动创建包含映射规则的架构、标识、数据集和数据流。 您可以根据需要自定义这些资源。
* **使用我的现有资源**：使用您创建的现有数据集和架构摄取您的数据。 如果需要，您还可以创建新数据集和架构。

>[!NOTE]
>
>使用需要更改数据捕获工作流或支持多个数据模型的源时，模板可以自动生成关系架构。 这些架构启用了Data Mirror的实时数据同步功能。\
>将模板与关系架构结合使用时，自动生成的资产将包含必需的主键、版本标识符和时间戳标识符字段。\
>有关详细信息，请参阅[Data Mirror概述](../../../xdm/data-mirror/overview.md)和[关系架构技术参考](../../../xdm/schema/relational.md)。

要使用自动生成的资源，请选择&#x200B;**[!UICONTROL Browse templates]**，然后选择&#x200B;**[!UICONTROL Select]**。

![一个弹出窗口，其中包含浏览模板或使用现有资源的选项。](../../images/tutorials/templates/browse-templates.png)

### 身份验证

此时将显示身份验证步骤，提示您创建新帐户或使用现有帐户。

>[!BEGINTABS]

>[!TAB 使用现有帐户]

要使用现有帐户，请选择[!UICONTROL Existing account]，然后从显示的列表中选择要使用的帐户。

![现有帐户的选择页面，其中包含您可以访问的现有帐户列表。](../../images/tutorials/templates/existing-account.png)

>[!TAB 创建新帐户]

要创建新帐户，请选择&#x200B;**[!UICONTROL New account]**，然后提供源连接详细信息和帐户身份验证凭据。 完成后，选择&#x200B;**[!UICONTROL Connect to source]**&#x200B;并留出一些时间来建立新连接。

![具有源连接详细信息和帐户身份验证凭据的新帐户的身份验证页面。](../../images/tutorials/templates/new-account.png)

>[!ENDTABS]

### 选择模板

经过帐户身份验证后，您现在可以选择要用于数据流的模板。

+++[!DNL Marketo Engage]模板
下表概述了[!DNL Marketo Engage]源可用的模板。

| [!DNL Marketo Engage]模板 | 描述 |
| --- | --- |
| 活动 | 活动模板可捕获活动（如电子邮件交互、网站交互和销售呼叫）的基于事件的快照。 |
| 公司 | 公司模板可捕获业务帐户详细信息，如公司公司财务信息、位置和账单信息。 |
| 指定帐户 | “指定帐户”模板可捕获已确定为要跟踪的目标帐户的详细信息。 |
| 机会 | Opportunities模板可捕获业务机会详细信息，如类型、销售阶段和相关帐户。 |
| 机会联系人角色 | Opportunity Contact Roles模板可捕获与特定机会关联的潜在客户的角色的详细信息。 |
| 人员 | “人员”模板可捕获个别人员的属性，如人口统计详细信息、联系信息和同意首选项。 |
| 计划成员资格 | 计划成员资格模板可捕获与商业营销活动关联的联系人的详细信息，包括培养节奏和联系人回复。 |
| 项目 | 项目模板可捕获商业营销活动详细信息，如状态、渠道、时间表和成本。 |
| 静态列表成员资格 | 静态列表成员资格模板捕获人员与其静态列表中的成员资格之间的关系。 |
| 静态列表 | 静态列表模板可捕获特定用例的实例化人员列表。 |

{style="table-layout:auto"}

+++

+++[!DNL Salesforce]个B2B模板
下表概述可用于[!DNL Salesforce]源的B2B模板。

| [!DNL Salesforce]个B2B模板 | 描述 |
| --- | --- |
| 帐户联系人关系 | 帐户联系人关系模板可捕获联系人与一个或多个帐户之间的关系。 |
| 帐户 | Account模板可捕获业务帐户详细信息，如公司财务信息、位置和账单信息。 |
| 营销活动成员 | 营销活动成员模板捕获单个潜在客户或联系人与特定[!DNL Salesforce]营销活动之间的关系。 |
| 营销活动 | 营销活动模板可捕获业务帐户详细信息，如公司财务信息、位置和账单信息。 |
| 联系人 | Contact模板可捕获联系人的属性，如人口统计信息、联系人信息和相关业务实体。 |
| 潜在客户 | 商机模板捕获商机的属性，如人口统计详细信息、联系信息和相关业务实体。 |
| 机会 | Opportunities模板可捕获业务机会详细信息，如类型、销售阶段和相关帐户。 |
| 机会联系人角色 | Opportunity Contact Roles模板可捕获与特定机会关联的潜在客户的角色的详细信息。 |

{style="table-layout:auto"}

+++

+++[!DNL Salesforce]个B2C模板
下表概述可用于[!DNL Salesforce]源的B2C模板。

| [!DNL Salesforce]个B2C模板 | 描述 |
| --- | --- |
| 联系人 | Contact模板可捕获联系人的属性，如人口统计信息、联系人信息和相关业务实体。 |
| 潜在客户 | 商机模板捕获商机的属性，如人口统计详细信息、联系信息和相关业务实体。 |

{style="table-layout:auto"}

+++

+++[!DNL Microsoft Dynamics]个B2B模板
下表概述可用于[!DNL Microsoft Dynamics]源的B2B模板。

| [!DNL Microsoft Dynamics]个B2B模板 | 描述 |
| --- | --- |
| 帐户 | Account模板可捕获业务帐户详细信息，如公司财务信息、位置和账单信息。 |
| 营销活动 | 营销活动模板可捕获业务帐户详细信息，如公司财务信息、位置和账单信息。 |
| 联系人 | Contact模板可捕获联系人的属性，如人口统计信息、联系人信息和相关业务实体。 |
| 潜在客户 | 商机模板捕获商机的属性，如人口统计详细信息、联系信息和相关业务实体。 |
| 营销列表 | 营销列表模板可捕获为营销活动或其他销售目的创建的一组现有或潜在客户。 |
| 营销列表成员 | 营销列表成员可捕获营销列表中任何一种客户记录类型的详细信息，例如潜在客户、客户或联系人。 |
| 机会 | Opportunities模板可捕获业务机会详细信息，如类型、销售阶段和相关帐户。 |
| 机会联系人角色 | Opportunity Contact Roles模板可捕获与特定机会关联的潜在客户的角色的详细信息。 |

{style="table-layout:auto"}

+++

+++[!DNL Microsoft Dynamics]个B2C模板
下表概述可用于[!DNL Microsoft Dynamics]源的B2C模板。

| [!DNL Microsoft Dynamics]个B2C模板 | 描述 |
| --- | --- |
| 联系人 | Contact模板可捕获联系人的属性，如人口统计信息、联系人信息和相关业务实体。 |
| 潜在客户 | 商机模板捕获商机的属性，如人口统计详细信息、联系信息和相关业务实体。 |

{style="table-layout:auto"}

+++

根据您选择的业务类型，将显示模板列表。 选择模板名称旁边的预览图标![预览图标](/help/images/icons/preview.png)以预览模板中的示例数据。

![突出显示预览图标的模板列表。](../../images/tutorials/templates/templates.png)

此时将显示预览窗口，允许您浏览并检查模板中的示例数据。 完成后，选择&#x200B;**[!UICONTROL Got it]**。

![预览示例数据窗口。](../../images/tutorials/templates/preview-sample-data.png)

接下来，从列表中选择要使用的模板。 您可以选择多个模板并一次创建多个数据流。 但是，每个帐户只能使用一次模板。 选择模板后，请选择&#x200B;**[!UICONTROL Finish]**&#x200B;并等待一段时间以生成资产。

如果从可用模板列表中选择一个或多个项目，则仍将生成所有B2B架构和身份命名空间，以确保正确配置架构之间的B2B关系。

>[!NOTE]
>
>已使用的模板将从选择中禁用。

![已选择具有机会联系人角色模板的模板列表。](../../images/tutorials/templates/select-template.png)

### 设置计划

[!DNL Microsoft Dynamics]和[!DNL Salesforce]源都支持计划数据流。

使用计划界面配置数据流的摄取计划。 将您的摄取频率设置为&#x200B;**一次**&#x200B;以创建一次性摄取。

![Dynamics和Salesforce模板的计划界面。](../../images/tutorials/templates/schedule.png)

或者，您也可以将摄取频率设置为&#x200B;**分钟**、**小时**、**天**&#x200B;或&#x200B;**周**。 如果计划数据流以进行多次摄取，则必须设置时间间隔以在每次摄取之间建立一个时间范围。 例如，摄取频率设置为&#x200B;**小时**，间隔设置为&#x200B;**15**&#x200B;意味着您的数据流计划每&#x200B;**15小时**&#x200B;摄取一次数据。

在此步骤中，您还可以启用&#x200B;**回填**&#x200B;并为增量数据摄取定义列。 回填用于摄取历史数据，而您为增量摄取定义的列允许从现有数据中区分新数据。

完成摄取计划的配置后，请选择&#x200B;**[!UICONTROL Finish]**。

![已启用回填的Dynamics和Salesforce模板的计划界面。](../../images/tutorials/templates/backfill.png)

### 查看资源 {#review-assets}

>[!CONTEXTUALHELP]
>id="platform_sources_templates_review"
>title="查看自动生成的资产"
>abstract="生成所有资产最多需要五分钟时间。如果您选择离开页面，在生成完资产后，将向您发送通知以返回页面。您可以在资产生成后查看资产，并随时对数据流进行其他配置。"

[!UICONTROL Review template assets]页面将显示作为模板的一部分自动生成的资源。 在此页中，可以查看与源连接关联的自动生成的架构、数据集、身份命名空间和数据流。 生成所有资产最多需要五分钟时间。如果您选择离开页面，在生成完资产后，将向您发送通知以返回页面。您可以在资产生成后查看资产，并随时对数据流进行其他配置。

默认情况下，自动生成的数据流设置为草稿状态，以允许对配置进行进一步自定义，如映射规则或计划频率。 选择数据流名称旁边的省略号(`...`)，然后选择&#x200B;**[!UICONTROL Preview mappings]**&#x200B;以查看为草稿数据流创建的映射集。

![已选择预览映射选项的下拉窗口。](../../images/tutorials/templates/preview.png)

此时将显示一个预览页面，允许您检查源数据字段与目标架构字段之间的映射关系。 查看数据流的映射后。 选择&#x200B;**[!UICONTROL Got it.]**

![映射预览窗口。](../../images/tutorials/templates/preview-mappings.png)

在执行之后，您可以随时更新数据流。 选择数据流名称旁边的省略号(`...`)，然后选择&#x200B;**[!UICONTROL Update dataflow]**。 您将转到源工作流页面，可以在其中更新数据流详细信息，包括部分摄取、错误诊断和警报通知的设置以及数据流的映射。

您可以使用架构编辑器视图对自动生成的架构进行更新。 有关详细信息，请访问[上的使用架构编辑器](../../../xdm/tutorials/create-schema-ui.md)的指南。

![已选择更新数据流选项的下拉窗口。](../../images/tutorials/templates/update.png)

>[!TIP]
>
>您可以通过源工作区中的[!UICONTROL Dataflows]目录页面访问草稿数据流。 从顶部标题中选择&#x200B;**[!UICONTROL Dataflows]**，然后从列表中选择要更新的数据流。
>
>![源工作区数据流目录中的现有数据流列表。](../../images/tutorials/templates/dataflows.png)

### 发布数据流

通过浏览源工作流开始发布流程。 选择[!UICONTROL Update dataflow]后，您将进入工作流的&#x200B;*[!UICONTROL Add data]*&#x200B;步骤。 选择&#x200B;**[!UICONTROL Next]**&#x200B;以继续。

![为草稿数据流添加数据步骤](../../images/tutorials/templates/continue-draft.png)

接下来，确认数据流详细信息，并配置错误诊断、部分摄取和警报通知的设置。 完成后，选择&#x200B;**[!UICONTROL Next]**。

![草稿数据流的数据流详细信息步骤。](../../images/tutorials/templates/dataflow-detail.png)

>[!NOTE]
>
>您可以随时选择&#x200B;**[!UICONTROL Save as draft]**&#x200B;以停止并保存您对数据流所做的更改。

此时将显示映射步骤。 在此步骤中，您可以重新配置数据流的映射配置。 有关用于映射的数据准备功能的综合指南，请访问[数据准备UI指南](../../../data-prep/ui/mapping.md)。

![草稿数据流的映射步骤。](../../images/tutorials/templates/mapping.png)

最后，查看数据流的详细信息，然后选择&#x200B;**[!UICONTROL Save & ingest]**&#x200B;以发布草稿。

![草稿数据流的审核步骤。](../../images/tutorials/templates/review.png)

## 后续步骤

通过学习本教程，您现在已使用模板创建数据流以及架构、数据集和身份命名空间等资产。 有关源的一般信息，请访问[源概述](../../home.md)。

## 警报和通知 {#alerts-and-notifications}

Adobe Experience Platform警报支持模板，您可以使用通知面板接收有关资源状态的更新，并导航回审核页面。

选择Experience Platform UI顶部标题中的通知图标，然后选择状态警报以查看要审阅的资源。

![高亮显示Experience Platform UI中通知面板，其中包含用于警报失败数据流的通知。](../../images/tutorials/templates/notifications.png)

您可以更新模板的警报设置，以接收有关数据流状态的电子邮件和Experience Platform内通知。 有关配置警报的更多信息，请阅读有关[如何订阅源数据流的警报](../ui/alerts.md)的指南。