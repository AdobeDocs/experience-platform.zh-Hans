---
title: 智能重新参与
description: 在关键转化时刻提供引人注目的互联体验，以智能的方式重新吸引不常光顾的客户。
exl-id: 13f6dbc9-7471-40bf-824d-27922be0d879
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '3424'
ht-degree: 100%

---

# 以智能的方式重新吸引客户回归

在以明智且负责任的方式重新吸引在完成转化之前放弃转化的客户。通过体验而不是提醒来吸引流失的客户，以提高转化率并推动客户存留期值的增长。

采用实时考虑内容，考虑消费者的所有品质和行为，并根据线上和线下事件快速提供重新资格认证。

![逐步智能重新参与高级视觉概述。](../intelligent-re-engagement/images/step-by-step.png)

## 用例概述

在研究重新参与历程的示例时，您将会构建架构、数据集和受众。您还会在 [!DNL Adobe Journey Optimizer] 中发现设置示例历程所需的功能，以及在目标内创建付费媒体广告所需的功能。本指南使用了重新吸引客户参与下面概述的用例历程的示例：

* **重新参与历程**——针对放弃在网站和移动应用程序上浏览产品的客户。
* **放弃的购物车历程**——已将产品放入购物车，但尚未在网站和移动应用程序上购买的客户。
* **订购确认历程**——侧重于通过网站和移动应用程序购买的产品。

## 先决条件和规划 {#prerequisites-and-planning}

在完成实施用例的步骤后，您将使用以下 Real-Time CDP 功能和 UI 元素（按使用顺序列出）。确保您拥有所有这些区域所需的基于属性的访问控制权限，或让系统管理员授予您这些必要的权限。

* [[!DNL Adobe Real-Time Customer Data Platform (Real-Time CDP)]](https://experienceleague.adobe.com/docs/platform-learn/tutorials/rtcdp/understanding-the-real-time-customer-data-platform.html)——跨数据源集成数据，以推动活动。然后，该数据可用于创建活动受众，并显示电子邮件和网络促销图块中使用的个性化数据元素（例如，姓名或与帐户相关的信息）。CDP 还可用于通过电子邮件和网络激活受众（通过 [!DNL Adobe Target]）。
   * [架构](/help/xdm/home.md)
   * [配置文件](/help/profile/home.md)
   * [数据集](/help/catalog/datasets/overview.md)
   * [受众](/help/segmentation/home.md)
   * [[!DNL Adobe Journey Optimizer]](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/journey.html)
   * [目标](/help/destinations/home.md)
   * [事件或受众触发器](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioning/collect-event-data/data-collection.html)
   * [受众/事件](https://experienceleague.adobe.com/docs/journey-optimizer/using/audiences-profiles-identities/audiences/about-audiences.html)
   * [历程操作](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/journey.html)

### 如何实现该用例：高级概述 {#achieve-the-use-case-high-level}

以下是三个重新参与历程示例的高级概述。

>[!BEGINTABS]

>[!TAB 重新参与历程]

重新参与历程的目标是放弃在网站和移动应用程序上浏览产品的情况。当产品已被查看但未购买或添加到购物车时，会触发此历程。如果过去 24 小时内没有添加列表，则三天后会触发品牌参与功能。<p>![客户智能重新参与历程高级视觉概述。](../intelligent-re-engagement/images/re-engagement-journey.png "客户智能重新参与历程高级视觉概述。"){width="2560" zoomable="yes"}</p>

1. 您创建架构和数据集，然后标记[!UICONTROL 配置文件]。
2. 数据通过 Web SDK、Mobile Edge SDK 或 API 集成到 Experience Platform。也可以使用分析数据连接器，但可能会导致历程延迟。
3. 您将配置文件加载到 Real-Time CDP 中，并制定治理策略来确保负责任的使用。
4. 您从配置文件列表中构建重点受众，以检查&#x200B;**客户**&#x200B;是否在过去三天内参与了活动。
5. 您在 [!DNL Adobe Journey Optimizer] 中创建一个重新参与历程。
6. 如果需要，请与&#x200B;**数据合作伙伴**&#x200B;合作，以将受众激活到所需的付费媒体目标。
7. [!DNL Adobe Journey Optimizer] 检查是否同意，并发送配置的各种操作。

>[!TAB 放弃的购物车历程]

放弃的购物车历程针对的是在网站和移动应用程序上，已放入购物车但尚未购买的产品。此外，付费媒体活动可以使用此方法启动和停止。<p>![客户放弃的购物车历程高级视觉概述。](../intelligent-re-engagement/images/abandoned-cart-journey.png "客户放弃的购物车历程高级视觉概述。"){width="2560" zoomable="yes"}</p>

1. 您创建架构和数据集，然后标记[!UICONTROL 配置文件]。
2. 数据通过 Web SDK、Mobile Edge SDK 或 API 集成到 Experience Platform。也可以使用分析数据连接器，但可能会导致历程延迟。
3. 您将配置文件加载到 Real-Time CDP 中，并制定治理策略来确保负责任的使用。
4. 您从配置文件列表中建立重点受众，以检查&#x200B;**客户**&#x200B;是否已将商品放入购物车，但尚未完成购买。**[!UICONTROL 添加到购物车]**&#x200B;事件会启动一个等待 30 分钟的计时器，然后检查购买情况。如果没有购买，那么该&#x200B;**客户**&#x200B;会被添加到&#x200B;**[!UICONTROL 放弃的购物车]**&#x200B;受众中。
5. 您在 [!DNL Adobe Journey Optimizer] 中创建一个放弃的购物车之历程。
6. 如果需要，请与&#x200B;**数据合作伙伴**&#x200B;合作，以将受众激活到所需的付费媒体目标。
7. [!DNL Adobe Journey Optimizer] 检查是否同意，并发送配置的各种操作。

>[!TAB 订购确认历程]

订购确认历程侧重于通过网站和移动应用程序购买的产品。<p>![客户订购确认历程高级视觉概述。](../intelligent-re-engagement/images/order-confirmation-journey.png "客户订购确认历程高级视觉概述。"){width="2560" zoomable="yes"}</p>

1. 您创建架构和数据集，然后标记[!UICONTROL 配置文件]。
2. 数据通过 Web SDK、Mobile Edge SDK 或 API 集成到 Experience Platform。也可以使用分析数据连接器，但可能会导致历程延迟。
3. 您将配置文件加载到 Real-Time CDP 中，并制定治理策略来确保负责任的使用。
4. 您在 [!DNL Adobe Journey Optimizer] 中创建一个确认历程。
5. [!DNL Adobe Journey Optimizer] 会使用首选渠道发送订购确认消息。

>[!ENDTABS]

## 如何实现用例 {#achieve-use-case-instruction}

要完成上述高级概述中的每个步骤，请通读以下部分，其中提供了更多信息和更详细说明的链接。

### 您将会使用的 UI 功能和元素 {#ui-functionality-and-elements}

在完成实施用例的步骤后，您将使用本文档开头列出的 Real-Time CDP 功能和 UI 元素。确保您拥有所有这些区域所需的基于属性的访问控制权限，或让系统管理员授予您这些必要的权限。

### 创建架构设计并指定字段组 {#schema-design}

体验数据模型 (XDM) 资源在 [!DNL Adobe Experience Platform] 的[!UICONTROL “架构”]工作区中进行管理。您可以查看和浏览由 [!DNL Adobe]（例如，[!UICONTROL 字段组]）提供的核心资源，并为贵组织创建自定义资源和架构。

有关创建[架构](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html)的更多信息，请阅读[“创建架构教程”。](/help/xdm/tutorials/create-schema-ui.md)

有四种用于重新参与用例的架构设计。每个架构都需要设置特定的字段，以及我们强烈建议的一些字段。

#### 客户属性架构

此架构用于构建和引用构成客户信息的配置文件数据。这些数据通常通过您的 CRM 或类似系统摄入 [!DNL Adobe Experience Platform] 中，并且是引用用于个性化、营销同意和增强分段功能的客户详细信息所必需的。

客户属性架构由 [!UICONTROL XDM 个人配置文件]类表示，该类包括以下字段组：

+++个人联系方式（字段组）

[个人联系方式](/help/xdm/field-groups/profile/personal-contact-details.md)是 XDM 个人配置文件类的标准架构字段组，它描述了个人的联系信息。

| 字段 | 要求 | 描述 |
| --- | --- | --- |
| `mobilePhone.number` | 必需 | 此人的手机号码，该号码会用于短信。 |
| `personalEmail.address` | 必需 | 此人的电子邮件地址。 |

+++

+++人口统计详细信息（字段组）

[人口统计详细信息](/help/xdm/field-groups/profile/demographic-details.md)是 XDM 个人配置文件类的标准架构字段组。该字段组提供根级人员对象，其子字段描述的是有关个人的信息。

| 字段 | 要求 |
| --- | --- |
| `person.name.firstName` | 建议 |
| `person.name.lastName` | 建议 |

+++

+++外部源系统审计详细信息（字段组）

[外部来源系统审计属性](/help/xdm/data-types/external-source-system-audit-attributes.md)是一种标准体验数据模型 (XDM) 数据类型，用于捕获有关外部来源系统的审核详细信息。

+++

+++同意和偏好设置字段组（字段组）

[同意和偏好设置](/help/xdm/field-groups//profile/consents.md)字段组提供单个对象类型字段同意，以捕获同意和偏好设置信息。

| 字段 | 要求 |
| --- | --- |
| `consents.marketing.email.val` | 必需 |
| `consents.marketing.preferred` | 必需 |
| `consents.marketing.push.val` | 必需 |
| `consents.marketing.sms.val` | 必需 |
| `consents.personalize.content.val` | 必需 |
| `consents.share.val` | 必需 |

+++

+++配置文件测试详细信息（字段组）

该字段组用于最佳实践。

+++

#### 客户数字交易架构

此架构用于构建和引用构成您的网站和/或关联数字平台上发生的客户活动的事件数据。这些数据通常会通过 Web SDK 摄入 [!DNL Adobe Experience Platform] 中，并且对于引用用于触发历程、详细的在线客户分析和增强的分段功能的各种浏览和转换事件是必须的。

客户数字交易架构由 [!UICONTROL XDM ExperienceEvent] 类表示，其中包括以下字段组：

+++Adobe Experience Platform Web SDK ExperienceEvent（字段组）

| 字段 | 要求 |
| --- | --- |
| `device.model` | 建议 |
| `environment.browserDetails.userAgent` | 建议 |

+++

+++Web 详细信息（字段组）

Web 详细信息是 XDM ExperienceEvent 类的标准架构字段组，用于描述有关 Web 详细信息事件的信息，例如交互、页面详细信息和反向链接。

| 字段 | 要求 | 描述 |
| --- | --- | --- |
| `web.webInteraction.linkClicks.id` | 建议 | 与交互对应的 Web 链接或 URL 的 ID。 |
| `web.webInteraction.linkClicks.value` | 建议 | 与交互对应的 Web 链接或 URL 的点击次数。 |
| `web.webInteraction.name` | 建议 | Web 页面的名称。 |
| `web.webInteraction.URL` | 建议 | 网页的 URL。 |
| `web.webPageDetails.name` | 建议 | 发生 Web 交互的网页的名称。 |
| `web.webPageDetails.URL` | 建议 | 发生 Web 交互的网页的 URL。 |
| `web.webReferrer.URL` | 建议 | 描述 Web 交互的反向链接，即在记录当前 Web 交互之前访客的 URL。 |

+++

+++消费者体验事件（字段组）

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

| 字段 | 要求 | 描述 |
| --- | --- | --- |
| `endUserIDs._experience.emailid.authenticatedState` | 必需 | 最终用户电子邮件地址 ID 已验证状态。 |
| `endUserIDs._experience.emailid.id` | 必需 | 最终用户电子邮件地址 ID。 |
| `endUserIDs._experience.emailid.namespace.code` | 必需 | 最终用户电子邮件地址 ID 命名空间代码。 |
| `endUserIDs._experience.mcid.authenticatedState` | 必需 | [!DNL Adobe] Marketing Cloud ID (MCID) 已验证状态。MCID 现在称为 Experience Cloud ID (ECID)。 |
| `endUserIDs._experience.mcid.id` | 必需 | [!DNL Adobe] Marketing Cloud ID (MCID). MCID 现在称为 Experience Cloud ID (ECID)。 |
| `endUserIDs._experience.mcid.namespace.code` | 必需 | [!DNL Adobe] Marketing Cloud ID (MCID) 命名空间代码。 |

+++

+++外部源系统审计详细信息（字段组）

外部来源系统审计属性是一种标准体验数据模型 (XDM) 数据类型，用于捕获有关外部来源系统的审核详细信息。

+++

#### 客户离线交易架构

此架构用于构建和引用构成您的网站之外的平台上发生的客户活动的事件数据。该数据通常会从 POS（或类似系统）摄入 [!DNL Adobe Experience Platform]，并且通常会通过 API 连接流式传输到 Platform。其目的是引用各种线下转化事件，以用于触发历程、深入的线上和线下客户分析以及增强的分段能力。

客户离线交易架构由 [!UICONTROL XDM ExperienceEvent] 类表示，其中包括以下字段组：

+++商务详细信息（字段组）

| 字段 | 要求 | 描述 |
| --- | --- | --- |
| `commerce.cart.cartID` | 必需 | 购物车的 ID。 |
| `commerce.order.orderType` | 必需 | 描述产品订购类型的对象。 |
| `commerce.order.payments.paymentAmount` | 必需 | 描述产品订购付款金额的对象。 |
| `commerce.order.payments.paymentType` | 必需 | 描述产品订购付款类型的对象。 |
| `commerce.order.payments.transactionID` | 必需 | 对象产品订单交易 ID。 |
| `commerce.order.purchaseID` | 必需 | 对象产品订单购买 ID。 |
| `productListItems.name` | 必需 | 代表客户选择的产品的项目名称列表。 |
| `productListItems.priceTotal` | 必需 | 代表客户选择的产品的项目列表的总价。 |
| `productListItems.product` | 必需 | 所选择的产品。 |
| `productListItems.quantity` | 必需 | 代表客户选择的产品的项目列表的数量。 |

+++

+++个人联系方式（字段组）

| 字段 | 要求 | 描述 |
| --- | --- | --- |
| `mobilePhone.number` | 必需 | 此人的手机号码，该号码会用于短信。 |
| `personalEmail.address` | 必需 | 此人的电子邮件地址。 |

+++

+++外部源系统审计详细信息（字段组）

外部来源系统审计属性是一种标准体验数据模型 (XDM) 数据类型，用于捕获有关外部来源系统的审核详细信息。

+++

#### Adobe Web 连接器架构

>[!NOTE]
>
>如果您使用的是 [!DNL Adobe Analytics Data Connector]，则这是一个可选的实施。

此架构用于构建和引用构成您的网站和/或关联数字平台上发生的客户活动的事件数据。此架构类似于“客户数字交易”架构，但其不同之处在于，它是为了在当 Web SDK 不可作为数据收集选项时使用；因此，当您使用[!DNL Adobe Analytics Data Connector]将您的在线数据发送到[!DNL Adobe Experience Platform]作为主要或辅助数据流时， 需要该架构。

[!DNL Adobe]Web 连接器架构由 [!UICONTROL XDM 体验事件]类表示，其中包括以下字段组：

+++Adobe Analytics ExperienceEvent 模板（字段组）

| 字段 | 要求 | 描述 |
| --- | --- | --- |
| `web.webInteraction.linkClicks.id` | 建议 | 与交互对应的 Web 链接或 URL 的 ID。 |
| `web.webInteraction.linkClicks.value` | 建议 | 与交互对应的 Web 链接或 URL 的点击次数。 |
| `web.webInteraction.name` | 建议 | Web 页面的名称。 |
| `web.webInteraction.URL` | 建议 | 网页的 URL。 |
| `web.webPageDetails.name` | 建议 | 发生 Web 交互的网页的名称。 |
| `web.webPageDetails.URL` | 建议 | 发生 Web 交互的网页的 URL。 |
| `web.webReferrer.URL` | 建议 | 描述 Web 交互的反向链接，即在记录当前 Web 交互之前访客的 URL。 |
| `commerce.cart.cartID` | 建议 | |
| `commerce.cart.cartSource` | 建议 | |
| `commerce.cartAbandons.id` | 建议 | |
| `commerce.cartAbandons.value` | 建议 | |
| `commerce.order.orderType` | 建议 | |
| `commerce.order.payments.paymentAmount` | 建议 | |
| `commerce.order.payments.paymentType` | 建议 | |
| `commerce.order.payments.transactionID` | 建议 | |
| `commerce.order.priceTotal` | 建议 | |
| `commerce.order.purchaseID` | 建议 | |
| `commerce.productListAdds.id` | 建议 | |
| `commerce.productListAdds.value` | 建议 | |
| `commerce.productListOpens.id` | 建议 | |
| `commerce.productListOpens.value` | 建议 | |
| `commerce.productListRemoval.id` | 建议 | |
| `commerce.productListRemoval.value` | 建议 | |
| `commerce.productListViews.id` | 建议 | |
| `commerce.productListViews.value` | 建议 | |
| `commerce.productViews.id` | 建议 | |
| `commerce.productViews.value` | 建议 | |
| `commerce.purchases.id` | 建议 | |
| `commerce.purchases.value` | 建议 | |
| `marketing.campaignGroup` | 建议 | |
| `marketing.campaignName` | 建议 | |
| `marketing.trackingCode` | 建议 | |
| `productListItems.name` | 建议 | |
| `productListItems.priceTotal` | 建议 | |
| `productListItems.product` | 建议 | |
| `productListItems.quantity` | 建议 | |
| `endUserIDs._experience.emailid.authenticatedState` | 必需 | 最终用户电子邮件地址 ID 已验证状态。 |
| `endUserIDs._experience.emailid.id` | 必需 | 最终用户电子邮件地址 ID。 |
| `endUserIDs._experience.emailid.namespace.code` | 必需 | 最终用户电子邮件地址 ID 命名空间代码。 |
| `endUserIDs._experience.mcid.authenticatedState` | 必需 | [!DNL Adobe] Marketing Cloud ID (MCID) 已验证状态。MCID 现在称为 Experience Cloud ID (ECID)。 |
| `endUserIDs._experience.mcid.id` | 必需 | [!DNL Adobe] Marketing Cloud ID (MCID). MCID 现在称为 Experience Cloud ID (ECID)。 |
| `endUserIDs._experience.mcid.namespace.code` | 必需 | [!DNL Adobe] Marketing Cloud ID (MCID) 命名空间代码。 |

+++

+++外部源系统审计详细信息（字段组）

外部来源系统审计属性是一种标准体验数据模型 (XDM) 数据类型，用于捕获有关外部来源系统的审核详细信息。

+++

### 从架构创建数据集 {#dataset-from-schema}

数据集是对一组数据的存储和管理结构。智能重新参与历程的每个架构都有一个单独的数据集。

有关如何从架构创建[数据集](/help/catalog/datasets/overview.md)的更多信息，请阅读[数据集 UI 指南。](/help/catalog/datasets/user-guide.md)。

>[!NOTE]
>
>与架构创建步骤类似，您需要使数据集包含在实时客户配置文件中。有关启用数据集以在实时客户配置文件中使用的更多信息，请参阅[创建架构教程。](/help/xdm/tutorials/create-schema-ui.md#profile)

### 隐私、同意和数据治理 {#privacy-consent}

#### 同意政策

>[!IMPORTANT]
>
>为客户提供取消订阅接收品牌通信的能力是一项法律要求，同时这也是为了确保这一选择得到尊重。通过[隐私法规概述](https://experienceleague.adobe.com/docs/experience-platform/privacy/regulations/overview.html)了解有关适用法律的更多信息。

创建重新参与路径时，应该考虑以下[同意策略](https://experienceleague.adobe.com/docs/platform-learn/data-collection/web-sdk/consent/overview.html)：

* 如果 `consents.marketing.email.val = "Y"`，则可以发送电子邮件
* 如果 `consents.marketing.sms.val = "Y"`，则可以发送短信
* 如果 `consents.marketing.push.val = "Y"`，则可以推送
* 如果 `consents.share.val = "Y"`，则可以发布广告

#### 数据治理标签和执行

创建重新参与路径时，应该考虑以下[数据治理标签](/help/data-governance/labels/overview.md)：

* 个人电子邮件地址会被用作直接可识别数据，该数据会用来识别或联系特定个人而不是设备。
   * `personalEmail.address = I1`

#### 营销政策

重新参与历程不需要[营销政策](/help/data-governance/policies/overview.md)，但是，应根据需要考虑以下内容：

* 限制敏感数据
* 限制现场广告
* 限制电子邮件定位
* 限制跨站点定位
* 限制将直接可识别数据与匿名数据相结合

### 创建受众 {#create-audience}

#### 为品牌重新参与历程创建受众

重新参与历程会使用受众来定义配置文件存储中的配置文件子集共享的特定属性或行为，以将适销对路的人群与您的客户群区分开来。可以在 [!DNL Adobe Experience Platform] 上通过多种方式创建受众。

有关如何创建受众的更多信息，请参阅[受众服务 UI 指南](https://experienceleague.adobe.com/docs/experience-platform/segmentation/ui/overview.html#create-audience)。

有关如何直接组成[受众](/help/segmentation/home.md)的更多信息，请参阅[受众组合 UI 指南。](/help/segmentation/ui/audience-composition.md)

有关如何通过平台衍生的区段定义建立受众的更多信息，请阅读[受众生成器 UI 指南。](/help/segmentation/ui/segment-builder.md)

>[!BEGINTABS]

>[!TAB 重新参与历程]

创建此受众是为了增强经典的“放弃购物车”场景。虽然放弃购物车通常侧重于在特定时间段内将产品添加到购物车而后没有购买的情况，但此类受众会寻找更早的参与，特别是那些可能浏览过特定产品但没有将其添加到购物车中，并且在特定时间范围内没有在您的网站上进行后续活动的人。这些受众有助于让符合此纳入标准的客户“优先考虑”您的品牌，也可以用于数字属性可能与传统电子商务模型不同的客户。

以下事件用于重新参与历程，其中用户在线查看了产品，在接下来的 24 小时内没有将其添加到购物车，并且随后的 3 天内没有出现品牌参与活动。

设置此受众时需要以下字段和条件：

* `EventType: commerce.productViews`
   * `Timestamp: <= 24 hours before now`
* `EventType is not: commerce.procuctListAdds`
   * `Timestamp: <= 24 hours before now, GAP(>= 3 days)`
* `EventType: application.launch or web.webpagedetails.pageViews or commerce.purchases`
   * `Timestamp: <= 2 days before now`

对重新参与历程的描述符显示为：

`Include audience who have at least 1 EventType = ProductViews event THEN have at least 1 Any event where (EventType does not equal commerce.productListAdds) and occurs in last 24 hour(s) then after 3 days do not have any Any event where (EventType = application.launch or web.webpagedetails.pageViews or commerce.purchases) and occurs in last 2 day(s).`

>[!TAB 放弃的购物车历程]

创建此受众是为了支持经典的“放弃购物车”场景。其目的是找到将产品添加到购物车但最终没有进行购买的客户。这些受众不仅有助于让您的客户“优先考虑”您的品牌，而且还会优先考虑他们留下而没有后续购买的产品。

以下事件用于废弃购物车之旅，其中用户在购物车中添加了产品，但在过去 24 小时内没有完成购买或清空购物车。

设置此受众时需要以下字段和条件：

* `EventType: commerce.productListAdds`
   * `Timestamp: >= 1 days before now and <= 4 days before now `
* `EventType: commerce.purchases`
   * `Timestamp: <= 4 days before now`
* `EventType: commerce.productListRemovals`
   * `Timestamp: <= 4 days before now`

放弃的购物车历程的描述符显示为：

`Include EventType = commerce.productListAdds between 30 min and 1440 minutes before now. exclude EventType = commerce.purchases 30 minutes before now OR EventType = commerce.productListRemovals AND Cart ID equals Product List Adds1 Cart ID (the inclusion event).`

>[!TAB 订购确认历程]

这个历程不需要创建任何受众。

>[!ENDTABS]

### Adobe Journey Optimizer 中的历程设置 {#journey-setup}

>[!NOTE]
>
>[!DNL Adobe Journey Optimizer] 并不涵盖图中所示的所有内容。所有[付费媒体广告](/help/destinations/catalog/social/overview.md)均在[!UICONTROL 目标]中创建。

[[!DNL Adobe Journey Optimizer]](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/journey.html) 可帮助您为客户提供贴合心意的、上下文和个性化的体验。客户历程是客户与品牌互动的整个过程。每个用例历程都需要特定的信息。下面列出的是每个历程分支所需的精确数据。

>[!BEGINTABS]

>[!TAB 重新参与历程]

重新参与历程的目标是放弃在网站和移动应用程序上浏览产品的情况。<p>![客户智能重新参与历程高级视觉概述。](../intelligent-re-engagement/images/re-engagement-journey.png "客户智能重新参与历程高级视觉概述。"){width="2560" zoomable="yes"}</p>

+++活动

* 事件 1：产品查看次数
   * 架构：客户数字交易
   * 字段：
      * `EventType`
   * 条件：
      * `EventType = commerce.productViews`
      * 字段：
         * `Commerce.productViews.id`
         * `Commerce.productViews.value`
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

* 事件 2：加入购物车
   * 架构：客户数字交易
   * 字段：
      * `EventType`
   * 条件：
      * `EventType = commerce.productListAdds`
      * 字段：
         * `Commerce.productListAdds.id`
         * `Commerce.productListAdds.value`
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
         * `commerce.cart.cartID`
         * `endUserIDs._experience.emailid.authenticatedState`
         * `endUserIDs._experience.emailid.id`
         * `endUserIDs._experience.emailid.namespace.code`
         * `_id`

* 事件 3：品牌参与
   * 架构：客户数字交易
   * 字段：
      * `EventType`
   * 条件：
      * `EventType in application.launch, commerce.purchases, web.webpagedetails.pageViews`
      * 字段：
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
         * `web.webpagedetails.URL`
         * `web.webpagedetails.isHomePage`
         * `web.webpagedetails.name`
         * `endUserIDs._experience.emailid.authenticatedState`
         * `endUserIDs._experience.emailid.id`
         * `endUserIDs._experience.emailid.namespace.code`
         * `_id`
         * `Commerce.purchases.id`
         * `Commerce.purchases.value`
         * `shipping.address.city`
         * `shipping.address.countryCode`
         * `shipping.address.postalCode`
         * `shipping.address.state`
         * `shipping.address.street1`
         * `shipping.address.street2`
         * `shipping.shipDate`
         * `shipping.trackingNumber`
         * `shipping.trackingURL`

+++

+++关键历程逻辑

* 历程进入逻辑
   * 产品查看事件

* 条件
   * 检查自上次查看产品以来至少有一次在线或离线购买事件。
      * 架构：客户数字交易
      * `eventType = commerce.purchases`
      * `timestamp > timestamp of product last viewed`

   * 检查自上次查看产品以来至少有一次离线购买：
      * 架构：客户离线交易
      * `eventType = commerce.purchases`
      * `timestamp > timestamp of product last viewed`

   * 条件 - 选择目标渠道
      * 电子邮件
         * `consents.marketing.email.val = y`
      * 推送
         * `consents.marketing.push.val=y`
      * 短信
         * `consents.marketing.sms.val = y`

   * 渠道个性化
      * 基于产品查看情况的个性化渠道内容。

+++

>[!TAB 放弃的购物车历程]

放弃的购物车历程针对的是在网站和移动应用程序上，已放入购物车但尚未购买的产品。<p>![客户放弃的购物车历程高级视觉概述。](../intelligent-re-engagement/images/abandoned-cart-journey.png "客户放弃的购物车历程高级视觉概述。"){width="2560" zoomable="yes"}</p>

+++活动

* 事件 2：加入购物车
   * 架构：客户数字交易
   * 字段：
      * `EventType`
   * 条件：
      * `EventType = commerce.productListAdds`
      * 字段：
         * `Commerce.productListAdds.id`
         * `Commerce.productListAdds.value`
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
         * `commerce.cart.cartID`
         * `endUserIDs._experience.emailid.authenticatedState`
         * `endUserIDs._experience.emailid.id`
         * `endUserIDs._experience.emailid.namespace.code`
         * `_id`

* 事件 4：在线购买
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

* 事件 3：品牌参与
   * 架构：客户数字交易
   * 字段：
      * `EventType`
   * 条件：
      * `EventType in application.launch, commerce.purchases, web.webpagedetails.pageViews`
      * 字段：
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
         * `web.webpagedetails.URL`
         * `web.webpagedetails.isHomePage`
         * `web.webpagedetails.name`
         * `endUserIDs._experience.emailid.authenticatedState`
         * `endUserIDs._experience.emailid.id`
         * `endUserIDs._experience.emailid.namespace.code`
         * `_id`
         * `Commerce.purchases.id`
         * `Commerce.purchases.value`
         * `shipping.address.city`
         * `shipping.address.countryCode`
         * `shipping.address.postalCode`
         * `shipping.address.state`
         * `shipping.address.street1`
         * `shipping.address.street2`
         * `shipping.shipDate`
         * `shipping.trackingNumber`
         * `shipping.trackingURL`

+++

+++关键历程逻辑

* 历程进入逻辑
   * `AddToCart` 活动

* AuthenticatedState 已通过验证

* 条件：自上次放弃购物车以来离线购买：
   * 架构：客户离线交易
   * `eventType = commerce.purchases`
   * `timestamp > timestamp of cart was last abandoned`

* 条件：自上次放弃购物车后已清除的购物车：
   * 架构：客户数字交易
   * `eventType = commerce.cartCleared`
   * `cartID`（购物车的 ID）
   * `timestamp > timestamp of cart was last abandoned`

* 选择目标渠道（选择一个或多个渠道以扩大覆盖范围）
   * 电子邮件
      * `consents.marketing.email.val = y`
   * 推送
      * `consents.marketing.push.val = y`
   * 短信
      * `consents.marketing.sms.val = y`
   * 渠道个性化
      * 显示购物车详细信息，并能够以表格形式显示多个产品。

+++

>[!TAB 订购确认历程]

订购确认历程侧重于通过网站和移动应用程序购买的产品。<p>![客户订购确认历程高级视觉概述。](../intelligent-re-engagement/images/order-confirmation-journey.png "客户订购确认历程高级视觉概述。"){width="2560" zoomable="yes"}</p>

+++活动

* 事件 4：在线购买
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
   * 选择目标渠道（选择一个或多个渠道以扩大覆盖范围）
      * 订单确认本质上是一种服务，因此通常不需要检查同意情况。
      * 电子邮件
      * 推送
      * 短信

   * 渠道内容个性化
      * 显示订购详细信息，并可以使用表格格式显示产品列表。

+++

>[!ENDTABS]

有关在 [!DNL Adobe Journey Optimizer] 中创建历程的更多信息，请阅读[开始使用历程指南。](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/journey.html)

### 在目标内设置付费媒体广告 {#paid-media-ads}

目标框架用于付费媒体广告。检查同意情况后，它会发送到所配置的各个目的地。有关目标的更多信息，请阅读[目标概览](/help/destinations/home.md)文档。

#### 目标所需数据

流式处理区段导出目标（例如 Facebook、Google 目标客户匹配功能、Google DV360）支持来自客户数据的各种标识：

* `personalEmail.address`
* `ECID`
* `mobilePhone.number`

“放弃购物车区段”是流式传输的，因此可由目标框架用于此用例。

* 流/已触发
   * [广告](/help/destinations/catalog/advertising/overview.md)/[付费媒体和社交](/help/destinations/catalog/social/overview.md)
   * [移动设备](/help/destinations/catalog/mobile-engagement/overview.md)
   * [流式处理目标](/help/destinations/catalog/streaming/http-destination.md)
   * [自定义目标 SDK](/help/destinations/destination-sdk/overview.md)
