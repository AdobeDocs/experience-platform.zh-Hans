---
title: 使用合作伙伴辅助的访客识别功能，为未知访客提供个性化的现场体验
description: 了解如何使用合作伙伴辅助的访客识别为访客营造个性化的现场体验。
feature: Use Cases, Personalization, Customer Acquisition
exl-id: 99677988-1df8-47b1-96b1-0ef6db818a1d
source-git-commit: f988d7665a40b589ca281d439b6fca508f23cd03
workflow-type: tm+mt
source-wordcount: '2568'
ht-degree: 72%

---

# 使用合作伙伴辅助的访客识别功能，为未知访客提供个性化的现场体验

>[!AVAILABILITY]
>
>已获得许可Real-Time CDP（应用程序服务）、Adobe Experience Platform Activation、Real-Time CDP、Real-Time CDP Prime、Real-Time CDP Ultimate的客户可以使用此功能。 阅读[产品说明](https://helpx.adobe.com/cn/legal/product-descriptions.html)中关于这些软件包的详细信息，并联系您的 Adobe 代表了解更多信息。

了解如何使用合作伙伴辅助的识别为您的 Web 资产访客营造个性化的体验。使用本教程了解为了向经过身份验证和未经身份验证的访客展现个性化体验，Experience Platform 和其他 Experience Cloud 解决方案中各个元素的实施顺序。

![一张信息图，其中描述如何使用合作伙伴提供的属性为访客营造个性化的体验。](/help/rtcdp/assets/partner-data/onsite-personalization/onsite-personalization-overview.png)

## 为什么考虑此用例 {#why-this-use-case}

随着消费者与品牌以各种方式互动，数字体验碎片化变得非常真实，并变得越来越难以解决。 用于具有凝聚力的体验、有针对性的推荐和量身定制的交互的最佳客户参与策略都受用户识别的约束。

在这种情况下，合作伙伴辅助的实时识别可以产生有意义的改变。 Adobe允许身份合作伙伴加入我们复杂的客户端数据收集和市场领先的体验优化产品，从第一次访问开始有效地提高体验交付标准，而无需先前历史记录或身份验证。

这对于身份验证率较低的垂直行业（如包装消费品、在线零售等）特别有用。

## 行业示例 {#industry-example}

以一个家装品牌为例，其身份验证率偏低。此品牌要为首次访客营造个性化的体验，其中既没有以前的历史记录或身份验证，也逐渐不再依靠第三方 Cookie。

此品牌选择利用合作伙伴识别技术以按概率识别访客并营造更加个性化的体验。当访客沿营销漏洞下移时，这样做有助于促使访客仔细考虑。例如，该品牌可能会使用合作伙伴提供的人口统计信号制作现场内容以吸引最近搬家的人，并为流行的 DIY 产品打折。

## 先决条件和规划 {#prerequisites-and-planning}

在规划使用合作伙伴提供的属性为经过身份验证和未经身份验证的访客营造个性化的体验时，请在规划过程中考虑以下先决条件：

* 您合作伙伴的识别技术期待哪些输入，以使其可叠加其他属性？
* 与确定性确认属性相比，您在多大程度上愿意根据概率派生的数据集在不同的渠道和不同用例中提供个性化？
* 预先经过身份验证但被识别的访客在身份验证后的体验应发生什么变化？

### 用户界面功能、Experience Platform组件以及您将使用的Experience Cloud产品 {#ui-functionality-and-elements}

要成功实施此用例，您必须使用 Real-Time Customer Data Platform 和其他 Experience Cloud 解决方案的多个区域。确保您拥有所有这些区域所需的[基于属性的访问控制权限](/help/access-control/abac/overview.md)，或让系统管理员授予您这些必要的权限。

* 数据收集
   * [Adobe Experience Platform Web SDK](/help/collection/js/js-overview.md)
   * [标记](/help/tags/home.md)
   * [数据流](/help/datastreams/overview.md)
* Real-Time CDP 中的数据管理
   * [身份标识](/help/identity-service/features/namespaces.md)
   * [架构](/help/xdm/home.md)
   * [数据使用情况标签](/help/data-governance/labels/overview.md)
   * [数据集](/help/catalog/datasets/overview.md)
* Web 资产个性化
   * [边缘分段](/help/segmentation/methods/edge-segmentation.md)
   * [边缘个性化目标](/help/destinations/destination-types.md#edge-personalization-destinations)
   * [Adobe Target](/help/destinations/catalog/personalization/adobe-target-connection.md)（或您选择的个性化平台。本用例教程重点介绍 Adobe Target 作为个性化引擎）

## 视频演练 {#video-walkthrough}

查看下面的视频教程，逐步了解如何为未知访客提供个性化的现场体验：

>[!VIDEO](https://video.tv.adobe.com/v/3423076/?learn=on)

## 如何实现该用例：高级概述 {#achieve-the-use-case-high-level}

![一张信息图，其中描述如何使用合作伙伴提供的属性为访客营造个性化的体验。](/help/rtcdp/assets/partner-data/onsite-personalization/onsite-personalization-steps.png)

1. 作为&#x200B;**客户**，您通过&#x200B;**数据合作伙伴**&#x200B;可实时洞察以其他方式匿名的网站访客。
2. 作为&#x200B;**客户**，您在资产上部署客户端库以调用&#x200B;**合作伙伴** API，并且您配置 Web SDK 或移动 SDK 以将合作伙伴提供的信号发送到 Real-Time CDP。
3. 当&#x200B;**访客**&#x200B;浏览您的网站或应用程序时，**合作伙伴**&#x200B;按概率识别访客，并返回属性和 ID。
4. Real-Time CDP 运行边缘分段以评估传入的事件点击，并根据 [ECID 标识符](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=zh-Hans)将结果保持不变。
5. Adobe Target 使用边缘分段输出将体验呈现回&#x200B;**访客**&#x200B;以供进行会话中个性化。
6. 事件完整地保存下来，用于分析和重新定位等下游工作流。

## 如何实现用例：分步说明 {#step-by-step-instructions}

通读以下部分（其中包括指向更多文档的链接）以完成上方高级概述中的每个步骤。

### 数据管理 - 创建身份标识命名空间、架构和数据集以管理数据属性 {#data-management}

为实现使未经身份验证的访客体验个性化的用例做准备时，您必须首先在 Real-Time CDP 中设置数据管理结构以接收传入的实时事件和受众资格筛选数据。

#### 创建合作伙伴 ID 身份标识命名空间

首先，您需要创建合作伙伴 ID 身份标识命名空间。导航到左边栏中的&#x200B;**[!UICONTROL Customer]** > **[!UICONTROL Identities]**，然后选择屏幕右上角的&#x200B;**[!UICONTROL Create identity namespace]**。

![“创建身份标识命名空间”对话框，其中突出显示合作伙伴 ID。](/help/rtcdp/assets/partner-data/onsite-personalization/create-identity-namespace.png)

详细阅读如何[创建合作伙伴 ID 身份标识命名空间](/help/rtcdp/partner-data/prospecting.md#create-partner-id-namespace)。

#### 创建架构

接下来，创建一个[!UICONTROL Experience Event]架构以保存您以后将从Web属性中收集的时间系列数据，并确保使用[!UICONTROL XDM ExperienceEvent]作为架构的基类。 阅读如何[使用 Experience Platform UI 创建架构](/help/xdm/ui/resources/schemas.md#create)。

![“架构”工作区，其中突出显示“创建架构”和“XDM ExperienceEvent”。](/help/rtcdp/assets/partner-data/onsite-personalization/create-experience-event-schema.png)

当您创建架构并[将字段组添加到该架构](/help/xdm/ui/resources/schemas.md#add-field-groups)时，请考虑添加[访问网页](/help/xdm/field-groups/event/web-details.md)和[身份标识映射](/help/xdm/field-groups/profile/identitymap.md)字段组。除此之外，还有其他字段组适用于您的数字资产和数据收集实践。

此外，还可创建或重用现有的字段组并将它添加到您的架构以捕获合作伙伴关于访客提供的洞察。阅读如何[创建字段组](/help/xdm/ui/resources/field-groups.md)和如何[将字段添加到字段组](/help/xdm/ui/resources/field-groups.md)。例如，如果预期要对照合作伙伴提供的洞察（如年龄范围、就业状况、月消费能力或购买行为）进行个性化，请让您的字段组加入相应的字段。

假设数据合作伙伴提供一个稳定的访客标识符，而您要将它引入到 Real-Time CDP 中，则务必在您的自定义字段组中为该标识符加入一个恰当命名的字段。您还应在早先创建的身份标识命名空间中将该字段标为身份标识。还要记得[使该架构可被包括在轮廓中](/help/xdm/ui/resources/schemas.md#profile)。

#### 创建数据集

接下来，您必须创建一个数据集以容纳您从您的 Web 资产访客收集、并将用于现场个性化的时间序列数据。

阅读有关[如何创建数据集](/help/catalog/datasets/user-guide.md#create)的教程，并记得选择从架构创建数据集的选项。根据您在上一步中创建的架构创建数据集。

与创建架构时的步骤类似，您需要启用数据集以包含在[!UICONTROL Real-Time Customer Profile]中。 有关启用数据集以在[!UICONTROL Real-Time Customer Profile]中使用的更多信息，请阅读[创建架构教程。](/help/xdm/tutorials/create-schema-ui.md#profile)

### 在您的 Web 资产上实施事件数据收集 {#implement-data-collection}

设置数据管理配置后，您现在需要在您的 Web 资产上实施实时事件[数据收集](/help/collection/home.md)。您需要使用Adobe数据收集库[!UICONTROL Web SDK]检测您的资产，以收集实时事件调用并将它们发送回Real-Time CDP。 此项由几个数据收集组件上的几个独立任务组成。

>[!IMPORTANT]
>
>要检索合作伙伴提供的属性，您还必须&#x200B;*将您的 Web 资产与合作伙伴 API 或其他方法集成以实时调用属性和从数据合作伙伴检索属性*。请与您选择的合作伙伴讨论这方面的内容，因为这不是本教程的主题。

首先，使用屏幕右上角的应用程序切换器导航到&#x200B;**[!UICONTROL Data Collection]**&#x200B;部分。

>[!TIP]
>
>如果您在应用程序切换器中看不到[!UICONTROL Data Collection]，请联系您的系统管理员以请求访问权限。

![应用程序切换器进入“数据收集”部分。](/help/rtcdp/assets/partner-data/onsite-personalization/app-switcher-data-collection.png)

UI的&#x200B;**[!UICONTROL Data Collection]**&#x200B;部分类似于以下图像。

Experience Platform UI的![数据收集部分。](/help/rtcdp/assets/partner-data/onsite-personalization/data-collection-home.png)

#### 创建数据流

作为数据收集部分中的第一步，[创建一个新的数据流](/help/datastreams/configure.md)。该数据流是如何收集数据并正确地传送到适当的 Adobe 应用程序（在本例中为 Experience Platform）的基础。

创建数据流时，在&#x200B;**[!UICONTROL Event schema]**&#x200B;字段中，选择您之前创建的架构。

![在配置新数据流时突出显示的事件架构选择器。](/help/rtcdp/assets/partner-data/onsite-personalization/event-schema-selector-datastream.png)

[从下拉菜单中选择您之前创建的事件数据集](/help/datastreams/configure.md#aep)，选中&#x200B;**[!UICONTROL Edge Segmentation]**&#x200B;和&#x200B;**[!UICONTROL Personalization Destinations]**&#x200B;旁边的复选框，然后选择&#x200B;**[!UICONTROL Save]**。

请注意，在此场景中您不必选择轮廓数据集，因为您引入的是基于事件的时间序列数据。

#### 创建标记属性

将某个资产设想为容器，在将标记部署到网站时将在其中填入扩展、规则、数据元素和库。

导航到&#x200B;**[!UICONTROL Tags]**&#x200B;并选择&#x200B;**[!UICONTROL New property]**。

![创建新的标记资产。](/help/rtcdp/assets/partner-data/onsite-personalization/create-tag-property.png)

填写必填字段并选择&#x200B;**[!UICONTROL Save]**。

![填写新资产的必填字段。](/help/rtcdp/assets/partner-data/onsite-personalization/tag-property-fields.png)

获取有关如何[创建标记资产](https://experienceleague.adobe.com/docs/platform-learn/implement-in-websites/configure-tags/create-a-property.html?lang=zh-Hans)的完整信息。

接下来，您必须在该资产内安装各种扩展。选择您的标记属性并导航到[!UICONTROL Extensions]部分。

![选择新的标记资产。](/help/rtcdp/assets/partner-data/onsite-personalization/select-tag-property.png)

请注意，已安装[!UICONTROL Core]扩展。 您必须安装另外两个扩展，如后续部分中所述。

![查看安装的扩展。](/help/rtcdp/assets/partner-data/onsite-personalization/view-existing-extensions.png)

#### 安装 Web SDK 扩展

请注意，本教程介绍如何用 Web SDK 为您的网站安装测量功能。还可在您的应用程序上使用[移动 SDK](https://developer.adobe.com/client-sdks/documentation/) 使您应用程序访客的体验个性化。

![在扩展目录中查看 Web SDK 扩展。](/help/rtcdp/assets/partner-data/onsite-personalization/web-sdk-extension.png)

在配置Web SDK的屏幕中，向下导航到&#x200B;**[!UICONTROL Datastreams]**&#x200B;部分，并提供有关您正在使用的Experience Platform沙盒的信息。 从下一个下拉列表中选择适当的沙盒和在前面的步骤中创建的数据流。您可以为所有其他环境选择相同的沙盒和数据流值。保持其他设置不变，并选择&#x200B;**[!UICONTROL Save]**。

获取有关[如何安装 Web SDK](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/tags-configuration/install-web-sdk.html?lang=zh-Hans) 的完整信息。

#### 安装 ID 服务扩展

使用 [Experience Cloud ID 服务扩展](/help/tags/extensions/client/id-service/overview.md)为所有 Experience Cloud 解决方案的访客创建基于设备的唯一第一方身份标识。在扩展目录中搜索&#x200B;**[!UICONTROL ID Service]**&#x200B;并进行安装。 安装扩展时保留所有默认设置。

![在扩展目录中查看 ID 服务扩展。](/help/rtcdp/assets/partner-data/onsite-personalization/id-service-extension.png)

#### 设置环境

接下来，从左侧导航转到&#x200B;**[!UICONTROL Environments]**&#x200B;部分。 在此步骤中，您必须将您的网站连接到 Adobe Edge Network 以实时检索和传送访客信息。

选择开发环境右侧的盒子图标，然后复制出现在一个模式窗口中的 JavaScript 代码片段的标准版本。

![选择在数据收集 UI 的“环境”部分中突出显示的盒子图标。](/help/rtcdp/assets/partner-data/onsite-personalization/select-box-icon.png)

必须将此代码片段添加到您网站的最顶部。因此，您的网站将调用 Adobe Edge Network 以检索将在页面上加载并执行的 JavaScript 逻辑。这样，访客 ID 生成、数据收集和实时体验个性化等功能即可正常工作。

#### 设置数据元素

数据元素是数据字典（即数据映射）的构建基块。单个数据元素就是一个变量，可将其值映射到查询字符串、URL、Cookie 值、JavaScript 变量等。详细阅读[数据元素](/help/tags/ui/managing-resources/data-elements.md)。

对于此用例，您必须设置两个数据元素。

首先，设置一个 `partnerData` 元素。导航到&#x200B;**[!UICONTROL Data Elements]**&#x200B;部分并选择&#x200B;**[!UICONTROL Create New Data Element]**。

![创建新数据元素。](/help/rtcdp/assets/partner-data/onsite-personalization/create-data-element.gif)

将数据元素命名为`partnerData`，将[!UICONTROL extension]值保留为[!UICONTROL Core]，并将&#x200B;**[!UICONTROL Data Element Type]**&#x200B;设置为&#x200B;**[!UICONTROL JavaScript Variable]**。 在标题为`partnerData`的字段中输入&#x200B;**[!UICONTROL JavaScript variable name]**&#x200B;并选择&#x200B;**[!UICONTROL Save]**。

![突出显示正确配置 partnerData 数据元素需要作出的选择。](/help/rtcdp/assets/partner-data/onsite-personalization/create-partnerdata-data-element.png)

要设置第二个数据元素，请命名新变量`pageVisit`，将&#x200B;**[!UICONTROL Extension]**&#x200B;设置为&#x200B;**[!UICONTROL Adobe Experience Platform]**&#x200B;并选择&#x200B;**[!UICONTROL XDM Object]**&#x200B;作为数据类型。

![突出显示正确配置 pageVisit 数据元素需要作出的选择。](/help/rtcdp/assets/partner-data/onsite-personalization/page-visit-data-element.png)

从“架构”中选择与预计从数据合作伙伴获得的值对应的第三方属性。然后，选择标题为&#x200B;**[!UICONTROL Provide entire object]**&#x200B;的单选按钮。 选择看起来像数据库的图标，然后选择您早先创建的 `partnerData` 数据元素。

#### 设置规则

在&#x200B;**[!UICONTROL Rules]**&#x200B;部分中，您可以配置网站以向Adobe发送个性化请求，并将属性加载到您刚刚创建的数据元素中。 详细阅读[创建规则](/help/tags/ui/managing-resources/rules.md)。

选择 **[!UICONTROL Create new Rule]**。为此规则命名&#x200B;**[!UICONTROL Personalize]**&#x200B;并选择&#x200B;**[!UICONTROL Events]**&#x200B;旁边的+号。 选择&#x200B;**[!UICONTROL Page Bottom]**&#x200B;作为事件并保存。

![选择规则的事件类型部分。](/help/rtcdp/assets/partner-data/onsite-personalization/add-events-rule.png)

选择&#x200B;**[!UICONTROL Actions]**&#x200B;旁边的+号。 将扩展更新为&#x200B;**[!UICONTROL Adobe Experience Platform Web SDK]**&#x200B;并将&#x200B;**[!UICONTROL Action Type]**&#x200B;设置为&#x200B;**[!UICONTROL Send event]**。

![选择规则的操作类型部分。](/help/rtcdp/assets/partner-data/onsite-personalization/add-action-rule.png)

从右侧的&#x200B;**[!UICONTROL Type]**&#x200B;下拉选择器中，选择`web.webpagedetails.pageViews`作为事件类型。

![选择事件类型。](/help/rtcdp/assets/partner-data/onsite-personalization/add-pageview-type-rule.png)

选择 XDM 数据旁边的数据库图标，然后选择 `pageVisit` 数据元素。

向下滚动操作配置列表，并确保选中标题为&#x200B;**[!UICONTROL Render visual personalization decisions]**&#x200B;的框。 这一点对于在网页上直观地呈现通过 Adobe Target 或其他类似产品投放的体验很重要。选择&#x200B;**[!UICONTROL Keep Changes]**，然后选择&#x200B;**[!UICONTROL Save]**&#x200B;规则。

![选中“呈现视觉个性化决策”复选框。](/help/rtcdp/assets/partner-data/onsite-personalization/render-visual-personalization-toggle.png)

#### 设置发布工作流

要将此配置部署到网页，下一步是构建一个库，其中包括您刚刚创建的资源。详细阅读[设置发布流](/help/tags/ui/publishing/publishing-flow.md)。

选择&#x200B;**[!UICONTROL Publishing Flow]**，然后选择&#x200B;**[!UICONTROL Add Library]**。

选择&#x200B;**[!UICONTROL Add all Changed Resources]**，为库命名，将环境设置为&#x200B;**[!UICONTROL Development]**&#x200B;并选择&#x200B;**[!UICONTROL Save & Build to Development]**。

![创建库并部署到开发环境](/help/rtcdp/assets/partner-data/onsite-personalization/create-publishing-workflow.gif)

#### 测试您的网站

此时，应已用 Web SDK 为您的网站完整地安装了测量功能。要测试数据收集是否如预期的那样正常工作，您可导航到您的网站，并使用浏览器的开发人员工具检查网络流量。

在搜索框中输入 `interact`，刷新页面，您应看到填入从您的网站到 Adobe Edge Network 的网络调用。

![在开发人员工具中查看填入网络事件。](/help/rtcdp/assets/partner-data/onsite-personalization/events-filtered.png)

### 个性化 {#personalization}

您现在已准备好创建个性化并为其激活受众。

#### 创建受众并设置边缘分段

在Experience Platform UI中，导航到&#x200B;**[!UICONTROL Customer]** > **[!UICONTROL Audiences]**&#x200B;并创建受众以捕获您的网站访客。

![查看如何导航到受众。](/help/rtcdp/assets/partner-data/onsite-personalization/navigate-to-audiences.png)

您必须使用[边缘分段](/help/segmentation/methods/edge-segmentation.md)设置受众，以便在访客访问您的Web资产时实时评估访客的受众成员资格。

确保还要为边缘受众设置一个[活动边缘合并策略](/help/destinations/ui/activate-edge-personalization-destinations.md#create-merge-policy)。

#### 与 Adobe Target 或其他自定义个性化目标集成

您现在已准备好与个性化引擎集成，以向您的网站或应用程序访客显示个性化内容。Adobe 建议为此用途使用 [Adobe Target 目标](/help/destinations/catalog/personalization/adobe-target-connection.md)。

>[!IMPORTANT]
>
>阅读有关[将受众激活到边缘个性化目标](/help/destinations/ui/activate-edge-personalization-destinations.md)的教程，以便完整地了解激活受众所需的步骤。

## 限制和故障排除 {#limitations-and-troubleshooting}

在探索本页中描述的用例时，请注意以下限制：

* 如果您使用合作伙伴 ID，请注意在构建您的[身份标识图](/help/identity-service/features/identity-graph-viewer.md)时不会使用这些 ID。

## 由合作伙伴数据支持实现的其他用例 {#other-use-cases}

探索通过 Real-Time CDP 中的合作伙伴数据支持实现的更多用例：

* [用受信任的数据合作伙伴提供的属性补充第一方轮廓](/help/rtcdp/partner-data/supplement-first-party-profiles.md)，以改善您的数据基础、洞察客户群的新情况并获得更好的受众优化。
* 使用 Real-Time CDP 中的第三方数据支持，[通过数据合作伙伴提供的潜在客户轮廓扩充您的轮廓基础并与其交流以获取或接触新客户](/help/rtcdp/partner-data/prospecting.md)。
* [扩大了潜在客户轮廓和潜在客户受众的激活范围](/help/destinations/ui/activate-prospect-audiences.md)，以选择目标。
