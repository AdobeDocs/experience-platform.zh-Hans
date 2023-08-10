---
title: 使用合作伙伴辅助的访客识别功能来个性化现场体验
description: 了解如何使用合作伙伴辅助的访客识别，为访客提供个性化的现场体验。
hide: true
hidefromtoc: true
source-git-commit: b66a50e40aaac8df312a2c9a977fb8d4f1fb0c80
workflow-type: tm+mt
source-wordcount: '2492'
ht-degree: 7%

---

# 使用合作伙伴辅助的访客识别功能来个性化现场体验

了解如何使用合作伙伴辅助的识别功能，为Web资产访客提供个性化体验。 使用本教程了解Experience Platform和其他Experience Cloud解决方案中各种元素的实施顺序，向经过身份验证和未经身份验证的访客显示个性化体验。

![此信息图表描述如何使用合作伙伴提供的属性为访客提供个性化体验。](/help/rtcdp/assets/partner-data/onsite-personalization/onsite-personalization-steps.png)

## 行业示例 {#industry-example}

例如，考虑一个身份验证率较低的家庭改进品牌。 此品牌希望向首次访问的访客提供个性化的体验，而无需过往历史记录或身份验证，并且不会减少对第三方Cookie的依赖。

此品牌选择利用合作伙伴识别技术以概率方式识别访客，并提供更个性化的体验。 当访客在营销漏斗中向下移动时，这有助于提高考虑程度。 例如，该品牌可能会使用合作伙伴提供的人口统计信号来显示网站上的内容，以吸引最近刚搬家的人，并为流行的DIY产品提供折扣。

## 先决条件和规划 {#prerequisites-and-planning}

当计划使用合作伙伴提供的属性为您的经过身份验证和未经身份验证的访客提供个性化体验时，请考虑以下在计划过程中的先决条件：

* 合作伙伴的识别技术需要哪些输入，以便它们可以叠加其他属性？
* 与确定性确认属性相比，您在多大程度上可以轻松地根据概率派生的属性在不同渠道和不同用例中实现个性化？
* 经过预身份验证但已识别的访客在进行身份验证时，其体验应该如何变化？

### 用户界面功能、平台组件以及您将使用的Experience Cloud产品 {#ui-functionality-and-elements}

要成功实施此用例，您必须使用Real-time Customer Data Platform和其他Experience Cloud解决方案的多个区域。 确保您拥有所需的 [基于属性的访问控制权限](/help/access-control/abac/overview.md) 或要求系统管理员授予您必要的权限。

* 数据收集
   * [Adobe Experience Platform Web SDK](/help/edge/home.md)
   * [标记](/help/tags/home.md)
   * [数据流](/help/datastreams/overview.md)
* Real-Time CDP中的数据管理
   * [标识](/help/identity-service/namespaces.md)
   * [架构](/help/xdm/home.md)
   * [数据使用情况标签](/help/data-governance/labels/overview.md)
   * [数据集](/help/catalog/datasets/overview.md)
* Web属性个性化
   * [边缘分段](/help/segmentation/ui/edge-segmentation.md)
   * [Edge个性化目标](/help/destinations/destination-types.md#edge-personalization-destinations)
   * [Adobe Target](/help/destinations/catalog/personalization/adobe-target-connection.md) （或您选择的个性化平台）。 此用例教程重点介绍了Adobe Target作为个性化引擎)

## 如何实现该用例：大致概述 {#achieve-the-use-case-high-level}

![此信息图表描述如何使用合作伙伴提供的属性为访客提供个性化体验。](/help/rtcdp/assets/partner-data/onsite-personalization/onsite-personalization-steps.png)

1. 作为 **客户**，您从以下位置获得许可 **数据合作伙伴** 能够实时获取有关匿名网站访客的见解。
2. 作为 **客户**，您可以在要调用的资产上部署客户端库 **合作伙伴** API以及您配置Web SDK或Mobile SDK以将合作伙伴提供的信号发送到Real-Time CDP。
3. 浏览您的网站或应用程序时， **访客** 可能会被 **合作伙伴**，用于返回属性和ID。
4. Real-Time CDP运行边缘分段以评估传入的事件点击量并保留针对以下各项的结果 [ECID标识符](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=zh-Hans).
5. Adobe Target使用边缘分段输出将体验呈现回 **访客** 用于会话内个性化。
6. 对于分析和重定位等下游工作流，该事件将完整保留。

## 如何实现用例：分步说明 {#step-by-step-instructions}

通读以下部分（其中包括指向更多文档的链接）以完成上方大致概述中的每个步骤。

### 数据管理 — 创建身份命名空间、架构和数据集以管理数据属性 {#data-management}

为了准备实现用例以个性化未经身份验证的访客体验，您必须首先在Real-Time CDP中设置数据管理结构以接收传入的实时事件和受众资格数据。

#### 创建合作伙伴ID身份命名空间

首先，您需要创建合作伙伴ID身份命名空间。 导航到 **[!UICONTROL 客户]** > **[!UICONTROL 身份]** 在左边栏中，然后选择 **[!UICONTROL 创建身份命名空间]** 在屏幕右上角。

![选中了创建身份命名空间对话框以及合作伙伴ID。](/help/rtcdp/assets/partner-data/onsite-personalization/create-identity-namespace.png)

详细了解如何 [创建合作伙伴ID身份命名空间](/help/rtcdp/partner-data/prospecting.md#create-partner-id-namespace).

#### 创建架构

接下来，创建 [!UICONTROL 体验事件] 用于保存您以后将从Web资产中收集的时间系列数据的架构，并确保使用 [!UICONTROL XDM ExperienceEvent] 作为架构的基类。 阅读如何 [使用Experience PlatformUI创建架构](/help/xdm/ui/resources/schemas.md#create).

![包含创建架构和XDM体验事件的架构工作区突出显示。](/help/rtcdp/assets/partner-data/onsite-personalization/create-experience-event-schema.png)

在创建架构和 [将字段组添加到您的架构](/help/xdm/ui/resources/schemas.md#add-field-groups)，考虑添加 [访问网页](/help/xdm/field-groups/event/web-details.md) 和 [标识映射](/help/xdm/field-groups/profile/identitymap.md) 字段组。 这是适用于您的数字财产和数据收集实践的其他字段组之外的扩展。

此外，您可以创建或重用现有字段组，并将其添加到您的架构中，以捕获合作伙伴提供的关于访客的分析。 阅读如何 [创建字段组](/help/xdm/ui/resources/field-groups.md) 以及操作方法 [添加字段](/help/xdm/ui/resources/field-groups.md) 到字段组。 例如，如果您希望根据合作伙伴提供的见解（如年龄范围、就业状态、每月购买力或购买行为）进行个性化，请让您的字段组包含相应的字段。

假定数据合作伙伴为访客提供了一个稳定的标识符，并且您想要将它引入Real-Time CDP中，请确保为自定义字段组中的标识符提供了正确命名的字段。 您还应在之前创建的身份命名空间中将字段标记为身份。 另请记住 [启用要包含在配置文件中的架构](/help/xdm/ui/resources/schemas.md#profile).

#### 创建数据集

接下来，必须创建一个数据集来保存您从Web资产访客收集并将用于现场个性化的时间序列数据。

阅读有关的教程 [如何创建数据集](/help/catalog/datasets/user-guide.md#create) 并记得选择选项以从架构创建数据集。 根据您在上一步中创建的架构创建数据集。

与创建架构时的步骤类似，您需要启用要包含在中的数据集 [!UICONTROL Real-time Customer Profile]. 有关启用数据集以便在中使用的更多信息 [!UICONTROL Real-time Customer Profile]，阅读 [创建架构教程。](/help/xdm/tutorials/create-schema-ui.md#profile)

### 在Web资产上实施事件数据收集 {#implement-data-collection}

在设置数据管理配置后，您现在需要实施实时事件 [数据收集](/help/collection/home.md) （在您的Web资产上）。 您需要使用Adobe数据收集库检测您的资产 —  [!UICONTROL Web SDK]  — 收集实时事件调用并将它们发送回Real-Time CDP。 此项目由几个数据收集组件中的几个单独任务组成。

>[!IMPORTANT]
>
>要检索合作伙伴提供的属性，您还必须 *将Web资产与合作伙伴API或其他方法集成，以便实时调用并检索数据合作伙伴的属性*. 请与您选择的合作伙伴讨论此方面，因为本教程不涉及此方面。

首先，使用屏幕右上角的应用程序切换器导航到 **[!UICONTROL 数据收集]** 部分。

>[!TIP]
>
>如果您无法查看，请与系统管理员联系以请求访问权限 [!UICONTROL 数据收集] 在应用程序切换器中。

![用于转到“数据收集”部分的应用程序切换器。](/help/rtcdp/assets/partner-data/onsite-personalization/app-switcher-data-collection.png)

此 **[!UICONTROL 数据收集]** UI的部分类似于以下图像。

![Platform UI的数据收集部分。](/help/rtcdp/assets/partner-data/onsite-personalization/data-collection-home.png)

#### 创建数据流

作为数据收集部分的第一步， [创建新数据流](/help/datastreams/configure.md). 数据流是收集数据并正确路由到正确的Adobe应用程序(在本例中为Experience Platform)的基础。

在创建数据流时，在 **[!UICONTROL 事件架构]** 字段中，选择您之前创建的架构。

![配置新数据流时突出显示的事件架构选择器。](/help/rtcdp/assets/partner-data/onsite-personalization/event-schema-selector-datastream.png)

[选择事件数据集](/help/datastreams/configure.md#aep) 之前从下拉列表中创建的下拉菜单，请选中旁边的复选框 **[!UICONTROL 边缘分段]** 和 **[!UICONTROL 个性化目标]**，并选择 **[!UICONTROL 保存]**.

请注意，在此场景中无需选择用户档案数据集，因为您将引入基于事件的时间序列数据。

#### 创建标记属性

将资产视为一个容器，在将标记部署到网站时可在其中填充扩展、规则、数据元素和库。

导航到 **[!UICONTROL 标记]** 并选择 **[!UICONTROL 新建属性]**.

![创建新的标记属性。](/help/rtcdp/assets/partner-data/onsite-personalization/create-tag-property.png)

填写必填字段并选择 **[!UICONTROL 保存]**.

![填写新资产的必填字段。](/help/rtcdp/assets/partner-data/onsite-personalization/tag-property-fields.png)

获取有关如何执行操作的完整信息 [创建标记属性](https://experienceleague.adobe.com/docs/platform-learn/implement-in-websites/configure-tags/create-a-property.html).

接下来，必须在资产中安装各种扩展。 选择您的标记属性并导航到 [!UICONTROL 扩展] 部分。

![选择您的新标记属性。](/help/rtcdp/assets/partner-data/onsite-personalization/select-tag-property.png)

请注意 [!UICONTROL 核心] 已安装扩展。 您必须再安装两个扩展，如下节所述。

![查看已安装的扩展。](/help/rtcdp/assets/partner-data/onsite-personalization/view-existing-extensions.png)

#### 安装Web SDK扩展

请注意，本教程将介绍如何使用Web SDK检测您的网站。 您还可以使用 [移动SDK](https://developer.adobe.com/client-sdks/documentation/) 可将体验个性化。

![扩展目录中的Web SDK扩展视图。](/help/rtcdp/assets/partner-data/onsite-personalization/web-sdk-extension.png)

在配置Web SDK的屏幕中，向下导航到 **[!UICONTROL 数据流]** 部分，并提供有关您使用的Experience Platform沙盒的信息。 从下一个下拉菜单中选择相应的沙盒以及在之前步骤中创建的数据流。 您可以为所有其他环境选择相同的沙盒和数据流值。 保留其他设置不变，然后选择 **[!UICONTROL 保存]**.

获取有关以下项的完整信息： [如何安装Web SDK](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/tags-configuration/install-web-sdk.html).

#### 安装ID服务扩展

使用 [Experience CloudID服务扩展](/help/tags/extensions/client/id-service/overview.md) 为所有Experience Cloud解决方案中的访客创建基于设备的独特第一方身份。 搜索 **[!UICONTROL ID服务]** ，并安装该扩展。 安装扩展时，请保留所有默认设置。

![扩展目录中的ID服务扩展视图。](/help/rtcdp/assets/partner-data/onsite-personalization/id-service-extension.png)

#### 设置环境

接下来，前往 **[!UICONTROL 环境]** 左侧导航栏中的部分。 在此步骤中，您必须将网站连接到Adobe Edge网络，以便实时检索和提供访客信息。

选择开发环境右侧的框图标，并复制在模式窗口中显示的JavaScript代码片段的标准版本。

![在数据收集UI的环境部分中高亮显示的选择框图标。](/help/rtcdp/assets/partner-data/onsite-personalization/select-box-icon.png)

您必须将此代码段添加到网站的最顶部。 因此，您的网站将调用Adobe Edge网络以检索将在页面上加载和执行的JavaScript逻辑。 这允许访客ID生成、数据收集和实时体验个性化等功能发挥作用。

#### 设置数据元素

数据元素是数据字典（或数据映射）的构建块。单个数据元素是一个变量，其值可以映射到查询字符串、URL、Cookie 值、JavaScript 变量等。详细了解 [数据元素](/help/tags/ui/managing-resources/data-elements.md).

出于此用例的目的，您必须设置两个数据元素。

首先，设置 `partnerData` 元素。 导航至 **[!UICONTROL 数据元素]** 部分并选择 **[!UICONTROL 创建新数据元素]**.

![创建新数据元素。](/help/rtcdp/assets/partner-data/onsite-personalization/create-data-element.gif)

将数据元素命名为 `partnerData`，保留 [!UICONTROL 扩展] 值是 [!UICONTROL 核心]，并设置 **[!UICONTROL 数据元素类型]** 作为 **[!UICONTROL JavaScript变量]**. 输入 `partnerData` 在标题为的字段中 **[!UICONTROL JavaScript变量名称]** 并选择 **[!UICONTROL 保存]**.

![突出显示用于正确配置partnerData数据元素的选项。](/help/rtcdp/assets/partner-data/onsite-personalization/create-partnerdata-data-element.png)

要设置第二个数据元素，请命名新变量 `pageVisit`，设置 **[!UICONTROL 扩展名]** 到 **[!UICONTROL Adobe Experience Platform]** 并选择 **[!UICONTROL XDM对象]** 作为数据类型。

![突出显示用于正确配置pageVisit数据元素的选择。](/help/rtcdp/assets/partner-data/onsite-personalization/page-visit-data-element.png)

从架构中，选择与您从数据合作伙伴中期望的值对应的第三方属性。 然后，选择标题为的单选按钮 **[!UICONTROL 提供整个对象]**. 选择与数据库相似的图标，然后选择 `partnerData` 您之前创建的数据元素。

#### 设置规则

在 **[!UICONTROL 规则]** 部分，您可以配置网站以向Adobe发送个性化请求，并将属性加载到您刚刚创建的数据元素中。 详细了解 [创建规则](/help/tags/ui/managing-resources/rules.md).

选择 **[!UICONTROL 创建新规则]**. 命名此规则 **[!UICONTROL 个性化]** 并选择旁边的+符号 **[!UICONTROL 活动]**. 选择 **[!UICONTROL Page Bottom]** 作为事件并保存。

![规则的事件类型部分的选择。](/help/rtcdp/assets/partner-data/onsite-personalization/add-events-rule.png)

选择旁边的+号 **[!UICONTROL 操作]**. 将扩展更新到 **[!UICONTROL Adobe Experience Platform Web SDK]** 并设置 **[!UICONTROL 操作类型]** 到 **[!UICONTROL 发送事件]**.

![规则的操作类型部分的选择。](/help/rtcdp/assets/partner-data/onsite-personalization/add-action-rule.png)

从 **[!UICONTROL 类型]** 在右侧的下拉选择器中，选择 `web.webpagedetails.pageViews` 作为事件类型。

![选择事件类型。](/help/rtcdp/assets/partner-data/onsite-personalization/add-pageview-type-rule.png)

选择XDM数据旁边的数据库图标，然后选择 `pageVisit` 数据元素。

向下滚动操作配置列表，并确保选中标题为 **[!UICONTROL 呈现可视化个性化决策]**. 对于允许在网页上以可视方式呈现通过Adobe Target或其他类似产品交付的体验，这一点很重要。 选择 **[!UICONTROL 保留更改]**，然后 **[!UICONTROL 保存]** 规则。

![选中呈现可视化个性化决策复选框。](/help/rtcdp/assets/partner-data/onsite-personalization/render-visual-personalization-toggle.png)

#### 设置发布工作流程

要将此配置部署到网页，下一步是构建一个库，其中包含您刚刚创建的资源。 详细了解 [设置发布流](/help/tags/ui/publishing/publishing-flow.md).

选择 **[!UICONTROL 发布流]** 然后 **[!UICONTROL 添加库]**.

选择 **[!UICONTROL 添加所有更改的资源]**，为库命名，将环境设置为 **[!UICONTROL 开发]** 并选择 **[!UICONTROL 保存并生成到开发环境]**.

![创建库并部署到开发环境](/help/rtcdp/assets/partner-data/onsite-personalization/create-publishing-workflow.gif)

#### 测试您的网站

此时，应该使用Web SDK对您的网站进行全面检测。 要测试数据收集是否按预期工作，您可以导航到您的网站，并使用浏览器的开发人员工具来检查网络流量。

输入 `interact` 在搜索框中，刷新页面，此时您应该会看到从网站到Adobe Edge网络调用的填充结果。

![在开发人员工具中填充的网络事件视图。](/help/rtcdp/assets/partner-data/onsite-personalization/events-filtered.png)

### 个性化 {#personalization}

您现在可以创建并激活受众以进行个性化。

#### 设置边缘分段

设置 [边缘分割](/help/segmentation/ui/edge-segmentation.md) 因此，会在访客访问您的Web资产时实时评估访客的受众成员资格。

确保同时设置 [主动边缘合并策略](/help/destinations/ui/activate-edge-personalization-destinations.md#create-merge-policy) （对于Edge受众）。

#### 与Adobe Target或其他自定义个性化目标集成

现在，您可以与个性化引擎集成，向网站或应用程序访客显示个性化内容。 Adobe建议使用 [Adobe Target目标](/help/destinations/catalog/personalization/adobe-target-connection.md) 为了这个目的。

>[!IMPORTANT]
>
>阅读有关的教程 [将受众激活到边缘个性化目标](/help/destinations/ui/activate-edge-personalization-destinations.md) 完整查看激活受众所需的步骤。

## 限制和故障排除 {#limitations-and-troubleshooting}

在探索本页中描述的用例时，请注意以下限制：

* 如果您使用合作伙伴ID，请注意，在构建您的 [身份图](/help/identity-service/ui/identity-graph-viewer.md).

## 由合作伙伴数据支持实现的其他用例 {#other-use-cases}

探索通过 Real-Time CDP 中的合作伙伴数据支持实现的更多用例：

* [使用可信赖的数据合作伙伴的属性来补充第一方配置文件，以改善您的数据基础，获得对客户群的全新见解，并提升受众优化。](/help/rtcdp/partner-data/supplement-first-party-profiles.md)
* 在Real-Time CDP中使用第三方数据支持来 [使用数据合作伙伴提供的潜在客户配置文件扩大您的用户档案库，并与他们接洽，以争取或接触新客户](/help/rtcdp/partner-data/prospecting.md).
* （**即将推出**）[!BADGE Beta]{type=Informative}**扩大激活**&#x200B;使用合作伙伴 ID 发布不接受 PII 或哈希 PII 的生态系统。