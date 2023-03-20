---
keywords: Experience Platform；主页；热门主题；数据管理；数据使用策略用户指南
solution: Experience Platform
title: 在UI中管理数据使用策略
description: Adobe Experience Platform Data Governance提供了一个用户界面，允许您创建和管理数据使用策略。 本文档概述了可在策略工作区中通过Experience Platform用户界面执行的操作。
exl-id: 29434dc1-02c2-4267-a1f1-9f73833e76a0
source-git-commit: e539b1e165227d9a888bfe12d8205e285b3ce259
workflow-type: tm+mt
source-wordcount: '1413'
ht-degree: 7%

---

# 在UI中管理数据使用策略 {#user-guide}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_dataUsagePolicies_description"
>title="描述"
>abstract=""

本文档介绍如何使用 **[!UICONTROL 策略]** 工作区，以创建和管理数据使用策略。

>[!NOTE]
>
>有关如何在UI中管理访问控制策略的信息，请参阅 [基于属性的访问控制UI指南](../../access-control/abac/ui/policies.md) 中。

>[!IMPORTANT]
>
>默认情况下，所有数据使用策略(包括由Adobe提供的核心策略)都处于禁用状态。 要考虑实施单个策略，必须手动启用该策略。 请参阅 [启用策略](#enable) 以了解有关如何在UI中执行此操作的步骤。

## 先决条件

本指南需要对以下内容有一定的了解 [!DNL Experience Platform] 概念：

* [数据管理](../home.md)
* [数据使用策略](./overview.md)

## 查看现有策略 {#view-policies}

在 [!DNL Experience Platform] UI，选择 **[!UICONTROL 策略]** 打开 **[!UICONTROL 策略]** 工作区。 在 **[!UICONTROL 浏览]** 选项卡，您可以看到可用策略的列表，包括其关联的标签、营销操作和状态。

![](../images/policies/browse-policies.png)

如果您有权访问同意策略，请选择 **[!UICONTROL 同意策略]** 切换到在 [!UICONTROL 浏览] 选项卡。

![](../images/policies/consent-policy-toggle.png)

选择列出的策略以查看其描述和类型。 如果选择了自定义策略，则会显示其他控件以编辑、删除或 [启用/禁用策略](#enable).

![](../images/policies/policy-details.png)

## 创建自定义策略 {#create-policy}

要创建新的自定义数据使用策略，请选择 **[!UICONTROL 创建策略]** 的右上角 **[!UICONTROL 浏览]** 选项卡 **[!UICONTROL 策略]** 工作区。

![](../images/policies/create-policy-button.png)

根据您是否属于同意策略测试版，会出现以下情况之一：

* 如果您不是测试版的一部分，则会立即将您带到 [创建数据管理策略](#create-governance-policy).
* 如果您是测试版的一部分，则对话框会为 [创建同意策略](#consent-policy).
   ![](../images/policies/choose-policy-type.png)

### 创建数据管理策略 {#create-governance-policy}

的 **[!UICONTROL 创建策略]** 工作流。 首先，为新策略提供名称和描述。

![](../images/policies/create-policy-description.png)

接下来，选择策略所基于的数据使用标签。 选择多个标签时，您可以选择数据应包含所有标签还是仅包含其中一个标签，以便策略应用。 选择 **[!UICONTROL 下一个]** 完成。

![](../images/policies/add-labels.png)

的 **[!UICONTROL 选择营销操作]** 中。 从提供的列表中选择相应的营销操作，然后选择 **[!UICONTROL 下一个]** 继续。

>[!NOTE]
>
>选择多个营销操作时，策略会将其解释为“OR”规则。 换言之，该政策适用于 **any** 中，将执行选定的营销操作。

![](../images/policies/add-marketing-actions.png)

的 **[!UICONTROL 审阅]** 步骤，允许您在创建新策略之前查看新策略的详细信息。 满意后，选择 **[!UICONTROL 完成]** 创建策略。

![](../images/policies/policy-review.png)

的 **[!UICONTROL 浏览]** 选项卡，该选项卡现在会列出新创建的“草稿”状态策略。 要启用策略，请参阅下一节。

![](../images/policies/created-policy.png)

### 创建同意策略 {#consent-policy}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_dataUsagePolicies_instructions"
>title="说明"
>abstract=""

>[!IMPORTANT]
>
>同意策略仅适用于已购买的组织 **Adobe医疗保健盾** 或 **Adobe隐私和安全防护**.

如果选择创建同意策略，则会显示一个新屏幕，用于配置新策略。

![](../images/policies/consent-policy-dialog.png)

要使用同意策略，您的配置文件数据中必须存在同意属性。 请参阅 [同意处理Experience Platform](../../landing/governance-privacy-security/consent/adobe/overview.md) 有关如何在并集架构中包含所需属性的详细步骤。

同意策略由两个逻辑组件组成：

* **[!UICONTROL 如果]**:将触发策略检查的条件。 这可以基于正在执行的特定营销操作、存在特定数据使用标签，或两者的组合。
* **[!UICONTROL 然后]**:要将用户档案包含在触发策略的操作中，必须存在的同意属性。

#### 配置条件 {#consent-conditions}

>[!CONTEXTUALHELP]
>id="platform_governance_policies_consentif"
>title="“如果”条件"
>abstract="首先定义会触发策略检查的条件。条件可以包括正在采取的某些营销行动、存在的某些数据治理标签，或两者的组合。"

在 **[!UICONTROL 如果]** 部分，选择应触发此策略的营销操作和/或数据使用标签。 选择 **[!UICONTROL 查看全部]** 和 **[!UICONTROL 选择标签]** 查看可用营销操作和标签的完整列表。

添加至少一个条件后，您可以选择 **[!UICONTROL 添加条件]** 要继续根据需要添加其他条件，请从下拉菜单中选择相应的条件类型。

![](../images/policies/add-condition.png)

如果选择多个条件，则可以使用它们之间显示的图标来切换“AND”和“OR”之间的条件关系。

![](../images/policies/and-or-selection.png)

#### 选择同意属性 {#consent-attributes}

>[!CONTEXTUALHELP]
>id="platform_governance_policies_consentthen"
>title="“则”条件"
>abstract="定义“如果”条件后，使用“则”部分从联合架构中选择至少一个同意属性。这是必须存在的属性，以便配置文件包含在此策略所控制的操作中。"

在 **[!UICONTROL 然后]** 部分，从并集架构中至少选择一个同意属性。 这是必须存在的属性，以便配置文件包含在此策略所控制的操作中。您可以从列表中选择一个提供的选项，或选择 **[!UICONTROL 查看全部]** 直接从并集架构中选择属性。

选择同意属性时，请选择您希望此策略检查的属性值。

![](../images/policies/select-schema-field.png)

在您至少选择了一个同意属性后， **[!UICONTROL 策略属性]** 面板更新以显示根据此策略允许的预计用户档案数，包括用户档案存储总数的百分比。 此估计会在您调整策略配置时自动更新。

![](../images/policies/audience-preview.png)

要向策略添加其他同意属性，请选择 **[!UICONTROL 添加结果]**.

![](../images/policies/add-result.png)

您可以根据需要继续向策略添加和调整条件和同意属性。 如果您对配置满意，请在选择 **[!UICONTROL 保存]**.

![](../images/policies/name-and-save.png)

现在将创建同意策略，其状态将设置为 [!UICONTROL 已禁用] 默认情况下。 要立即启用策略，请选择 **[!UICONTROL 状态]** 在右边栏中切换。

![](../images/policies/enable-consent-policy.png)

#### 验证策略实施

创建并启用同意策略后，您可以在将区段激活到目标时，预览该策略对您同意的受众有何影响。 请参阅 [同意策略评估](../enforcement/auto-enforcement.md#consent-policy-evaluation) 以了解更多信息。

## 启用或禁用策略 {#enable}

默认情况下，所有数据使用策略(包括由Adobe提供的核心策略)都处于禁用状态。 要考虑实施单个策略，您必须通过API或UI手动启用该策略。

您可以在 **[!UICONTROL 浏览]** 选项卡 **[!UICONTROL 策略]** 工作区。 从列表中选择自定义策略以在右侧显示其详细信息。 在 **[!UICONTROL 状态]**，选择切换按钮以启用或禁用策略。

![](../images/policies/enable-policy.png)

## 查看营销操作 {#view-marketing-actions}

在 **[!UICONTROL 策略]** 工作区中，选择 **[!UICONTROL 营销操作]** 选项卡，查看由Adobe和您自己的组织定义的可用营销操作列表。

![](../images/policies/marketing-actions.png)

## 创建营销操作 {#create-marketing-action}

要创建新的自定义营销操作，请选择 **[!UICONTROL 创建营销操作]** 的右上角 **[!UICONTROL 营销操作]** 选项卡 **[!UICONTROL 策略]** 工作区。

![](../images/policies/create-marketing-action.png)

的 **[!UICONTROL 创建营销操作]** 对话框。 输入营销操作的名称和描述，然后选择 **[!UICONTROL 创建]**.

![](../images/policies/create-marketing-action-details.png)

新创建的操作将显示在 **[!UICONTROL 营销操作]** 选项卡。 现在，您可以在 [创建新的数据使用策略](#create-policy).

![](../images/policies/created-marketing-action.png)

## 编辑或删除营销操作 {#edit-delete-marketing-action}

>[!NOTE]
>
>只能编辑由您的组织定义的自定义营销操作。 无法更改或删除由Adobe定义的营销操作。

在 **[!UICONTROL 策略]** 工作区中，选择 **[!UICONTROL 营销操作]** 选项卡，查看由Adobe和您自己的组织定义的可用营销操作列表。 从列表中选择自定义营销操作，然后使用右侧部分中提供的字段来编辑营销操作的详细信息。

![](../images/policies/edit-marketing-action.png)

如果任何现有的使用策略未使用营销操作，则可以通过选择 **[!UICONTROL 删除营销操作]**.

>[!NOTE]
>
>尝试删除现有策略正在使用的营销操作时，会显示一条错误消息，指示删除尝试失败。

![](../images/policies/delete-marketing-action.png)

## 后续步骤

本文档概述了如何在 [!DNL Experience Platform] UI。 有关如何使用 [!DNL Policy Service API]，请参阅 [开发人员指南](../api/getting-started.md). 有关如何实施数据使用策略的信息，请参阅 [策略实施概述](../enforcement/overview.md).

以下视频演示了如何在 [!DNL Experience Platform] UI:

>[!VIDEO](https://video.tv.adobe.com/v/32977?quality=12&learn=on)
