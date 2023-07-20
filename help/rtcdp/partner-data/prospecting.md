---
title: （测试版）通过潜在客户用例吸引和赢取新客户
description: 了解如何通过Real-Time CDP中的合作伙伴数据支持提供的潜在用例吸引和赢取新客户。
hide: true
hidefromtoc: true
badgeBeta: label="Beta" type="informative" before-title="true"
source-git-commit: 486e1390dfa0602bef15d196d4a1a5befdc9ff23
workflow-type: tm+mt
source-wordcount: '1953'
ht-degree: 15%

---

# 通过潜在客户用例吸引和赢取新客户

>[!AVAILABILITY]
>
>* 此 Beta 功能可供已获得 Real-Time CDP（应用程序服务）、Adobe Experience Platform 激活、Real-time CDP、Real-Time CDP Prime、Real-Time CDP Ultimate 许可的客户使用。阅读[产品说明](https://helpx.adobe.com/legal/product-descriptions.html)中关于这些软件包的详细信息，并联系您的 Adobe 代表了解更多信息。

使用Real-Time CDP中的第三方数据支持，通过数据合作伙伴提供的潜在客户配置文件来扩展您的用户档案库，并与他们互动以获取或吸引新客户。

![客户发现潜在客户用例高级可视化概述。](/help/rtcdp/assets/partner-data/prospecting/prospecting-use-case-overview.png)

## 先决条件和规划 {#prerequisites-and-planning}

当您考虑使用Real-Time CDP中的合作伙伴数据支持联系和吸引新客户时，请考虑在规划过程中满足以下先决条件：

* 您希望合作伙伴提供的配置文件以何种节奏摄取并刷新Real-Time CDP？
* 您的下游目标需要什么身份？
* 确保摄取的标识符可在下游操作
* 您正在摄取的合作伙伴数据是否绑定到广泛接受的持久标识符，例如个人身份信息(PII)、经过哈希处理的PII或合作伙伴标识符？
* 从合作伙伴的角度以及您自己的法律、隐私或合规团队来看，您需要了解哪些数据使用策略？

## 如何实现该用例：高级概述 {#achieve-the-use-case-high-level}

在您扩展Real-Time CDP以吸引和赢取新客户之前，请确保使用Real-Time CDP为您的第一部分数据奠定坚实的基础。 实现此用例的工作流类似于与已知客户互动的工作流。

![客户发现潜在客户用例高级可视化概述。](/help/rtcdp/assets/partner-data/prospecting/prospecting-use-case-steps.png)

1. As a **客户**，您可从一个或多个目标客户配置文件授予许可 **数据合作伙伴** 帮助推动漏斗客户获取工作。
2. As a **客户**，您可以扩展用户档案数据和治理模型以摄取 **合作伙伴** — 提供的目标客户配置文件列表。
3. As a **客户**，您可以将潜在客户配置文件加载到Real-Time CDP中，并构建治理策略以确保负责任地使用。
4. As a **客户**，则可以从潜在客户用户档案的列表中构建重点受众。
5. As a **客户**，您可以将潜在客户受众激活到接受潜在客户列表中可用身份的目标。
6. 如果需要，请使用 **数据合作伙伴** 用于向所需的付费媒体目标进行最后一英里激活。

## 如何实现用例：分步说明 {#step-by-step-instructions}

通读以下部分（其中包括指向更多文档的链接），以完成上面高级概述中的每个步骤。

### 您将使用的UI功能和元素 {#ui-functionality-and-elements}

在您完成实施用例的步骤后，您将使用以下Real-Time CDP功能和UI元素（按使用顺序列出）。 确保您具有所有这些区域所需的基于属性的访问控制权限，或要求系统管理员授予您必要的权限。

* [标识](/help/identity-service/namespaces.md)
* [架构](/help/xdm/home.md)
* [数据使用情况标签](/help/data-governance/labels/overview.md)
* [数据集](/help/catalog/datasets/overview.md)
* [源](/help/sources/home.md)
* 用户档案（指向潜在客户用户档案的链接）
* 受众（链接到潜在客户受众）
* [目标](/help/destinations/home.md)

### 从合作伙伴处许可第三方配置文件详细信息 {#license-profiles-from-partner}

此步骤在 [先决条件](#prerequisites-and-planning) 和Adobe假定您与受信任的数据供应商签订了正确的合同协议，可以摄取数据合作伙伴提供的潜在客户配置文件。

### 扩展您的用户档案数据和治理模型，以适应合作伙伴提供的潜在客户用户档案 {#extend-governance-model}

为了准备从数据合作伙伴接收目标客户配置文件，您必须在Real-Time CDP中扩展数据管理框架以适应此新配置文件类型。

您将使用的身份、数据管理和治理组件包括：

* 新 **[!UICONTROL 合作伙伴ID]** 合作伙伴提供的配置文件的标识类型
* 新 **[!UICONTROL XDM单个潜在客户配置文件]** XDM类
* **（文档即将发布）** 为合作伙伴数据支持量身定制的现场小组
* **（文档即将发布）** 您将为来自合作伙伴的属性添加的第三方标签

#### 创建合作伙伴ID标识命名空间

首先，为您将从合作伙伴收到的用户档案创建新的标识类型。 要实现此目的，必须在“身份”部分中创建该类型的新身份命名空间 **[!UICONTROL 合作伙伴ID]**.

![创建新的合作伙伴ID标识命名空间。](/help/rtcdp/assets/partner-data/prospecting/create-partner-identity-namespace.png)

* 有关合作伙伴ID命名空间的更多信息，请参阅 [身份类型部分](/help/identity-service/namespaces.md).
* 阅读 Experience Platform 用户界面中有关[如何定义身份字段](/help/xdm/ui/fields/identity.md)的内容。

#### 使用创建新架构 **[!UICONTROL XDM单个潜在客户配置文件]** 类

下一个，在 **[!UICONTROL 数据管理]** > **[!UICONTROL 架构]**，创建新架构并为其分配 **[!UICONTROL XDM单个潜在客户配置文件]** 类。

![在XDM架构生成器中搜索XDM Individual Prospect Profile类。](/help/rtcdp/assets/partner-data/prospecting/xdm-individual-prospect-class.png)

阅读如何 [在UI中创建和编辑架构](/help/xdm/ui/resources/schemas.md) 并获取有关XDM Individual Prospect Profile类别的完整信息（即将提供链接）。

此 **[!UICONTROL XDM单个潜在客户配置文件]** 类预配置了以下显示的字段。 要使用合作伙伴为潜在客户配置文件提供的属性扩充您的架构，您可以使用所需的属性创建新字段组并将其添加到架构中，也可以使用Adobe提供的预配置字段组之一。

![XDM Individual Prospect Profile类的预配置字段。](/help/rtcdp/assets/partner-data/prospecting/preconfigured-fields-individual-prospect-class.png)

接下来，您必须选择之前创建的partnerID标识作为架构的主标识。 配置文件记录必须带有主要标识符。 此步骤是确保目标客户数据可以加载到配置文件存储中并可用于分段和激活所必需的。

>[!AVAILABILITY]
>
>目标客户配置文件自动限制为仅使用合作伙伴ID类型的ID命名空间。 这是通过设计实现的，并确保将您的第一方和潜在客户用户档案进行干净的分离。

![选择之前配置的合作伙伴ID作为架构中的主要标识。](/help/rtcdp/assets/partner-data/prospecting/select-partner-id-as-primary-identity.gif)

请注意，尚未为配置文件启用架构。 切换配置文件按钮以启用此架构以包含在配置文件服务中。 有关启用架构以便在Real-Time Customer Profile中使用的更多信息，请参阅 [创建架构教程。](/help/xdm/tutorials/create-schema-ui.md#profile)

![为配置文件启用模式.](/help/rtcdp/assets/partner-data/prospecting/enable-schema-for-profile.png)

#### 将第三方数据管理标签添加到架构中的所有字段

考虑将第三方数据管理标签添加到组成架构的所有字段。 为了确保负责任地使用第三方数据并最大程度地降低数据泄露风险，这一点非常重要。 查找有关第三方数据管理标签的更多信息（添加约旦提供的文档链接）

为此，请执行以下步骤：

1. 导航到您创建的架构并选择 **[!UICONTROL 标签]** 选项卡。
2. 使用最顶部的复选框按钮选择此架构中的所有字段，然后单击右侧的铅笔图标以将数据治理标签应用于此架构。
3. 选择 **[!UICONTROL 合作伙伴生态系统]** 左侧类别中的标签。
4. 选择名为的标签 **[!UICONTROL 第三方]** 并选择 **[!UICONTROL 保存]**.
5. 请注意，架构中的所有字段现在都带有您在上一步中选择的标签。

>[!SUCCESS]
>
>您的架构现在可以使用了，您可以继续下一步以从数据合作伙伴中摄取潜在客户数据。

此外，在此步骤中，请考虑当您通过扩展数据管理策略来加入合作伙伴提供的第三方数据时，您的数据治理模型会如何变化。探索以下文档链接中的注意事项：

* （**即将推出**）将第三方数据保存在单独的数据集中，以便轻松地删除它并撤消集成。
* (**即将推出**）购买数据卫生附加组件的客户可在数据集上使用[数据集过期](/help/hygiene/ui/dataset-expiration.md)功能。
* （**即将推出**）创建引入第三方数据的派生数据集时请务必小心，因为一旦混合在一起，删除第三方数据的唯一解决方案是删除整个派生数据集。

### 加载目标客户配置文件列表并检查目标客户配置文件视图

在您准备好数据模型以管理潜在客户用户档案后，是时候引入数据了。

#### 创建数据集并加载示例目标客户数据

要加载一些示例数据并填充目标客户配置文件，请创建一个数据集并上传您从数据合作伙伴收到的文件。 完成以下步骤：

1. 导航到 **[!UICONTROL 数据管理]** > **[!UICONTROL 数据集]** 并选择 **[!UICONTROL 创建数据集]**.
2. 选择“从架构创建数据集”
3. 选择在上一步中创建的架构
4. 为数据集命名并指定描述（可选）。
5. 选择&#x200B;**[!UICONTROL 完成]**。

![为潜在客户用户档案创建数据集步骤的记录。](/help/rtcdp/assets/partner-data/prospecting/create-dataset-for-prospect-profiles.gif)

请注意，与创建架构的步骤类似，您需要启用数据集以包含在Real-time Customer Profile中。 有关启用数据集以在Real-time Customer Profile中使用的更多信息，请参阅 [创建架构教程。](/help/xdm/tutorials/create-schema-ui.md#profile)

![为配置文件启用数据集。](/help/rtcdp/assets/partner-data/prospecting/enable-dataset-for-profile.png)

要将您从合作伙伴收到的文件加载到数据集中，请选择该数据集，在右边栏中向下滚动，然后选择 **[!UICONTROL 添加数据]**. 您可以拖放文件或选择 **[!UICONTROL 选择文件]** 导航到文件位置并将其选定。

![将文件添加到数据集。](/help/rtcdp/assets/partner-data/prospecting/add-file-to-dataset.png)

将数据合作伙伴的用户档案列表加载到Real-Time CDP后，请转到 [Inspect已加载的目标客户配置文件部分](#inspect-profiles) 以检查UI中是否填充了潜在客户配置文件。

#### 通过源连接器引入目标客户数据

您可以设置重复文件导入，以通过源连接器从合作伙伴中摄取数据，并将潜在客户用户档案列表引入Real-Time CDP。

Real-Time CDP下面列出了为此目的推荐的一些源连接器，但请注意，任何基于文件的摄取方法都可以用于您的目的。

* [Amazon S3](/help/sources/connectors/cloud-storage/s3.md)
* [SFTP](/help/sources/connectors/cloud-storage/sftp.md)

将数据合作伙伴的用户档案列表加载到Real-Time CDP中后，请转到下一部分以检查是否在UI中填充潜在客户用户档案。

#### Inspect加载的目标客户配置文件 {#inspect-profiles}

要查看目标客户配置文件的列表，请导航到 **[!UICONTROL 潜在客户]** > **[!UICONTROL 配置文件]** 在左边栏中。

请注意，您刚刚加载到Real-Time CDP中的潜在客户配置文件可能需要长达两个小时才能显示在中 **[!UICONTROL 浏览]** Prospect Profile屏幕视图。 如果页面显示消息“当前没有可浏览的潜在客户配置文件”，请稍后重试。 等待一段时间后，潜在客户配置文件应开始显示在 **[!UICONTROL 浏览]** 视图。

>[!TIP]
>
>请注意 **[!UICONTROL 身份命名空间]** 列。 如果您与多个数据供应商合作，请使用此列推断潜在客户配置文件的来源。

![加载到Real-Time CDP中的目标客户用户档案视图。](/help/rtcdp/assets/partner-data/prospecting/prospect-profiles-view.png)

您还可以选择任何潜在客户配置文件进行进一步检查，如下所示。

![有关如何检查目标客户配置文件的视图。](/help/rtcdp/assets/partner-data/prospecting/inspect-prospect-profile.gif)

(**即将推出**)阅读有关潜在客户配置文件的更多信息。

### 创建目标客户受众 {#create-prospect-audiences}

使用Real-Time CDP中的分段功能，从潜在客户配置文件中创建受众。 使用所需的分段规则来创建定制的受众。

要开始使用并构建由潜在客户配置文件组成的受众，请导航到 **[!UICONTROL 潜在客户]** > **[!UICONTROL 受众]**.

![目标客户受众视图。](/help/rtcdp/assets/partner-data/prospecting/prospect-audiences.png)

请注意，目标客户配置文件的受众构建体验不同于从已知的第一方客户构建受众的体验。 此视图仅限于：

* 您之前创建的目标客户类中的属性。
* 仅限批次配置文件评估。
* 不支持根据时间序列事件构建受众。

(**即将推出**)阅读有关潜在客户受众的更多信息。

### 将目标客户配置文件激活到目标 {#activate-to-destinations}

通过将潜在客户受众导出到目标来利用这些受众。 目前，仅特定目标，例如 [Amazon S3](/help/destinations/catalog/cloud-storage/amazon-s3.md) 或 [!BADGE 字母]{type=Informative}[LiveRamp](/help/destinations/catalog/advertising/liveramp.md) 目标支持激活目标客户配置文件。

## 由合作伙伴数据支持实现的其他用例 {#other-use-cases}

探索通过 Real-Time CDP 中的合作伙伴数据支持实现的更多用例：

* [!BADGE Beta]{type=Informative}[使用可信赖的数据合作伙伴的属性来补充第一方配置文件，以改善您的数据基础，获得对客户群的全新见解，并提升受众优化。](/help/rtcdp/partner-data/supplement-first-party-profiles.md)
* （**即将推出**）[!BADGE Beta]{type=Informative}**利用合作伙伴辅助的认可**&#x200B;在访问期间提供个性化现场体验，以及在访问后异地重新定位，而无需用户进行身份验证或之前使用过您的品牌。