---
title: 在不依赖第三方Cookie的情况下吸引和赢取新客户
description: 了解如何不依赖第三方 Cookie，而是通过潜在客户发掘用例吸引和获得新客户。
feature: Use Cases, Customer Acquisition
exl-id: b9e7b3af-2a13-4904-bd12-e3ed05a1988e
source-git-commit: e7c0551276d31d6809ace096c00e0dc2665090e6
workflow-type: tm+mt
source-wordcount: '2074'
ht-degree: 86%

---

# 在不依赖第三方Cookie的情况下吸引和赢取新客户

>[!AVAILABILITY]
>
>* 已获得许可Real-Time CDP（应用程序服务）、Adobe Experience Platform Activation、Real-Time CDP、Real-Time CDP Prime、Real-Time CDP Ultimate的客户可以使用此功能。 阅读[产品说明](https://helpx.adobe.com/cn/legal/product-descriptions.html)中关于这些软件包的详细信息，并联系您的 Adobe 代表了解更多信息。

使用 Real-Time CDP 中的第三方数据支持，通过数据合作伙伴提供的潜在客户轮廓拓展您的轮廓基础，并与潜在客户交流以获取或接触新客户。

![潜在客户发掘用例大致视觉概述。](/help/rtcdp/assets/partner-data/prospecting/prospecting-use-case-overview.png)

## 为什么考虑此用例 {#why-this-use-case}

各品牌同时面临着严峻的挑战：如何在不依赖第三方Cookie、预算有限、对透明度和广告支出回报要求较高的情况下，负责任地执行漏斗顶级的客户获取用例。

Adobe Real-Time Customer Data Platform可帮助品牌商安全地将其支持的数据管理平台(DMP)用例转换为无Cookie的替代方案，并且可将自助式分段、受众管理和激活的全部复杂性和功能整合到单个系统中。 Adobe始终专注于通过专利数据治理和同意框架负责任地使用数据，这一点丝毫没有影响。

例如，在需要运行营销活动以吸引潜在客户成为用户或已知客户时，请按照此用例中描述的步骤进行操作。

## 先决条件和规划 {#prerequisites-and-planning}

当您考虑联系和获得新客户时，请考虑在计划流程中的以下先决条件：

* 您希望将合作伙伴提供的轮廓摄取到 Real-Time CDP 中并进行刷新的节奏是什么？
* 您的下游目标需要什么身份标识？
* 确保摄取的标识符为可操作的下游
* 您摄取的合作伙伴数据是否与广泛接受的可持久标识符（如个人身份信息 (PII)、经过哈希处理的 PII 或合作伙伴标识符）有关？
* 从合作伙伴的角度以及您自己的法律、隐私或合规团队的角度来看，您需要了解哪些数据使用政策？

## 如何实现该用例：大致概述 {#achieve-the-use-case-high-level}

在拓展 Real-Time CDP 以吸引和获取新客户之前，请确保使用 Real-Time CDP 为您的第一方数据打下坚实的基础。实现此用例的工作流类似于与您已知的客户交流的工作流。

![潜在客户发掘用例大致视觉概述。](/help/rtcdp/assets/partner-data/prospecting/prospecting-use-case-steps.png)

1. 作为&#x200B;**客户**，您授予来自一个或多个&#x200B;**数据合作伙伴**&#x200B;的潜在客户轮廓的许可，帮助推动漏斗顶部的客户获取。
2. 作为&#x200B;**客户**，您扩展您的轮廓数据和治理模型以摄取&#x200B;**合作伙伴**&#x200B;提供的潜在客户轮廓列表。
3. 作为&#x200B;**客户**，您将潜在客户轮廓加载到 Real-Time CDP 中，并制定治理策略来确保负责任的使用。
4. 作为&#x200B;**客户**，您可以从潜在客户轮廓列表中构建重点受众。
5. 作为&#x200B;**客户**，您将潜在客户受众激活到接受潜在客户列表中可用的身份标识的目标。
6. 如果需要，请与&#x200B;**数据合作伙伴**&#x200B;合作，最终将受众激活到所需的付费媒体目标。

## 视频演练 {#video-walkthrough}

观看下面的视频教程，逐步了解如何联系和吸引潜在受众：

>[!VIDEO](https://video.tv.adobe.com/v/3423071/?learn=on)

## 如何实现用例：分步说明 {#step-by-step-instructions}

通读以下部分（其中包括指向更多文档的链接）以完成上方大致概述中的每个步骤。

### 您将使用的 UI 功能和元素 {#ui-functionality-and-elements}

在完成实现用例的步骤后，您将使用以下 Real-Time CDP 功能和 UI 元素（按使用顺序列出）。确保您拥有所有这些区域所需的基于属性的访问控制权限，或让系统管理员授予您这些必要的权限。

* [身份标识](/help/identity-service/features/namespaces.md)
* [架构](/help/xdm/home.md)
* [数据使用情况标签](/help/data-governance/labels/overview.md)
* [数据集](/help/catalog/datasets/overview.md)
* [源](/help/sources/home.md)
* [潜在客户轮廓](/help/profile/ui/prospect-profile.md)
* [潜在客户受众](/help/segmentation/types/prospect-audiences.md)
* [目标](/help/destinations/home.md)

### 授予来自合作伙伴的第三方轮廓详细信息的许可 {#license-profiles-from-partner}

这一步骤包含在[先决条件](#prerequisites-and-planning)中，Adobe 假设您与可信赖的数据供应商签订了恰当的合同协议，以摄取数据合作伙伴提供的潜在客户轮廓。

### 扩展您的轮廓数据和治理模型，以适应合作伙伴提供的潜在客户轮廓。 {#extend-governance-model}

要准备接收来自数据合作伙伴的潜在客户轮廓，您必须扩展 Real-Time CDP 中的数据管理框架以适应这种新的轮廓类型。

您将使用的身份标识、数据管理和治理组件包括：

* 合作伙伴提供的轮廓的新&#x200B;**[!UICONTROL 合作伙伴 ID]** 身份标识类型
* 新的 **[!UICONTROL XDM 单个潜在客户轮廓]** XDM 类
* **（文档即将发布）**&#x200B;为合作伙伴数据支持定制的字段组
* **（文档即将发布）**&#x200B;您将添加到来自合作伙伴的属性的第三方标签

#### 创建合作伙伴 ID 身份标识命名空间 {#create-partner-id-namespace}

首先，为您将从合作伙伴处收到的轮廓创建新的身份标识类型。为此，在“身份标识”部分中，您必须创建&#x200B;**[!UICONTROL 合作伙伴 ID]** 类型的新的身份标识命名空间。

![创建新的合作伙伴 ID 身份标识命名空间。](/help/rtcdp/assets/partner-data/prospecting/create-partner-identity-namespace.png)

* 阅读[身份标识类型部分](/help/identity-service/features/namespaces.md)，了解有关合作伙伴 ID 命名空间的更多信息。
* 阅读 Experience Platform 用户界面中有关[如何定义身份标识字段](/help/xdm/ui/fields/identity.md)的内容。

#### 使用 **[!UICONTROL XDM 单个潜在客户轮廓]**&#x200B;类创建新架构

接下来，在&#x200B;**[!UICONTROL 数据管理]** > **[!UICONTROL 架构]**&#x200B;中，创建一个新架构并将其分配给 **[!UICONTROL XDM 单个潜在客户轮廓]**&#x200B;类。

![在 XDM 架构生成器中搜索 XDM 单个潜在客户轮廓类。](/help/rtcdp/assets/partner-data/prospecting/xdm-individual-prospect-class.png)

了解如何[在 UI 中创建和编辑架构](/help/xdm/ui/resources/schemas.md)，并获取有关 XDM 单个潜在客户轮廓类的完整信息（链接即将发布）。

**[!UICONTROL XDM 单个潜在客户轮廓]**&#x200B;类已预先配置下面显示的字段。要使用合作伙伴为潜在客户轮廓提供的属性来扩充您的架构，您可以使用所需属性创建一个新的字段组并将其添加到架构中，也可以使用 Adobe 提供的某个预配置的字段组。

![XDM 单个潜在客户轮廓类的预配置的字段。](/help/rtcdp/assets/partner-data/prospecting/preconfigured-fields-individual-prospect-class.png)

接下来，您必须选择之前创建的 partnerID 身份标识作为架构的主要身份标识。轮廓记录必须带有主要标识符。此步骤是确保能够将潜在客户数据加载到配置文件存储中并使其可用于分段和激活所必需的。

>[!AVAILABILITY]
>
>潜在客户轮廓会自动限制为仅使用合作伙伴 ID 类型的 ID 命名空间。这是经过设计的，可确保您的第一方轮廓和潜在客户轮廓之间的清晰分离。

![选择之前配置的合作伙伴 ID 作为架构中的主要身份标识。](/help/rtcdp/assets/partner-data/prospecting/select-partner-id-as-primary-identity.gif)

请注意，尚未为轮廓启用架构。切换轮廓按钮以启用此架构，以便包含在轮廓服务中。有关启用架构以在实时客户轮廓中使用的更多信息，请参阅[创建架构教程。](/help/xdm/tutorials/create-schema-ui.md#profile)

![为轮廓启用架构。](/help/rtcdp/assets/partner-data/prospecting/enable-schema-for-profile.png)

#### 将第三方数据治理标签添加到架构中的所有字段

考虑将第三方数据治理标签添加到构成架构的所有字段。这对于确保负责任地使用第三方数据并最大限度地降低数据泄露风险非常重要。查找有关[第三方数据管理标签](../../data-governance/labels/reference.md#partner-ecosystem-labels)的更多信息。

为此，请执行以下步骤：

1. 导航到您创建的架构并选择&#x200B;**[!UICONTROL 标签]**&#x200B;选项卡。
2. 使用最上方的复选框按钮选择此架构中的所有字段，然后单击右侧的铅笔图标以将数据治理标签应用于此架构。
3. 从左侧的类别中选择&#x200B;**[!UICONTROL 合作伙伴生态系统]**&#x200B;标签。
4. 选择名为&#x200B;**[!UICONTROL 第三方]**&#x200B;的标签，并选择&#x200B;**[!UICONTROL 保存]**。
5. 请注意，架构中的所有字段现已具有上一步中选择的标签。

>[!SUCCESS]
>
>您的架构现已可供使用，您可以继续执行下一步以摄取来自数据合作伙伴的潜在客户数据。

此外，在此步骤中，请考虑当您通过扩展数据管理策略来加入合作伙伴提供的第三方数据时，您的数据治理模型会如何变化。探索以下文档链接中的注意事项：

* （**即将推出**）将第三方数据保存在单独的数据集中，以便轻松地删除它并撤消集成。
* (**即将推出**）购买数据卫生附加组件的客户可在数据集上使用[数据集过期](/help/hygiene/ui/dataset-expiration.md)功能。
* （**即将推出**）创建引入第三方数据的派生数据集时请务必小心，因为一旦混合在一起，删除第三方数据的唯一解决方案是删除整个派生数据集。

### 加载潜在客户轮廓列表并检查潜在客户轮廓视图

在准备好用于管理潜在客户轮廓的数据模型后，就可以摄取数据了。

#### 创建数据集并加载示例潜在客户数据

要加载一些示例数据并填充潜在客户轮廓，请创建数据集并上传您从数据合作伙伴那里收到的文件。完成以下步骤：

1. 导航到&#x200B;**[!UICONTROL 数据管理]** > **[!UICONTROL 数据集]**，并选择&#x200B;**[!UICONTROL 创建数据集]**。
2. 选择“从架构创建数据集”
3. 选择您在上一步中创建的架构
4. 为您的数据集命名并（可选）提供描述。
5. 选择&#x200B;**[!UICONTROL 完成]**。

![用于为潜在客户轮廓创建数据集的步骤的记录。](/help/rtcdp/assets/partner-data/prospecting/create-dataset-for-prospect-profiles.gif)

请注意，与架构创建步骤类似，您需要使数据集包含在实时客户轮廓中。有关启用数据集以在实时客户轮廓中使用的更多信息，请参阅[创建架构教程。](/help/xdm/tutorials/create-schema-ui.md#profile)

![为轮廓启用数据集。](/help/rtcdp/assets/partner-data/prospecting/enable-dataset-for-profile.png)

要将您从合作伙伴处收到的文件加载到数据集中，请选择数据集，在右边栏中向下滚动，然后选择&#x200B;**[!UICONTROL 添加数据]**。您可以拖放文件或选择&#x200B;**[!UICONTROL 选择文件]**&#x200B;以导航到文件位置并将其选定。

![将文件添加到数据集。](/help/rtcdp/assets/partner-data/prospecting/add-file-to-dataset.png)

将来自数据合作伙伴的轮廓列表加载到 Real-Time CDP 中后，继续进入[“检查加载的潜在客户轮廓”部分](#inspect-profiles)以检查潜在客户轮廓是否正填入 UI 中。

#### 通过源连接器摄取潜在客户数据

您可以设置定期文件导入，以通过源连接器摄取来自合作伙伴的数据，并将潜在客户轮廓列表引入 Real-Time CDP 中。

下面列出了一些用于此目的的推荐的源连接器，但请注意，任何基于文件的摄取到 Real-Time CDP 中的方法都能用于实现您的目的。

* [Amazon S3](/help/sources/connectors/cloud-storage/s3.md)
* [SFTP](/help/sources/connectors/cloud-storage/sftp.md)

将来自数据合作伙伴的轮廓列表加载到 Real-Time CDP 中后，继续进入下一部分以检查潜在客户轮廓是否正填入 UI 中。

#### 检查加载的潜在客户轮廓 {#inspect-profiles}

要查看潜在客户轮廓列表，请在左边栏中导航到&#x200B;**[!UICONTROL 潜在客户]** > **[!UICONTROL 轮廓]**。

请注意，您刚刚加载到 Real-Time CDP 中的潜在客户轮廓可能最多需要两个小时，才能显示在潜在客户轮廓屏幕的&#x200B;**[!UICONTROL 浏览]**&#x200B;视图中。如果页面显示消息“目前没有可供浏览的潜在客户轮廓”，请稍后重试。等待一段时间后，潜在客户轮廓应开始显示在&#x200B;**[!UICONTROL 浏览]**&#x200B;视图中。

>[!TIP]
>
>请注意，存在&#x200B;**[!UICONTROL 身份标识命名空间]**&#x200B;列。如果您与多个数据供应商合作，请使用此列来推断潜在客户轮廓的来源。

![加载到 Real-Time CDP 中的潜在客户轮廓的视图。](/help/rtcdp/assets/partner-data/prospecting/prospect-profiles-view.png)

您还可以选择任何潜在客户轮廓以执行进一步检查，如下所示。

![潜在客户轮廓的检查方式的视图。](/help/rtcdp/assets/partner-data/prospecting/inspect-prospect-profile.gif)

阅读有关[潜在客户轮廓](/help/profile/ui/prospect-profile.md)的更多信息。

### 创建潜在客户受众 {#create-prospect-audiences}

使用 Real-Time CDP 中的分段功能，从潜在客户轮廓创建受众。使用所需的分段规则来创建定制的受众。

要开始使用并构建由潜在客户轮廓构成的受众，请导航到&#x200B;**[!UICONTROL 潜在客户]** > **[!UICONTROL 受众]**。

![潜在客户受众的视图。](/help/rtcdp/assets/partner-data/prospecting/prospect-audiences.png)

请注意，潜在客户轮廓的受众构建体验与从已知的第一方客户构建受众的体验不同。此视图仅限于：

* 您之前创建的潜在客户类的属性。
* 仅批量轮廓评估。
* 不支持根据时间序列事件构建受众。

阅读有关[潜在客户受众](/help/segmentation/types/prospect-audiences.md)的更多信息。

### 激活目标的潜在客户轮廓 {#activate-to-destinations}

通过将潜在客户受众导出到目标来利用它们。目前，只有某些云存储目标支持激活潜在客户配置文件。

![支持潜在客户受众的目标。](/help/destinations/assets/ui/activate-prospect-audiences/data-types-filter.png)

[阅读有关将潜在客户激活到云存储目标的更多信息](/help/destinations/ui/activate-prospect-audiences.md)。

## 由合作伙伴数据支持实现的其他用例 {#other-use-cases}

探索通过 Real-Time CDP 中的合作伙伴数据支持实现的更多用例：

* [用受信任的数据合作伙伴提供的属性补充第一方轮廓](/help/rtcdp/partner-data/supplement-first-party-profiles.md)，以改善您的数据基础、了解客户群的新情况并获得更好的受众优化。
* [在访问期间使用合作伙伴帮助的访客识别](/help/rtcdp/partner-data/onsite-personalization.md)为未知访客提供个性化现场体验，用户无需进行身份验证或没有您的品牌历史记录。
* [扩大了潜在客户轮廓和潜在客户受众的激活范围](/help/destinations/ui/activate-prospect-audiences.md)，以选择目标。
