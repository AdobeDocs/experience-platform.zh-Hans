---
solution: Experience Platform
title: 了解如何使用AI助手创作和共享您自己的行动手册。
description: 如何创作和共享您自己的用例行动手册。
role: User
exl-id: 0bc49710-ad9e-4509-b7e6-55f9b9037aa9
source-git-commit: 5cdbc160369a146da3ae8ca39d8c3095887e03b5
workflow-type: tm+mt
source-wordcount: '1803'
ht-degree: 0%

---


# 创作并共享您自己的行动手册(Beta)

[!DNL Playbook Authoring Framework]由Adobe Experience Platform中的AI Assistant提供支持，允许您在Adobe Experience Platform中高效地创建、管理和共享行动手册。

该框架遵循三步流程：

1. **元数据捕获**：使用AI助手或Web窗体捕获行动手册元数据。

2. **技术关联**：将历程或受众等特定技术资产添加到行动手册。 您可以保留对开发沙盒中行动手册创建过程的完全控制权，确保与架构和其他独特数据结构保持一致。

3. **行动手册分发**：跨不同组织共享行动手册。 例如，ACME位于德国的Martech Center of Excellence可以制定一份“黄金”行动手册，并将其分发给泰国、澳大利亚等国的地区组织。 帮助标准化营销用例。

## 创建行动手册

您可以通过两种方式创建行动手册：使用AI助手或手动。 请阅读以下部分，了解如何使用AI助手创建行动手册。

### 行动手册概述

按照以下步骤使用AI助手创建行动手册：

在左侧导航面板中，选择&#x200B;**[!UICONTROL 行动手册]**。

![左侧导航面板中突出显示“行动手册”选项的Platform UI。](/help/use-case-playbooks/assets/playbooks/authoring/playbooks.png)

选择&#x200B;**[!UICONTROL 新建行动手册]**，然后选择&#x200B;**使用AI助手生成行动手册**。

![已选择“使用AI助手生成行动手册”选项的行动手册创建界面。](/help/use-case-playbooks/assets/playbooks/authoring/generate-playbook.png)

使用提示字段描述用例。 例如：

“与浏览跑步鞋但未完成购买的ACME客户接洽。”

![行动手册创建界面突出显示Web窗体区域，用户可以在该区域输入提示。](/help/use-case-playbooks/assets/playbooks/authoring/prompt.png)

选择&#x200B;**[!UICONTROL 生成]**&#x200B;以创建行动手册元数据。

![在提示区显示“生成”按钮的Playbook创建界面中突出显示。](/help/use-case-playbooks/assets/playbooks/authoring/generate.png)

生成后，选择&#x200B;**[!UICONTROL 编辑]**&#x200B;以根据需要修改生成的标题、描述和元数据。

![生成的、突出显示“编辑”按钮的行动手册，允许用户修改元数据。](/help/use-case-playbooks/assets/playbooks/authoring/edit.png)

为确保数据工程师拥有设置用例所需的所有详细信息，请填写&#x200B;**[!UICONTROL 行动手册详细信息]**&#x200B;部分。 虽然这些字段是可选的，但它们有助于捕获关键信息，使得连接正确的技术组件更加容易。 选择&#x200B;**[!UICONTROL 编辑]**&#x200B;以向以下字段添加值：

* **行业**
* **目标受众**
* **营销渠道**

![突出显示带有“编辑”按钮的行动手册详细信息部分，以便您添加或修改行业、目标受众和营销渠道等详细信息。](/help/use-case-playbooks/assets/playbooks/authoring/edit-details.png)

生成元数据后，选择&#x200B;**[!UICONTROL 编辑历程图]**&#x200B;以根据需要调整历程图中的步骤。

![用于修改历程图步骤的“编辑历程图”按钮。](/help/use-case-playbooks/assets/playbooks/authoring/edit-journey-map-button.png)

![历程图编辑器界面，这样您就可以在捕获行动手册元数据后调整步骤。](/help/use-case-playbooks/assets/playbooks/authoring/edit-journey-map.png)

然后，继续将剧本与技术资产相关联。 要手动创建行动手册，请选择&#x200B;**[!UICONTROL 手动创建行动手册]**。

![使用“手动创建行动手册”选项，从空白模板启动行动手册。](/help/use-case-playbooks/assets/playbooks/authoring/create-manually.png)

出现一个空白剧本模板。 填写详细信息，如&#x200B;**标题**&#x200B;和&#x200B;**描述**。 您还可以编辑历程图以根据需要添加事件和接触点。

## 将行动手册与技术资产关联

无论您是手动创建行动手册，还是使用AI助手创建行动手册，都必须将其与所需的技术资产相关联。 导航到&#x200B;**[!UICONTROL 技术Assets]**&#x200B;选项卡，然后选择所需的产品。 对于此示例，请选择&#x200B;**[!UICONTROL Journey Optimizer]**。

>[!NOTE]
>
> 未来版本中将添加对Real-Time CDP的支持。

![突出显示了“技术Assets”选项卡，其中显示“添加所需产品”按钮，可使用它将技术资产与行动手册关联。](/help/use-case-playbooks/assets/playbooks/authoring/technical-assets-add-required-product.png)

选择&#x200B;**[!UICONTROL 选择资产]**&#x200B;以将此剧本与历程关联，如下图所示。 然后选择&#x200B;**发布行动手册**&#x200B;以完成行动手册。

![突出显示带有“选择资源”按钮的“技术Assets”选项卡，您可以使用它将历程与行动手册关联。](/help/use-case-playbooks/assets/playbooks/authoring/select-assets.png)

![选择历程以将其与行动手册关联。](/help/use-case-playbooks/assets/playbooks/authoring/journey.png)

发布后，行动手册会自动提取和关联历程的模式和受众详细信息。

![已发布的行动手册，其中显示元数据和关联的技术资源。](/help/use-case-playbooks/assets/playbooks/authoring/publish-playbook.png)

所有创建的行动手册都可在&#x200B;**您的行动手册**&#x200B;选项卡中找到。

![“您的行动手册”选项卡显示已创建的行动手册列表。](/help/use-case-playbooks/assets/playbooks/authoring/your-playbooks-tab.png)

您可以从目录中选择任何行动手册，以创建实例以供重用。 请参阅文档以[了解如何创建实例](/help/use-case-playbooks/playbooks/create-share-reuse.md)。

![突出显示了“创建实例”选项的“行动手册概述”选项卡。](/help/use-case-playbooks/assets/playbooks/authoring/create-instance.png)

>[!NOTE]
>
> 剧本发布后，便无法编辑。 要进行更改，请删除剧本，然后重新开始。

## 示例提示

AI Assistant可以处理各种提示结构和提取关键细节，同时过滤掉不必要的信息。 以下是用户提示的一些示例以及系统如何解读它们。

**示例1：**

创建标题为“Complete the Look”的营销活动以提高销售额和CLV。 此活动鼓励购买厨具或家具的客户通过与购买相关的个性化推荐和优惠完成补充购买。 第一个消息是向客户提供产品推荐。 如果他们在7天内未进行任何购买，则会收到第二条消息，其中包含产品建议和选件。 使用推送通知和电子邮件联系客户。 定位过去7天在厨具或家具类别中购买过，且过去30天内未成为目标的客户。 作为营销活动的一部分，我们希望测量KPI，例如点击次数（电子邮件、应用程序、短信、推送）、CTR、电子钱包CTR、AOV转化。CLV收入、总购买事件（店内、数字、呼叫中心）。”

![在文本输入框中输入长提示以生成行动手册的示例。](/help/use-case-playbooks/assets/playbooks/authoring/long-prompt.png)

**示例2：**

“项目名称：时尚新闻稿
背景： （主动解决或解决问题）：旨在向订阅了新闻稿通信的ACME客户发送时尚新闻稿的历程。
目标：向订阅了通信的ACME客户发送时尚新闻稿电子邮件。
促销详细信息：客户每周通过电子邮件渠道接收时尚新闻。 电子邮件应基于性别、语言和市场进行个性化和内容变化。
项目渠道/接触点：电子邮件
目标受众：已订阅ACME时尚新闻稿通信的客户。
目标KPI/参与量度/ROI：1。 增加来自产品之收益。 2.提高客户忠诚度。”

![在文本输入框中输入有条理的列表样式提示以生成行动手册的示例。](/help/use-case-playbooks/assets/playbooks/authoring/organized-list-prompt.png)

**示例3：**

“在正在进行的产品促销活动中，鼓励消费者购买产品。
通过电子邮件、短信或推送通知发送适当的通信内容来购买产品，从而在持续促销期间与购物者互动。 在他们24小时没有参与促销活动后，向他们发送提醒电子邮件。”

![在文本输入框中输入用于生成行动手册的简要提示示例。](/help/use-case-playbooks/assets/playbooks/authoring/concise-prompt.png)

**示例4：**

“卖鞋给高中生。”

![在文本输入框中输入的一行提示用于生成行动手册的示例。](/help/use-case-playbooks/assets/playbooks/authoring/one-liner-prompt.png)

AI助手会删除所有不必要的详细信息，如“项目名称”或“背景”。 它可提取“目标受众”、“营销目标”和“营销渠道”等关键元素，并可与任何输入样式配合使用。

这些示例演示了AI如何从用户提示中优化和提取基本详细信息。

>[!NOTE]
>
> 在编写提示时避免使用任何PII或显式单词。

## 内容准则和审核

在创建行动手册时，请注意包括的语言和内容。 行动手册在整个组织中可见，以及用户标记的任何攻击性或不适当的内容。

### 标记和审阅流程

如果行动手册包含不适当或冒犯性的内容，Adobe会自动收到报告以供审核。 Adobe会审查标记的内容，在认为不合适时通知客户，并删除剧本。

## 在沙盒之间共享行动手册 {#share-playbooks-sandboxes}

在一个沙盒中创建和发布行动手册时，该行动手册会自动在您组织内的所有沙盒中可用。 此功能消除了对手动共享的需求，并允许您在任何其他沙盒中无缝创建行动手册的实例。

>[!TIP]
>
>如果行动手册引用的字段在目标沙盒的合并架构中不可用，或者如果您缺乏必要的权限，则在尝试创建实例时会显示一条错误消息。 消息指定缺少的字段和/或权限。

如果合并架构中缺少任何字段，则在导入期间会有一个对话框突出显示它们。

![在行动手册导入过程中列出合并架构中缺少的字段的对话框。](/help/use-case-playbooks/assets/playbooks/authoring/missing-fields.png)

## 在组织间共享您的行动手册 {#sharing-playbooks-organizations}

在多个团队需要遵循相同的最佳实践时，跨组织共享行动手册有助于确保一致性和效率。 要在组织之间共享行动手册，请执行以下步骤：

1. **登录到源组织**：从&#x200B;**[!UICONTROL 您的行动手册]**&#x200B;选项卡导航到包含您创建的行动手册并要共享的组织。
2. **发布行动手册**：如果行动手册尚未发布，则必须在共享之前发布。

   >[!NOTE]
   >
   >必须在源组织和目标组织之间建立合作伙伴关系，以实现行动手册共享。 了解如何[创建组织伙伴关系请求](/help/sandboxes/ui/sharing-packages-across-orgs.md#create-an-organization-partnership-request)。

3. **启动共享**：发布行动手册并建立伙伴关系后，选择&#x200B;**[!UICONTROL 共享行动手册]**。
4. **选择目标组织**：在出现提示时，选择要与你共享行动手册的组织。
5. **确认并共享**：确认您的选择。 您将收到指示已成功共享的确认消息。
6. **验证目标组织**：登录目标组织以验证行动手册是否可用。
7. **导入行动手册**：选择&#x200B;**[!UICONTROL 导入]**&#x200B;以将行动手册导入目标组织。 您可以在&#x200B;**行动手册**&#x200B;选项卡中查看它。

如果未显示行动手册，请确保已发布行动手册并且组织伙伴关系处于活动状态。

>[!IMPORTANT]
>
>不支持可传递的行动手册共享。 如果您将行动手册从一个组织共享到另一个组织，然后导入该行动手册，则它无法再次从接收组织共享到第三个组织。

## 所需的权限 {#required-permissions}

要访问沙盒并使用此功能，您需要以下权限：

### 沙盒权限

要访问存在该功能的沙盒环境，需要以下权限：

* **管理沙盒**
* **查看沙盒**

* **包共享权限**：

内部共享功能需要以下权限：

* [**管理包**](/help/sandboxes/ui/sandbox-tooling.md)
* [**共享包**](/help/sandboxes/ui/sharing-packages-across-orgs.md)

使用这些权限可以：

* 输入沙盒环境
* 访问沙盒中的功能
* 根据需要管理和共享包

这些权限位于权限列表的&#x200B;**[!UICONTROL 沙盒]**&#x200B;部分中。

![突出显示具有管理和共享行动手册相关权限的权限列表。](/help/use-case-playbooks/assets/playbooks/authoring/permissions.png)

### 历程和相关对象 — 权限

在构建使用行动手册的历程时，您可能引用其他对象，如&#x200B;**渠道**、**受众**&#x200B;和其他实体。 每个对象都有自己的权限集。

这些是与历程相关的操作的关键权限，例如：

* **查看历程**
* **管理历程**
* 与受众和渠道等对象相关的权限

您还需要以下受众权限：

* **区段读取**
* **个人资料读取**
* **数据集读取**

由于历程非常灵活，并且可能涉及许多互连的对象，因此它们的[完全权限](https://experienceleague.adobe.com/zh-hans/docs/journey-optimizer/using/access-control/privacy/high-low-permissions)将单独进行记录，并且可能会因您的特定用例而有所不同。

## 后续步骤

现在您已了解如何使用AI助手创建、发布和共享行动手册，了解如何开始使用可用的行动手册，并从[行动手册列表](/help/use-case-playbooks/playbooks/choose.md)为您的用例选择正确的行动手册。