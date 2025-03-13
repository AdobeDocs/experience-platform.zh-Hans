---
solution: Experience Platform
title: 了解如何使用AI助手创作和共享您自己的行动手册。
description: 如何创作和共享您自己的用例行动手册。
role: User
exl-id: 0bc49710-ad9e-4509-b7e6-55f9b9037aa9
source-git-commit: f76db5c8d397c6c7b006c70147c054dc0a67be04
workflow-type: tm+mt
source-wordcount: '1112'
ht-degree: 0%

---

# 创作并共享您自己的行动手册

[!DNL Playbook Authoring Framework]由Adobe Experience Platform中的AI Assistant提供支持，允许您在Adobe Experience Platform中高效地创建、管理和共享行动手册。

该框架遵循三步流程：

1. **元数据捕获**：使用AI助手或[Web窗体]捕获行动手册元数据。

2. **技术关联**：将历程或受众等特定技术资产添加到行动手册。 您可以保留对开发沙盒中行动手册创建过程的完全控制权，确保与架构和其他独特数据结构保持一致。

3. **行动手册分发**：跨不同组织共享行动手册。 例如，ACME位于德国的Martech Center of Excellence可以制定一份“黄金”行动手册，并将其分发给泰国、澳大利亚等国的地区组织。 帮助标准化营销用例。

## 创建行动手册

您可以通过两种方式创建行动手册：使用AI助手或手动。 请阅读以下部分以了解如何操作。

### 行动手册概述

按照以下步骤使用AI助手创建行动手册：

在左侧导航面板中，选择&#x200B;**[!UICONTROL 行动手册]**。

在UI的左侧导航窗格中突出显示![个“行动手册”。](/help/use-case-playbooks/assets/playbooks/authoring/playbooks.png)

选择&#x200B;**[!UICONTROL 新建行动手册]**，然后选择&#x200B;**使用AI助手生成行动手册**。

![选择了“使用AI助手生成行动手册”的行动手册界面。](/help/use-case-playbooks/assets/playbooks/authoring/generate-playbook.png)

在提示字段中，描述用例。

**示例**：“与浏览跑鞋但未完成购买的ACME客户接洽。”

![Web窗体区域突出显示的行动手册界面。](/help/use-case-playbooks/assets/playbooks/authoring/prompt.png)

选择&#x200B;**[!UICONTROL 生成]**&#x200B;以创建行动手册元数据。

![提示区域突出显示“生成”行动手册按钮。](/help/use-case-playbooks/assets/playbooks/authoring/generate.png)

生成后，选择&#x200B;**[!UICONTROL 编辑]**&#x200B;以根据需要修改生成的标题、描述和元数据。

![生成的、突出显示“编辑”按钮的行动手册。](/help/use-case-playbooks/assets/playbooks/authoring/edit.png)

为确保数据工程师拥有设置用例所需的所有详细信息，请填写&#x200B;**[!UICONTROL 行动手册详细信息]**&#x200B;部分。 虽然这些字段是可选的，但它们有助于捕获关键信息，使得连接正确的技术组件更加容易。 选择&#x200B;**[!UICONTROL 编辑]**&#x200B;以向以下字段添加值：

* **行业**
* **目标受众**
* **营销渠道**

![带有“编辑”按钮的剧本详细信息部分突出显示。](/help/use-case-playbooks/assets/playbooks/authoring/edit-details.png)

生成元数据后，选择&#x200B;**[!UICONTROL 编辑历程图]**&#x200B;以根据需要调整历程图中的步骤。

![编辑历程图按钮。](/help/use-case-playbooks/assets/playbooks/authoring/edit-journey-map-button.png)

![捕获行动手册元数据后编辑历程图。](/help/use-case-playbooks/assets/playbooks/authoring/edit-journey-map.png)

然后，继续将剧本与技术资产相关联。 要手动创建行动手册，请选择&#x200B;**[!UICONTROL 手动创建行动手册]**。

![手动创建行动手册](/help/use-case-playbooks/assets/playbooks/authoring/create-manually.png)

出现一个空白剧本模板。 填写详细信息，如&#x200B;**标题**&#x200B;和&#x200B;**描述**。 您还可以编辑历程图以根据需要添加事件和接触点。

## 将行动手册与技术资产关联

无论您是手动创建行动手册，还是使用AI助手创建行动手册，都必须将其与所需的技术资产相关联。 导航到&#x200B;**[!UICONTROL 技术Assets]**&#x200B;选项卡，然后选择所需的产品。 对于此示例，请选择&#x200B;**[!UICONTROL Journey Optimizer]**。

>[!NOTE]
>
> 未来版本中将添加对Real-Time CDP的支持。

![突出显示了“技术资产”选项卡和“添加所需产品”按钮。](/help/use-case-playbooks/assets/playbooks/authoring/technical-assets-add-required-product.png)

选择&#x200B;**[!UICONTROL 选择资产]**&#x200B;以将此剧本与历程关联，如下图所示。 然后选择&#x200B;**发布行动手册**&#x200B;以完成行动手册。

![“选择资源”按钮在“技术资源”选项卡上突出显示](/help/use-case-playbooks/assets/playbooks/authoring/select-assets.png)

![选择历程](/help/use-case-playbooks/assets/playbooks/authoring/journey.png)

发布后，行动手册会自动提取和关联历程的模式和受众详细信息。

![已发布的行动手册](/help/use-case-playbooks/assets/playbooks/authoring/publish-playbook.png)

所有创建的行动手册都可在&#x200B;**您的行动手册**&#x200B;选项卡中找到。

![“您的行动手册”选项卡](/help/use-case-playbooks/assets/playbooks/authoring/your-playbooks-tab.png)

您可以从目录中选择任何行动手册，以创建实例以供重用。 请参阅文档以[了解如何创建实例](/help/use-case-playbooks/playbooks/create-share-reuse.md)。

选择行动手册后，![“创建实例”选项在“行动手册概述”选项卡中突出显示。](/help/use-case-playbooks/assets/playbooks/authoring/create-instance.png)

>[!NOTE]
>
> 剧本发布后，便无法编辑。 要进行更改，请删除剧本，然后重新开始。

## 示例提示

AI Assistant可以处理各种提示结构和提取关键细节，同时过滤掉不必要的信息。 以下是用户提示的一些示例以及系统如何解释它们：

**示例1：**

创建标题为“Complete the Look”的营销活动以提高销售额和CLV。 此活动鼓励购买厨具或家具的客户通过与购买相关的个性化推荐和优惠完成补充购买。 第一个消息是向客户提供产品推荐。 如果他们在7天内未进行任何购买，则会收到第二条消息，其中包含产品建议和选件。 使用推送通知和电子邮件联系客户。 定位过去7天在厨具或家具类别中购买过，且过去30天内未成为目标的客户。 作为营销活动的一部分，我们希望测量KPI，例如点击次数（电子邮件、应用程序、短信、推送）、CTR、电子钱包CTR、AOV转化、CLV收入、总购买事件（店内、数字、呼叫中心）。”

![示例1提示](/help/use-case-playbooks/assets/playbooks/authoring/example-prompt.png)

**示例2：**

“项目名称：时尚新闻稿
背景： （主动解决或解决问题）：旨在向订阅了新闻稿通信的ACME客户发送时尚新闻稿的历程。
目标：向订阅了通信的ACME客户发送时尚新闻稿电子邮件。
促销详细信息：客户每周通过电子邮件渠道接收时尚新闻。 电子邮件应基于性别、语言和市场进行个性化和内容变化。
项目渠道/接触点：电子邮件
目标受众：已订阅ACME时尚新闻稿通信的客户。
目标KPI/参与量度/ROI：1。 增加来自产品之收益。 2.提高客户忠诚度。”

![示例2提示](/help/use-case-playbooks/assets/playbooks/authoring/example-2-prompt.png)

**示例3：**

“在正在进行的产品促销活动中，鼓励消费者购买产品。
通过电子邮件、短信或推送通知发送适当的通信内容来购买产品，从而在持续促销期间与购物者互动。 在他们24小时没有参与促销活动后，向他们发送提醒电子邮件。”

![示例3提示](/help/use-case-playbooks/assets/playbooks/authoring/example-3-prompt.png)

**示例4：**

“卖鞋给高中生。”

![示例4提示](/help/use-case-playbooks/assets/playbooks/authoring/example-4-prompt.png)

AI助手会删除所有不必要的详细信息，如“项目名称”或“背景”。 它可提取“目标受众”、“营销目标”和“营销渠道”等关键元素，并可与任何输入样式配合使用。

这些示例演示了AI如何从用户提示中优化和提取基本详细信息。

>[!NOTE]
>
> 在编写提示时避免使用任何PII或显式单词。

## 内容准则和审核

在创建行动手册时，请注意包括的语言和内容。 行动手册在整个组织中可见，用户可标记任何攻击性或不适当的内容。

### 标记和审阅流程

如果行动手册被标记为不适当或冒犯性的内容，则会自动报告给Adobe以供审查。 然后，Adobe会审查标记的内容，如果认为不适当，则会通知客户，并删除剧本。

## 后续步骤

现在您已了解如何使用AI助手创建和发布行动手册，了解如何开始使用可用的行动手册，并从[行动手册列表](/help/use-case-playbooks/playbooks/choose.md)为您的用例选择正确的行动手册。
