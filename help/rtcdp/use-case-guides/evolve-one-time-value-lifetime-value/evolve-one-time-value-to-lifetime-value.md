---
title: 将一次性客户价值提升至存留期价值
description: 了解如何根据特定客户的属性、行为和过去购买情况创建个性化促销活动，以提供最佳的补充性产品或服务。
feature: Use Cases
exl-id: 45f72b5e-a63b-44ac-a186-28bac9cdd442
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '3181'
ht-degree: 26%

---

# 将一次性客户价值提升至存留期价值

>[!IMPORTANT]
> 
>* 本页介绍Real-Time CDP和Adobe Journey Optimizer的示例实施，以实现所述的用例。 使用页面上提供的数字、资格标准和其他字段作为指南，而不是规范性数字。
>* 要完成此用例，您需要获得Real-Time CDP和Adobe Journey Optimizer的许可。 请在下面的[先决条件和规划部分](#prerequisites-and-planning)中阅读更多信息。

实施一次性客户价值对存留期价值用例以提高品牌参与度和品牌忠诚度。 借助Experience Platform的强大功能(通过[Real-Time CDP](/help/rtcdp/home.md)和[Journey Optimizer](https://experienceleague.adobe.com/zh-hans/docs/journey-optimizer/using/ajo-home)增强)，在多个渠道或历程上构建连接的客户体验。

您定位的角色是最近三个月内购买过一些产品的罕见访客。

考虑一下这些访问您的资产并偶尔购买您提供的产品或服务的客户。 您可能需要创建个性化的促销活动以吸引这些客户，这样您的品牌可以为他们提供更长期的价值，而不是一次性价值。 了解如何：

* 收集和管理数据
* 创建受众
* 创建历程以在Adobe Journey Optimizer中定位这些受众，并在Real-Time CDP中激活它们。

![逐步将一次性值转换为生命周期值高级视觉概览。](../evolve-one-time-value-lifetime-value/images/diagram-business-use-case.png){zoomable="yes"}

## 先决条件和规划 {#prerequisites-and-planning}

考虑到您已在内部定义了提高品牌忠诚度的业务目标和目的。 这可以转换为执行用例以提高客户参与度和忠诚度。

要实现此目的，所需技术包含两个Experience Platform应用程序[Real-Time CDP](https://experienceleague.adobe.com/docs/experience-platform/rtcdp/overview.html?lang=zh-Hans)和[Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/get-started/get-started.html?lang=zh-Hans)。 下面列出了您在实施用例时将使用的两个应用程序中的各种功能和UI元素。

>[!TIP]
>
>确保您拥有所有这些区域所需的[基于属性的访问控制权限](/help/access-control/abac/end-to-end-guide.md)，或让系统管理员授予您这些必要的权限。

* [[!DNL Adobe Real-Time Customer Data Platform (Real-Time CDP)]](https://experienceleague.adobe.com/docs/platform-learn/tutorials/rtcdp/understanding-the-real-time-customer-data-platform.html?lang=zh-Hans)：跨数据源集成数据以推动营销活动。 然后，该数据可用于创建活动受众，并显示电子邮件和网络促销图块中使用的个性化数据元素（例如，姓名或与帐户相关的信息）。最后，Real-Time CDP还可用于将受众激活到付费媒体目标。
   * [架构](/help/xdm/home.md)
   * [轮廓](/help/profile/home.md)
   * [数据集](/help/catalog/datasets/overview.md)
   * [受众](/help/segmentation/home.md)
   * [目标](/help/destinations/home.md)
* [[!DNL Adobe Journey Optimizer]](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/journey.html?lang=zh-Hans)：设计历程、设置触发器并创建正确的消息以向访客发送地址。
   * [事件或受众触发器](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioning/collect-event-data/data-collection.html?lang=zh-Hans)
   * [受众和活动](https://experienceleague.adobe.com/docs/journey-optimizer/using/audiences-profiles-identities/audiences/about-audiences.html?lang=zh-Hans)
   * [历程](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/journey.html?lang=zh-Hans)

## Real-Time CDP和Journey Optimizer架构

以下是Real-Time CDP和Journey Optimizer各个组件的高级架构视图。 此图显示了数据如何流经两个Experience Platform应用程序，从数据收集到通过历程或营销活动激活到目标的点，以实现本页面上描述的使用案例。

![架构高级可视化概述。](/help/rtcdp/use-case-guides/evolve-one-time-value-lifetime-value/images/architecture-diagram.png){zoomable="yes"}

## 如何实现该用例：高级概述 {#achieve-the-use-case-high-level}

以下是工作流的高级概述，以及历程工作流和激活工作流的组合。

在下图所示的示例工作流中，您将查找符合特定标准的客户，并且您希望引诱他们返回您的网站或应用程序。 您打算在旅程中设置这些变量，这样，这些变量将以更频繁的方式返回，而不是在您的资产上有限地执行活动。 您正尝试让他们返回到您的资产，一旦他们回来，您就会让他们进入旅程，在您的网站上进行经常性购买。 此处设置的营销活动限制为每月与客户进行一次接触。

首先，向高价值和低频率客户的受众发送一条消息。 然后，检查他们是否在过去三十天内收到此消息。 如果没有，则您可以将他们输入历程，例如关于新订阅计划的历程。 然后，您可以等待几天（在本示例中为7天）。 之后，如果他们尚未购买您向其发送消息的订阅，则可以通过目标投放付费媒体广告。 如果他们已购买订阅，您可以让他们输入订单确认历程，从而完成用例。

>[!IMPORTANT]
>
>如下面的内容所述，通过在您的架构中设置[专用同意字段组](#customer-attributes-schema)和[实施同意策略](#privacy-consent)，所有操作和工作流均以隐私和同意优先的方式实施。

>[!BEGINSHADEBOX]

![逐步将一次性值转换为生命周期值高级视觉概览。](../evolve-one-time-value-lifetime-value/images/step-by-step.png){zoomable="yes"}

1. 创建架构和数据集，然后为[!UICONTROL 配置文件]标记这些架构和数据集。
2. 通过Web SDK、Mobile Edge SDK或API收集数据并集成到Experience Platform中。 也可以使用分析数据连接器，但可能会导致历程延迟。
3. 您将轮廓加载到 Real-Time CDP 中，并制定治理策略来确保负责任的使用。
4. 您可以从用户档案列表中构建重点受众，以检查高值和低值客户。
5. 您在[!DNL Adobe Journey Optimizer]中创建两个历程，一个用于向用户发送有关新订阅计划的消息，另一个用于稍后向其发送消息以确认购买。
6. 如有需要，您可以激活尚未购买订阅的客户受众，使其访问所需的付费媒体目标。

>[!ENDSHADEBOX]

## 如何实现用例 {#achieve-use-case-instruction}

要完成上述高级概述中的每个步骤，请阅读以下部分，这些部分提供了指向更多信息和更详细说明的链接。

### 您将会使用的 UI 功能和元素 {#ui-functionality-and-elements}

当您完成实施用例的步骤时，您将使用本文档开头列出的Real-Time CDP、Adobe Journey Optimizer功能和UI元素。 确保您拥有所有这些区域所需的基于属性的访问控制权限，或让系统管理员授予您这些必要的权限。

### 创建架构设计并指定字段组 {#schema-design}

体验数据模型 (XDM) 资源在 [!DNL Adobe Experience Platform] 的[!UICONTROL “架构”]工作区中进行管理。您可以查看和浏览[!DNL Adobe]提供的核心资源（例如，[!UICONTROL 字段组]），并为您的组织创建自定义资源和架构。

有关创建[架构](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=zh-Hans)的更多信息，请阅读[“创建架构教程”。](/help/xdm/tutorials/create-schema-ui.md)

在此示例实施中，可为用例使用多种架构设计以将一次性值演化为生命周期值。 每个架构都包含要设置的特定必填字段，以及一些建议的字段。

根据实施示例，Adobe建议您创建以下三个架构来完成此用例：

* [客户属性架构](#customer-attributes-schema) （配置文件架构）
* [客户数字交易架构](#customer-digital-transactions-schema) （体验事件架构）
* [客户离线交易架构](#customer-offline-transactions-schema) （体验事件架构）

#### 客户属性架构 {#customer-attributes-schema}

使用此架构可构建和引用构成客户信息的用户档案数据。 这些数据通常通过您的 CRM 或类似系统摄入 [!DNL Adobe Experience Platform] 中，并且是引用用于个性化、营销同意和增强分段功能的客户详细信息所必需的。

![字段组突出显示的客户属性架构](/help/rtcdp/use-case-guides/evolve-one-time-value-lifetime-value/images/customer-attributes-schema.png)

客户属性架构由 [!UICONTROL XDM 个人轮廓]类表示，该类包括以下字段组：

+++人口统计详细信息（字段组）

[人口统计详细信息](/help/xdm/field-groups/profile/demographic-details.md)是 XDM 个人轮廓类的标准架构字段组。该字段组提供根级人员对象，其子字段描述的是有关个人的信息。

+++

+++个人联系方式（字段组）

[个人联系人详细信息](/help/xdm/field-groups/profile/personal-contact-details.md)是XDM个人资料类的标准架构字段组，用于描述个人联系信息。

+++

+++外部源系统审计详细信息（字段组）

[外部来源系统审计属性](/help/xdm/data-types/external-source-system-audit-attributes.md)是一种标准体验数据模型 (XDM) 数据类型，用于捕获有关外部来源系统的审核详细信息。

+++

+++同意和偏好设置字段组（字段组）

[同意和偏好设置](/help/xdm/field-groups/profile/consents.md)字段组提供单个对象类型字段同意，以捕获同意和偏好设置信息。

+++

#### 客户数字交易架构 {#customer-digital-transactions-schema}

此架构用于构建和引用构成您的客户活动的事件数据，这些活动发生在您的网站或其他关联的数字平台上。 此数据通常通过[Web SDK](/help/web-sdk/home.md)摄取到[!DNL Adobe Experience Platform]中，并且是引用各种浏览和转化事件所必需的，这些事件用于触发历程、详细的在线客户分析和增强的分段功能。

![突出显示字段组的客户数字交易架构](/help/rtcdp/use-case-guides/evolve-one-time-value-lifetime-value/images/customer-digital-transactions-schema.png)

客户数字交易架构由 [!UICONTROL XDM ExperienceEvent] 类表示，其中包括以下字段组：

+++Adobe Experience Platform Web SDK ExperienceEvent（字段组）

| 字段 | 要求 |
| --- | --- |
| `device.model` | 建议 |
| `environment.browserDetails.userAgent` | 建议 |

+++

+++Web 详细信息（字段组）

[Web详细信息](/help/xdm/field-groups/event/web-details.md)是XDM ExperienceEvent类的标准架构字段组，用于描述有关Web详细信息事件的信息，例如交互、页面详细信息和反向链接。

+++

+++消费者体验事件（字段组）

此字段组包含有关用户在您的Web资产上执行的操作（如购买或浏览事件）的各种信息。

| 字段 | 要求 |
| --- | --- |
| `commerce.cart.cartID` | 建议 |
| `commerce.cart.cartSource` | 建议 |
| `commerce.cartAbandons.id` | 建议 |
| `commerce.cartAbandons.value` | 建议 |
| `commerce.order.orderType` | 建议 |
| `commerce.order.payments.paymentAmount` | 建议 |
| `commerce.order.payments.paymentType` | 建议 |
| `commerce.order.payments.transactionID` | 建议 |
| `commerce.order.priceTotal` | 建议 |
| `commerce.order.purchaseID` | 建议 |
| `commerce.productListAdds.id` | 建议 |
| `commerce.productListAdds.value` | 建议 |
| `commerce.productListOpens.id` | 建议 |
| `commerce.productListOpens.value` | 建议 |
| `commerce.productListRemoval.id` | 建议 |
| `commerce.productListRemoval.value` | 建议 |
| `commerce.productListViews.id` | 建议 |
| `commerce.productListViews.value` | 建议 |
| `commerce.productViews.id` | 建议 |
| `commerce.productViews.value` | 建议 |
| `commerce.purchases.id` | 建议 |
| `commerce.purchases.value` | 建议 |
| `marketing.campaignGroup` | 建议 |
| `marketing.campaignName` | 建议 |
| `marketing.trackingCode` | 建议 |
| `productListItems.name` | 建议 |
| `productListItems.priceTotal` | 建议 |
| `productListItems.product` | 建议 |
| `productListItems.quantity` | 建议 |

+++

+++最终用户 ID 详细信息（字段组）

[最终用户ID详细信息](/help/xdm/field-groups/event/enduserids.md)字段组包含有关您的用户的各种信息，例如访问时他们是否在您的网站上进行了身份验证，以及有关其身份的信息。

+++

+++外部源系统审计详细信息（字段组）

外部来源系统审计属性是一种标准体验数据模型 (XDM) 数据类型，用于捕获有关外部来源系统的审核详细信息。

+++

#### 客户离线交易架构 {#customer-offline-transactions-schema}

此架构用于构建和引用构成您的网站之外的平台上发生的客户活动的事件数据。此数据通常从POS（或类似系统）摄取到[!DNL Adobe Experience Platform]中，并且通常通过API连接流式传输到Experience Platform中。 了解[批次摄取](/help/ingestion/batch-ingestion/getting-started.md)。 其目的是引用各种线下转化事件，以用于触发历程、深入的线上和线下客户分析以及增强的分段能力。

![突出显示字段组的客户离线交易架构](/help/rtcdp/use-case-guides/evolve-one-time-value-lifetime-value/images/customer-offline-transactions-schema.png)

客户离线交易架构由 [!UICONTROL XDM ExperienceEvent] 类表示，其中包括以下字段组：

+++商务详细信息（字段组）

[Commerce详细信息](/help/xdm/field-groups/event/commerce-details.md)是[!DNL XDM ExperienceEvent]类的标准架构字段组，用于描述商业数据，如产品信息（SKU、名称、数量）和标准购物车操作（订单、结帐、放弃）。

+++

+++个人联系方式（字段组）

[[!UICONTROL 个人联系人详细信息]](/help/xdm/field-groups/profile/personal-contact-details.md)是[!DNL XDM Individual Profile]类的标准架构字段组，用于描述个人联系信息。

+++

+++外部源系统审计详细信息（字段组）

外部来源系统审计属性是一种标准体验数据模型 (XDM) 数据类型，用于捕获有关外部来源系统的审核详细信息。

+++

#### Adobe Web 连接器架构 {#adobe-web-connector-schema}

>[!NOTE]
>
>如果您使用的是 [!DNL Adobe Analytics Data Connector]，则这是一个可选的实施。

此架构用于构建和引用构成您的客户活动的事件数据，这些活动发生在您的网站或其他关联的数字平台上。 此架构与客户数字交易架构类似，不同之处在于，当Web SDK不是数据收集的选项时，此架构可以。 因此，当您利用[!DNL Adobe Analytics Data Connector]将在线数据作为主数据流或辅助数据流发送到[!DNL Adobe Experience Platform]时，可以使用此架构。

![字段组突出显示的Adobe Web连接器架构](/help/rtcdp/use-case-guides/evolve-one-time-value-lifetime-value/images/adobe-web-schema.png)

[!DNL Adobe]Web 连接器架构由 [!UICONTROL XDM 体验事件]类表示，其中包括以下字段组：

+++Adobe Analytics ExperienceEvent 模板（字段组）

[[!UICONTROL Adobe Analytics ExperienceEvent完整扩展]](/help/xdm/field-groups/event/analytics-full-extension.md)是一个标准架构字段组，用于捕获Adobe Analytics收集的常见指标。

+++

### 从架构创建数据集 {#dataset-from-schema}

数据集是对一组数据的存储和管理结构。用于完成此示例实施的每个架构都有一个数据集。

有关如何从架构创建[数据集](/help/catalog/datasets/overview.md)的更多信息，请阅读[数据集 UI 指南。](/help/catalog/datasets/user-guide.md)。

>[!NOTE]
>
>与架构创建步骤类似，您需要使数据集包含在实时客户轮廓中。有关启用数据集以在实时客户轮廓中使用的更多信息，请参阅[创建架构教程。](/help/xdm/tutorials/create-schema-ui.md#profile)

### 隐私、同意和数据治理 {#privacy-consent}

#### 同意政策

>[!IMPORTANT]
>
>向客户提供取消订阅以停止从品牌接收通信的功能，以及确保遵循此选择是一项法律要求。 通过[隐私法规概述](https://experienceleague.adobe.com/docs/experience-platform/privacy/regulations/overview.html?lang=zh-Hans)了解有关适用法律的更多信息。

考虑实施以下[同意政策](https://experienceleague.adobe.com/docs/platform-learn/data-collection/web-sdk/consent/overview.html?lang=zh-Hans)，并在联系访客之前请求其同意：

* 如果 `consents.marketing.email.val = "Y"`，则可以发送电子邮件
* 如果 `consents.marketing.sms.val = "Y"`，则可以发送短信
* 如果 `consents.marketing.push.val = "Y"`，则可以推送
* 如果 `consents.share.val = "Y"`，则可以发布广告

#### 数据治理标签和执行

考虑添加并强制实施以下[数据管理标签](/help/data-governance/labels/overview.md)：

* 个人电子邮件地址用作直接可识别数据，用于识别或联系特定个人而不是设备。
   * `personalEmail.address = I1`

#### 营销政策

您在此用例中创建历程不需要[营销策略](/help/data-governance/policies/overview.md)。 但是，您可以根据需要考虑以下策略：

* 限制敏感数据
* 限制现场广告
* 限制电子邮件定位
* 限制跨站点定位
* 限制将直接可识别数据与匿名数据相结合

### 创建受众 {#create-audiences}

此用例要求您创建两个受众以定义由配置文件存储中的配置文件子集共享的特定属性或行为，从而区分可营销的人员群体。 在Adobe Experience Platform中，可以通过多种方式创建受众：

* 有关如何创建受众的信息，请阅读[受众服务UI指南](https://experienceleague.adobe.com/docs/experience-platform/segmentation/ui/overview.html?lang=zh-Hans#create-audience)。
* 有关如何构建[受众](/help/segmentation/home.md)的信息，请阅读[受众构建UI指南](/help/segmentation/ui/audience-composition.md)。
* 有关如何通过Experience Platform派生的区段定义构建受众的信息，请阅读[Audience Builder UI指南](/help/segmentation/ui/segment-builder.md)。

具体而言，您必须在用例的不同步骤中创建和使用两个受众，如下图所示。

![受众已突出显示。](/help/rtcdp/use-case-guides/evolve-one-time-value-lifetime-value/images/audiences-highlighted-in-diagram.png){zoomable="yes"}

>[!BEGINTABS]

>[!TAB Adobe Journey Optimizer合格受众]

此高价值低频率受众包括您希望通过历程联系到的用户档案，以便告知他们新的订阅计划。 受众详细信息如下：

* 描述：过去3个月内总计花费超过$250的用户档案
* 受众中需要的字段和条件：
   * 事件： `commerce.order.payments.paymentamount`
*总和：>= $250
   * 事件类型： `commerce.purchases`
*时间戳：距现在不到3个月


>[!TAB 付费媒体受众]

创建此受众是为了包含过去3个月内总计花费超过$250且过去7天内未购买过的用户档案。 受众详细信息如下：

* 描述：过去3个月内总计花费超过$250且过去7天内未购买过产品的用户档案。
* 所需字段和条件：
   * 事件类型： `journey.feedback`
      * 操作数： = true
   * 事件：`experience.journeyOrchestration.stepEvents.nodeName`
      * 操作数： = JourneyStepEventTracker — 未购买订阅
      * 时间戳：最近7天
   * EventType不是： `commerce.purchases`
      * 时间戳：&lt;= 7天前（现在）
   * 事件：SKU
      * 值： = `subscription`

>[!ENDTABS]

### Adobe Journey Optimizer 中的历程设置 {#journey-setup}

>[!NOTE]
>
>[!DNL Adobe Journey Optimizer] 并不涵盖图中所示的所有内容。所有[付费媒体广告](/help/destinations/catalog/social/overview.md)都是在[!UICONTROL 目标] [工作区](/help/destinations/ui/destinations-workspace.md)中创建的。

[[!DNL Adobe Journey Optimizer]](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/journey.html?lang=zh-Hans) 可帮助您为客户提供贴合心意的、上下文和个性化的体验。客户历程是客户与品牌互动的整个过程。每个用例历程都需要特定信息。

要完成此用例，您必须创建两个单独的历程：

* 生命周期历程，包括您发送给高价值、低频率客户的消息
* 响应您的呼叫并购买订阅的用户的订单确认历程。

![历程已突出显示。](/help/rtcdp/use-case-guides/evolve-one-time-value-lifetime-value/images/journeys-highlighted-in-diagram.png){zoomable="yes"}

下面列出的是每个历程分支所需的精确数据。

>[!BEGINTABS]

>[!TAB 生命周期历程]

存留期历程面向过去30天内未定位的高价值和低频率客户的受众。 系统向这些客户显示一条消息，如果7天后仍未购买，您可以将非购买者包含在受众中，您可以向其显示付费媒体广告。 如果确实有购买行为，则可以在订单确认历程中设置购买者，详细内容见单独的选项卡。

![生命周期历程高级可视化概述。](/help/rtcdp/use-case-guides/evolve-one-time-value-lifetime-value/images/lifetime-journey.png "生命周期历程的一次性值高级可视化概述。"){zoomable="yes"}

+++详细的历程逻辑

上面显示的历程遵循以下逻辑。

1. 读取受众：对于在上面的受众部分中创建的第一个受众，使用[读取受众活动](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/read-audience.html?lang=zh-Hans)。

2. 条件 — 首选渠道：使用[条件活动](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/condition-activity.html?lang=zh-Hans)来确定如何通过电子邮件、短信或推送通知联系客户。 使用三个操作活动创建三个分支。

3. 等待：使用[等待活动](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/read-audience.html?lang=zh-Hans)等待直至您侦听购买。

4. 条件 — 过去7天内购买的订阅？使用条件活动可侦听过去七天内的产品购买。

5. JourneyStepEventTracker — 未购买订阅：对尚未购买订阅的访客使用[自定义操作](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/using-custom-actions.html?lang=zh-Hans)，即使收到您的消息。 作为历程结束时的自定义条件的一部分，创建一个`journey.feedback`事件并将其添加到基于[!UICONTROL 历程步骤事件]架构的数据集。 您将使用此事件对尚未购买订阅且可通过付费媒体广告定位的受众进行分段。

+++

>[!TAB 订购确认历程]

订单确认历程侧重于是通过网站还是通过移动设备应用程序进行购买。 例如，在客户成功完成购买（例如与贵公司的订购）后，您可以在订单确认历程中设置它们。

![客户订购确认历程高级视觉概述。](/help/rtcdp/use-case-guides/evolve-one-time-value-lifetime-value/images/order-confirmation-journey.png "客户订购确认历程高级视觉概述。"){zoomable="yes"}

+++历程逻辑

在确认历程中使用以下建议的事件、字段和操作：

* 历程由在线购买事件触发
   * 架构：客户数字交易
   * 字段：
      * `EventType`
   * 条件：
      * `EventType = commerce.purchases`
      * 字段：
         * `Commerce.purchases.id`
         * `Commerce.purchases.value`
         * `eventType`
         * `identityMap.authenticatedState`
         * `identityMap.id`
         * `identityMap.primary`
         * `productListItems.SKU`
         * `productListItems.currencyCode`
         * `productListItems.name`
         * `productListItems.priceTotal`
         * `productListItems.product`
         * `productListItems.productImageUrl`
         * `productListItems.quantity`
         * `timestamp`
         * `endUserIDs._experience.emailid.authenticatedState`
         * `endUserIDs._experience.emailid.id`
         * `endUserIDs._experience.emailid.namespace.code`
         * `_id`

+++

+++关键历程逻辑

* 历程进入逻辑
   * 订购事件

* 条件
   * 选择Target渠道（您可以选择一个或多个渠道来扩大范围）。
      * 订单确认本质上是一种服务，因此通常不需要检查同意情况。
      * 电子邮件
      * 推送
      * 短信

   * 渠道内容个性化
      * 显示订购详细信息，并可以使用表格格式显示产品列表。

+++

>[!ENDTABS]

有关在[!DNL Adobe Journey Optimizer]中创建历程的更多信息，请阅读[历程入门](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/journey.html?lang=zh-Hans)指南。

### 设置显示付费媒体广告的目标 {#paid-media-ads}

某些用户可能尚未购买您的订阅，即使您向他们发送有关新计划的消息也是如此。 在等待多天（在此示例用例中为7天）后，您可以决定向这些用户显示付费媒体广告，以鼓励他们购买您的订阅。

对付费媒体广告使用Real-Time CDP中的目标框架。 从众多可用的广告目标中选择一个向您的客户显示付费媒体广告，并将您[之前创建的](#create-audiences)付费媒体受众激活到您选择的目标。 查看可用[广告](/help/destinations/catalog/advertising/overview.md)和[社交](/help/destinations/catalog/social/overview.md)目标的概述。

要了解如何将数据激活到目标(例如[The Trade Desk](/help/destinations/catalog/advertising/tradedesk.md)或[Google Customer Match](/help/destinations/catalog/advertising/google-customer-match.md))，请阅读以下文档：

* [创建新的目标连接](/help/destinations/ui/connect-destination.md)
* [将受众数据激活到流式受众导出目标](/help/destinations/ui/activate-segment-streaming-destinations.md)

## 后续步骤 {#next-steps}

通过在历程中设置低频率和高价值用户，并向部分用户显示付费媒体广告，您有望将部分用户从一次性价值转变为终生价值客户，从而提高品牌忠诚度和客户参与量度。

接下来，您可以探索Real-Time CDP支持的其他用例，例如[智能地重新吸引客户](/help/rtcdp/use-case-guides/intelligent-re-engagement/intelligent-re-engagement.md)或[在您的Web资产上向未经身份验证的用户显示个性化内容](/help/rtcdp/partner-data/onsite-personalization.md)。
