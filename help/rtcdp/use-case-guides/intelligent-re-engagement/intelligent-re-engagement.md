---
title: 智能重新参与
description: 在关键转化时刻提供引人注目的互联体验，以智能的方式重新吸引不常光顾的客户。
hide: true
hidefromtoc: true
source-git-commit: 7de5fe7808a22137c417a4ca865d764b0814b90e
workflow-type: tm+mt
source-wordcount: '3424'
ht-degree: 56%

---

# 以智能的方式重新吸引客户回归

重新吸引放弃某个转换的客户以智能和负责任的方式完成该转换。 通过体验而不是提醒来吸引流失的客户，以提高转化率并促进客户存留期价值的增长。

采用实时考虑因素，考虑所有消费者素质和行为，并根据在线和离线事件提供快速的重新认证。

![逐步智能重新参与高级视觉概述。](../intelligent-re-engagement/images/step-by-step.png)

## 用例概述

您将在处理重新参与历程示例时构建架构、数据集和受众。 您还将了解在中设置示例历程所需的功能 [!DNL Adobe Journey Optimizer] 以及在目标中创建付费媒体广告所需的受众。 本指南使用在下面概述的用例历程中重新吸引客户的示例：

* **重新参与历程**  — 定位已放弃在网站和移动设备应用程序上浏览产品的客户。
* **已放弃的购物车历程**  — 定位已将产品放入购物车但尚未在网站和移动设备应用程序上购买的客户。
* **订单确认历程**  — 重点关注通过网站和移动应用程序进行的产品购买。

## 先决条件和规划 {#prerequisites-and-planning}

在完成实施用例的步骤后，您将使用以下 Real-Time CDP 功能和 UI 元素（按使用顺序列出）。确保您拥有所有这些区域所需的基于属性的访问控制权限，或让系统管理员授予您这些必要的权限。

* [[!DNL Adobe Real-Time Customer Data Platform (Real-Time CDP)]](https://experienceleague.adobe.com/docs/platform-learn/tutorials/rtcdp/understanding-the-real-time-customer-data-platform.html)  — 跨数据源集成数据以推动营销活动。 然后，该数据可用于创建活动受众，并显示电子邮件和网络促销图块中使用的个性化数据元素（例如，姓名或与帐户相关的信息）。CDP还用于在电子邮件和Web上激活受众(通过 [!DNL Adobe Target])。
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

以下是三个重新参与示例历程的高级概述。

>[!BEGINTABS]

>[!TAB 重新参与历程]

重新参与历程定位网站和移动应用程序上放弃的产品浏览。 当产品已被查看但未购买或添加到购物车时，会触发此历程。如果过去 24 小时内没有添加列表，则三天后会触发品牌参与功能。<p>![客户智能重新参与历程高级视觉概述。](../intelligent-re-engagement/images/re-engagement-journey.png "客户智能重新参与历程高级视觉概述。"){width="2560" zoomable="yes"}</p>

1. 您可以创建架构和数据集，然后标记为 [!UICONTROL 个人资料].
2. 数据通过Web SDK、Mobile Edge SDK或API集成到Experience Platform中。 也可以使用Analytics Data Connector，但可能会导致历程延迟。
3. 您可以将配置文件加载到Real-Time CDP中，并构建治理策略以确保负责任地使用。
4. 您可以从配置文件列表中构建重点受众，以检查 **客户** 在过去三天里订了婚约。
5. 您在中创建重新参与历程 [!DNL Adobe Journey Optimizer].
6. 如果需要，请与&#x200B;**数据合作伙伴**&#x200B;合作，以将受众激活到所需的付费媒体目标。
7. [!DNL Adobe Journey Optimizer] 检查同意并发送配置的各种操作。

>[!TAB 放弃的购物车历程]

放弃的购物车历程面向已放入购物车但尚未在网站和移动设备应用程序上购买的产品。 此外，使用此方法启动和停止付费媒体营销活动。<p>![客户放弃的购物车历程高级视觉概述。](../intelligent-re-engagement/images/abandoned-cart-journey.png "客户放弃的购物车历程高级视觉概述。"){width="2560" zoomable="yes"}</p>

1. 创建架构和数据集，则标记为 [!UICONTROL 个人资料].
2. 数据通过Web SDK、Mobile Edge SDK或API集成到Experience Platform中。 也可以使用Analytics Data Connector，但可能会导致历程延迟。
3. 您可以将配置文件加载到Real-Time CDP中，并构建治理策略以确保负责任地使用。
4. 您可以从配置文件列表中构建重点受众，以检查 **客户** 已将商品放入购物车，但尚未完成购买。 **[!UICONTROL 添加到购物车]**&#x200B;事件会启动一个等待 30 分钟的计时器，然后检查购买情况。如果未购买任何产品，则 **客户** 已添加到 **[!UICONTROL 放弃购物车]** 受众。
5. 您在中创建放弃的购物车历程 [!DNL Adobe Journey Optimizer].
6. 如果需要，请与&#x200B;**数据合作伙伴**&#x200B;合作，以将受众激活到所需的付费媒体目标。
7. [!DNL Adobe Journey Optimizer] 检查同意并发送配置的各种操作。

>[!TAB 订购确认历程]

订购确认历程侧重于通过网站和移动应用程序购买的产品。<p>![客户订购确认历程高级视觉概述。](../intelligent-re-engagement/images/order-confirmation-journey.png "客户订购确认历程高级视觉概述。"){width="2560" zoomable="yes"}</p>

1. 您可以创建架构和数据集，然后标记为 [!UICONTROL 个人资料].
2. 数据通过Web SDK、Mobile Edge SDK或API集成到Experience Platform中。 也可以使用Analytics Data Connector，但可能会导致历程延迟。
3. 您可以将配置文件加载到Real-Time CDP中，并构建治理策略以确保负责任地使用。
4. 您可在中创建确认历程 [!DNL Adobe Journey Optimizer].
5. [!DNL Adobe Journey Optimizer] 使用首选渠道发送订单确认消息。

>[!ENDTABS]

## 如何实现用例 {#achieve-use-case-instruction}

要完成上述高级概述中的每个步骤，请通读以下部分，其中提供了更多信息和更详细说明的链接。

### 您将会使用的 UI 功能和元素 {#ui-functionality-and-elements}

在完成实施用例的步骤后，您将使用本文档开头列出的 Real-Time CDP 功能和 UI 元素。确保您拥有所有这些区域所需的基于属性的访问控制权限，或让系统管理员授予您这些必要的权限。

### 创建架构设计并指定字段组 {#schema-design}

体验数据模型(XDM)资源在中管理 [!UICONTROL 架构] 中的工作区 [!DNL Adobe Experience Platform]. 您可以查看和浏览提供的核心资源 [!DNL Adobe] (例如， [!UICONTROL 字段组])，并为您的组织创建自定义资源和架构。

有关创建的详细信息 [架构](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=zh-Hans)，阅读 [创建架构教程。](/help/xdm/tutorials/create-schema-ui.md)

有四种架构设计用于重新参与用例。 每个架构都需要设置特定的字段，以及一些强烈建议的字段。

#### 客户属性架构

此架构用于构建和引用构成客户信息的用户档案数据。 此数据通常摄取到 [!DNL Adobe Experience Platform] 通过CRM或类似系统，并且是引用用于个性化、营销同意和增强分段功能的客户详细信息所必需的。

客户属性架构由 [!UICONTROL XDM个人资料] 类，包括以下字段组：

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

此架构用于构建和引用在您的网站和/或关联的数字平台上发生的构成客户活动的事件数据。 此数据通常摄取到 [!DNL Adobe Experience Platform] 通过Web SDK，对于引用用于触发历程、详细的在线客户分析和增强的分段功能的各种浏览和转化事件是必需的。

客户数字交易模式由 [!UICONTROL XDM ExperienceEvent] 类，包括以下字段组：

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
| `endUserIDs._experience.mcid.id` | 必需 | [!DNL Adobe] Marketing CloudID (MCID)。 MCID 现在称为 Experience Cloud ID (ECID)。 |
| `endUserIDs._experience.mcid.namespace.code` | 必需 | [!DNL Adobe] Marketing Cloud ID (MCID) 命名空间代码。 |

+++

+++外部源系统审计详细信息（字段组）

外部来源系统审计属性是一种标准体验数据模型 (XDM) 数据类型，用于捕获有关外部来源系统的审核详细信息。

+++

#### 客户离线交易架构

此架构用于构建和引用构成您的客户活动的事件数据，这些活动发生在网站之外的平台上。 此数据通常摄取到 [!DNL Adobe Experience Platform] 从POS（或类似系统）访问，并且通常通过API连接流式传输到Platform。 其目的是引用各种离线转化事件，用于触发历程、深度在线和离线客户分析以及增强分段功能。

客户离线交易架构由 [!UICONTROL XDM ExperienceEvent] 类，包括以下字段组：

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
>如果您使用的是 [!DNL Adobe Analytics Data Connector].

此架构用于构建和引用在您的网站和/或关联的数字平台上发生的构成客户活动的事件数据。 此架构与客户数字交易架构类似，不同之处在于，此架构旨在于Web SDK不是数据收集选项时使用；因此，当您使用 [!DNL Adobe Analytics Data Connector] 将您的在线数据发送到 [!DNL Adobe Experience Platform] 作为主数据流或辅助数据流。

此 [!DNL Adobe] Web连接器架构由 [!UICONTROL XDM ExperienceEvent] 类，包括以下字段组：

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
| `endUserIDs._experience.mcid.id` | 必需 | [!DNL Adobe] Marketing CloudID (MCID)。 MCID 现在称为 Experience Cloud ID (ECID)。 |
| `endUserIDs._experience.mcid.namespace.code` | 必需 | [!DNL Adobe] Marketing Cloud ID (MCID) 命名空间代码。 |

+++

+++外部源系统审计详细信息（字段组）

外部来源系统审计属性是一种标准体验数据模型 (XDM) 数据类型，用于捕获有关外部来源系统的审核详细信息。

+++

### 从架构创建数据集 {#dataset-from-schema}

数据集是一组数据的存储和管理结构。 智能重新参与历程的每个架构都有一个数据集。

有关如何创建 [数据集](/help/catalog/datasets/overview.md) 从模式中，阅读 [数据集UI指南](/help/catalog/datasets/user-guide.md).

>[!NOTE]
>
>与架构创建步骤类似，您需要使数据集包含在实时客户配置文件中。有关启用数据集以在实时客户配置文件中使用的更多信息，请参阅[创建架构教程。](/help/xdm/tutorials/create-schema-ui.md#profile)

### 隐私、同意和数据治理 {#privacy-consent}

#### 同意政策

>[!IMPORTANT]
>
>为客户提供取消订阅接收品牌通信的能力是一项法律要求，同时这也是为了确保这一选择得到尊重。进一步了解 [隐私法规概述](https://experienceleague.adobe.com/docs/experience-platform/privacy/regulations/overview.html).

创建重新参与路径时，请执行以下操作 [同意政策](https://experienceleague.adobe.com/docs/platform-learn/data-collection/web-sdk/consent/overview.html) 应考虑以下事项：

* 如果 `consents.marketing.email.val = "Y"` 然后可以发送电子邮件
* 如果 `consents.marketing.sms.val = "Y"` 然后可以发送短信
* 如果 `consents.marketing.push.val = "Y"` 然后可以推送
* 如果 `consents.share.val = "Y"` 然后可以广告

#### 数据治理标签和实施

创建重新参与路径时，请执行以下操作 [数据治理标签](/help/data-governance/labels/overview.md) 应考虑以下事项：

* 个人电子邮件地址会被用作直接可识别数据，该数据会用来识别或联系特定个人而不是设备。
   * `personalEmail.address = I1`

#### 营销政策

没有 [营销策略](/help/data-governance/policies/overview.md) 但是，重新参与历程要求执行以下操作，这应根据需要进行考虑：

* 限制敏感数据
* 限制现场广告
* 限制电子邮件定位
* 限制跨站点定位
* 限制将直接可识别数据与匿名数据相结合

### 创建受众 {#create-audience}

#### 为品牌重新参与历程创建受众

重新参与历程会使用受众来定义配置文件存储中的配置文件子集共享的特定属性或行为，以将适销对路的人群与您的客户群区分开来。可以在以下位置通过多种方式创建受众： [!DNL Adobe Experience Platform].

有关如何创建受众的更多信息，请参阅 [受众服务UI指南](https://experienceleague.adobe.com/docs/experience-platform/segmentation/ui/overview.html#create-audience).

有关如何直接撰写的详细信息 [受众](/help/segmentation/home.md)，阅读 [受众合成UI指南](/help/segmentation/ui/audience-composition.md).

有关如何通过平台衍生的区段定义建立受众的更多信息，请阅读[受众生成器 UI 指南。](/help/segmentation/ui/segment-builder.md)

>[!BEGINTABS]

>[!TAB 重新参与历程]

创建此受众是对经典“购物车放弃”方案的增强。 由于放弃购买通常侧重于在特定时间段内没有后续购买的购物车添加，因此该受众会寻找较早的参与，尤其是那些可能浏览过特定产品但未将其添加到购物车并在特定时间段内未在您的网站上进行跟进活动的受众。 此受众有助于将您的品牌置于符合此包含标准的客户的“心目中”，此外，对于数字财产可能与传统电子商务模型不同的客户，也可以利用此受众。

以下事件用于重新参与历程，其中用户在线查看了产品，在接下来的 24 小时内没有将其添加到购物车，并且随后的 3 天内没有出现品牌参与活动。

设置此受众时需要以下字段和条件：

* `EventType: commerce.productViews`
   * `Timestamp: <= 24 hours before now`
* `EventType is not: commerce.procuctListAdds`
   * `Timestamp: <= 24 hours before now, GAP(>= 3 days)`
* `EventType: application.launch or web.webpagedetails.pageViews or commerce.purchases`
   * `Timestamp: <= 2 days before now`

重新参与历程的描述符显示为：

`Include audience who have at least 1 EventType = ProductViews event THEN have at least 1 Any event where (EventType does not equal commerce.productListAdds) and occurs in last 24 hour(s) then after 3 days do not have any Any event where (EventType = application.launch or web.webpagedetails.pageViews or commerce.purchases) and occurs in last 2 day(s).`

>[!TAB 放弃的购物车历程]

创建此受众是为了支持经典的“购物车放弃”方案。 其目的是查找向其购物车中添加了产品但最终未完成购买的客户。 此受众不仅有助于让您的品牌成为客户的“头等大事”，还有助于他们留下的产品，无需再购买。

以下事件用于放弃的购物车历程，在该历程中，用户将产品添加到购物车，但在过去24小时内未完成购买或清除购物车。

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

此历程不需要创建任何受众。

>[!ENDTABS]

### Adobe Journey Optimizer 中的历程设置 {#journey-setup}

>[!NOTE]
>
>[!DNL Adobe Journey Optimizer] 不包含图中显示的所有内容。 全部 [付费媒体广告](/help/destinations/catalog/social/overview.md) 创建于 [!UICONTROL 目标].

[[!DNL Adobe Journey Optimizer]](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/journey.html) 帮助您为客户提供互联、情境式和个性化的体验。 客户历程是客户与品牌互动的整个过程。每个用例历程都需要特定信息。 下面列出的是每个历程分支所需的精确数据。

>[!BEGINTABS]

>[!TAB 重新参与历程]

重新参与历程定位网站和移动应用程序上放弃的产品浏览。<p>![客户智能重新参与历程高级视觉概述。](../intelligent-re-engagement/images/re-engagement-journey.png "客户智能重新参与历程高级视觉概述。"){width="2560" zoomable="yes"}</p>

+++活动

* 活动1：产品查看次数
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

* 事件2：添加到购物车
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

* 活动3：品牌互动
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

放弃的购物车历程面向已放入购物车但尚未在网站和移动设备应用程序上购买的产品。<p>![客户放弃的购物车历程高级视觉概述。](../intelligent-re-engagement/images/abandoned-cart-journey.png "客户放弃的购物车历程高级视觉概述。"){width="2560" zoomable="yes"}</p>

+++活动

* 事件2：添加到购物车
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

* 活动4：在线购买
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

* 活动3：品牌互动
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
   * `cartID` （购物车的ID）
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

* 活动4：在线购买
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

### 在目标中设置付费媒体广告 {#paid-media-ads}

目标框架用于付费媒体广告。检查同意后，它会发送到配置的各种目标。 欲知目标的详情，请参阅 [目标概述](/help/destinations/home.md) 文档。

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
