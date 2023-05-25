---
keywords: RTCDP；CDP；Real-time Customer Data Platform；实时客户数据平台；real time cdp；cdp；rtcdp
title: Real-time Customer Data Platform快速入门
description: 在设置您实施的 Adobe Real-Time Customer Data Platform 时请使用此样板场景作为示例。
exl-id: 9f775d33-27a1-4a49-a4c5-6300726a531b
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '2333'
ht-degree: 2%

---

# Real-time Customer Data Platform快速入门

本快速入门指南将指导您完成Real-time Customer Data Platform (Real-Time CDP)的示例实施。 您可以将其用作设置自己的实施时的示例。 尽管本指南显示了具体的示例，但它链接到在创建设置时可以使用的其他信息。

此示例展示了由Adobe Experience Platform提供支持的Real-time Customer Data Platform的强大功能：

* 从多个源引入数据
* 将它们合并为一个 [!DNL real-time customer profile]
* 跨设备提供一致、相关和个性化的体验。

## 用例

运动服装公司Luma一直努力改善客户体验。 他们推出了一项新举措，以提高与礼品相关的销售额。 他们还希望减少过度接触，例如向客户投放令人讨厌的广告。

目前，他们花在媒体上的钱太多，这些媒体会针对访客以后不打算购买的项目进行重新定位。 例如，Luma不希望使用旨在为其他人一次性购买的项目重新定位某人。

目前，Luma的数据分散在多个源中。 因此，它们面临着重大挑战：

* 营销组织必须与各自拥有数据源的各个团队合作，包括网站、移动应用程序、忠诚度系统、CRM等。
* 当营销团队获得数据访问权限时，数据通常会失效，不再与其对时间敏感的活动相关。
* 他们需要统一数据，以便针对个人，而不是渠道。

因此，Luma具有以下业务目标：

* 从其完全不同的数据源创建其用户的实时单一视图。
* 通过跨不同渠道和设备的相关消息个性化营销活动。

要实现这些目标，营销团队需要能够大规模管理客户数据。

借助由Adobe Experience Platform提供支持的Real-Time CDP，Luma的营销组织可以：

1. 从不同的平台收集数据，并确保该数据可在下游用于其他营销活动。
1. 创建其消费者的单一、实时视图，而不考虑数据的来源。
1. 在所有接触点之间推动一致、相关和个性化的体验。

## 步骤

本教程包含以下步骤：

1. 构建 [客户配置文件](#customer-profile).
1. [个性化](#personalizing-the-user-experience) 用户体验。
1. 使用 [多个数据源](#using-multiple-data-sources).
1. [配置数据源](#configuring-a-data-source).
1. [收集数据](#bringing-the-data-together-for-a-specific-customer) 特定客户的。
1. 设置 [区段](#segments).
1. 设置 [目标](#destinations).
1. [跨设备拼合配置文件](#cross-device-identity-stitching).
1. [分析配置文件](#analyzing-the-profile).

## 客户配置文件

当客户首次访问您的网站时，您对他们一无所知。

![image](assets/luma-site.png)

在导航时，会实时捕获数据并不仅将其发送到Adobe Analytics中的报表包，还会直接发送到Adobe Experience Platform。 在收集数据时，您开始根据中的行为数据形成消费者的单一视图 [!DNL Experience Platform's real-time customer profile].

该网站的许多访客可能是以前从Luma购买的回头客。  Luma必须个性化消息传递和服务内容，以便为新访客和回访访客以及已知客户提供服务。

### 新客户的首次访问

例如，某个未识别的访客导航到Luma网站上的男士部分，并查看了几个正在运行Sweatt的访客。

![image](assets/luma-sweatshirts.png)

当客户导航以了解有关这些产品的更多信息时，这些产品查看次数会在Adobe Analytics中收集并发送到 [!DNL Experience Platform].

<!--![image](assets/luma-shirt-detail.png)-->

Luma可以将访客的行为映射到Adobe Experience Platform上的用户个人资料，并开始更全面地了解该消费者的行为。

### 获得更详细的客户视图

随着客户继续与网站交互，将呈现更清晰的图像。 例如，假设访客将产品添加到购物车并登录。

当客户登录时，她自称是Sarah Rose。

![image](assets/luma-login.png)

将合并两个标识：

* 匿名浏览数据
* 与Sarah Rose的帐户关联的现有数据

两个身份都合并到中的单个配置文件中 [!DNL Experience Platform]. Luma现在拥有此消费者的统一视图。

根据匿名访客在网站男性区域的浏览行为，可以假定该客户是男性。 Luma登录后，认出了Sarah Rose。 Luma利用 [!DNL Real-Time Customer Profile] 以优化跨渠道发送给她的消息传送。

## 个性化用户体验

我们对Sarah致以忠诚的谢意，感谢她成为铜牌会员，并提供了更多关于其福利以及如何提高地位和积分的信息。

她导航到主页浏览更多内容。

![image](assets/luma-personal.png)

Sarah获得个性化主页体验，该体验基于她进行动态交付 [!DNL Real-Time Customer Profile] 在Adobe Experience Platform中。

她看到相关内容，这要归功于Adobe Target中由Adobe Sensei提供支持的个性化功能，该功能会考虑她过去的购买情况以及对服装和用品的喜好。 Luma还根据自己最近浏览过的内容，为男士定制跑步装备。

在本页的下方，将显示Sarah的特色产品，以及基于她最近查看过的商品的全新推荐栏。

此个性化内容可帮助Sarah快速找到相关项目。 这可以提高转化率，并提供更愉快的客户体验。

### 将客户带回来

Sarah心烦意乱，离开网站，结束会议。 Luma可以使用她在Adobe Experience Platform中的数据来帮助她返回网站。

Real-time Customer Data Platform由Adobe Experience Platform提供支持，专为客户体验管理而构建。 它使组织能够：

* 简化数据集成和激活
* 管理已知和未知的数据使用情况
* 大规模加快营销用例

## 使用多个数据源

Luma的团队将所有行为和客户数据放在一个地方。

![image](assets/luma-dash.png)

他们可以摄取以下所有来源的数据：

* 现有Adobe Experience Cloud解决方案数据
* 非Adobe来源，如Luma的忠诚度计划、呼叫中心和销售点系统数据
* 来自Luma数据源的实时流数据
* 来自Adobe解决方案的实时数据（无需新标记）

来自不同来源的所有此类数据将合并到单个统一的客户配置文件中。

## 配置数据源

使用 [!DNL Real-Time Customer Data Platform] 将新的数据源引入Platform。 Real-Time CDP包括数据源目录，可以快速轻松地添加到配置文件中。

![image](assets/luma-source-cat.png)

例如，要摄取Luma的CRM数据，请筛选目录依据 *CRM*，以及包含以下内容的所有现成连接器 *CRM* 中列出了。 添加 [!DNL Microsoft Dynamics CRM] 数据：

1. 授权连接。

   ![image](assets/luma-source-auth.png)

1. 从推荐的XDM预映射表列表中选择要导入的内容。

   <!--    ![image](assets/luma-source-import.png) -->

   例如，选择 **[!UICONTROL 联系人]**. 会自动加载联系人数据的预览，以便您可以确保一切按预期显示。

   Adobe Experience Platform通过将标准字段自动映射到 [!DNL Experience Data Model] (XDM)配置文件架构。

1. 查看字段映射。

   <!--    ![image](assets/luma-source-mapping.png) -->

   例如，仔细检查联系人的email字段是否正确映射。\
   您可以选择预览数据并执行高级映射。

1. 设置计划。

   ![image](assets/luma-source-sched.png)

完事了。 您刚刚添加了 [!DNL Microsoft CRM] 作为数据源进入 [!DNL Experience Platform].

### 为使用策略引入的数据设置标签

Luma具有许多内部策略，这些策略限制使用某些类型收集的信息，并且还必须遵守关于数据使用的法律和隐私相关注意事项。 使用Adobe Experience Platform数据管理，可将预定义的数据使用标签应用于数据集（以及这些数据集中的特定字段），从而允许Luma根据特定使用限制对其数据进行分类。

![](assets/governance-labels.png)

应用数据使用标签后，Luma便可以使用数据管理来创建数据使用策略。 数据使用策略是描述允许对包含特定标签的数据执行的操作类型的规则。 当尝试在Real-Time CDP中执行构成策略违规的操作时，将阻止该操作，并提供警报以显示违反的策略及其原因。

## 为特定客户汇集数据

在此场景中，搜索Sarah Rose的用户档案。 她的个人资料随即出现，并附上了她用来登录的电子邮件。

<!-- ![image](assets/luma-find-profile.png) -->

Luma拥有的所有关于Sarah展示的个人资料信息。 这包括她的个人信息，如地址和电话号码、通信偏好以及她符合条件的区段。

| 类别 | 描述 |
|---|---|
| 标识 | 显示中链接在一起的标识 [!DNL Platform] 来自Sarah与Luma跨渠道和设备的互动。 将显示她来自网站的ECID。 她的身份还包括来自其移动应用程序的ECID、电子邮件ID，以及最近添加的CRM ID [!DNL Microsoft Dynamics] 数据集，以及从Luma忠诚度系统传递到Adobe Experience Platform的忠诚度ID。 |
| 事件 | 显示Sarah与Luma品牌的所有交互数据。 这包括她刚刚查看的项目、过去查看过的任何内容、她收到的电子邮件、她与呼叫中心的互动，以及每次互动都发生在什么渠道和设备上。 |

Real-Time CDP配置文件将Luma营销团队的工作流程从几周缩短到几分钟，并根据此360度客户视图解锁个性化的可能性。 配置文件将她登录前浏览网站时的行为数据与她现有的客户配置文件合并，从而全面了解Sarah。

营销团队可以使用此增强功能， [!DNL Real-Time Customer Profile] 更好地个性化Sarah的体验，并提高她对Luma的品牌忠诚度。

## 区段

借助强大的Adobe Experience Platform分段功能，营销人员可以基于中捕获的数据，组合属性、事件和现有区段 [!DNL Real-Time Customer Profile].

<!-- ![image](assets/luma-segments.png) -->

在这种情况下，Sarah最近在该网站上的互动表现出与她过去行为不同的行为。 她通常买女装。 不过，她购物车里装的是男士大运动衫。

Luma数据科学团队围绕购买倾向创建了模型。 有一种模型可以确定现有消费者的服装类别（例如男士/女士）或尺码是否有突然变化。 莎拉购买行为的变化表明她不是在为自己买东西。

<!-- ![image](assets/luma-gift.png) -->

### 定义区段

修改或创建一个区段，以表示似乎正在购买礼品的购物车放弃者：

```sql
Profile: Category != Preferred Category 
AND 
Product Size != Preferred Size 
in last 7 days.  
AND 
Abandoned Cart 
AND 
Loyalty member 
```

<!-- ![image](assets/luma-abandon.png)-->

因为Sarah在购物车中添加了一个明显的礼品并放弃了，Luma可以通过免费赠品包装来锁定她。

## 目标

添加“赠品购物车放弃者”区段后，您可以大致查看有多少人属于此区段。 您可以对其执行操作，并使其可用于跨渠道个性化。

选择 **[!UICONTROL 发送到目标]**.

在Real-Time CDP中，Luma可无缝地对其受众区段进行操作以实现个性化。\
在这里，我们看到可供Luma将此目标发送到Adobe解决方案和非Adobe解决方案的所有目标：

![image](assets/luma-dest.png)

### 选择目标

在此方案中，Luma希望通过在这些目标间进行个性化来重新定位此受众：

* Google，用于显示

   <!--* Facebook -->
* Adobe Campaign，用于电子邮件

<!-- ![image](assets/luma-sched-dest.png) -->

### 计划目标

您还可以安排在特定时间开始或结束区段。 该区段将在计划的日期在配置的平台中发布并自动更新。

>[!NOTE]
>
>（可选）如果您选择日期字段，则该字段会自动安排90天过期。

选择 **[!UICONTROL 保存]** 转到下一页。

当该受众中的客户购买产品时，他们对该受众的成员资格会实时被禁止。 他们不再符合条件，因为其状态已更改。

这样一来，Luma媒体团队的主管就无需为不符合条件的受众耗尽库存，从而节省了数十万美元。

### 实施目标的数据使用策略

Adobe Experience Platform包含隐私和安全控制，用于确定区段是否可用于激活到特定目标。 激活的启用或限制取决于创建目标时分配给目标的营销目的以及贵组织定义的数据使用策略。

如果活动违反策略，则会显示警告。 此警告包含数据谱系信息，可以帮助您确定违反策略的原因以及解决违规的方法。

有了这些控制项， [!DNL Experience Platform] 帮助Luma负责任地遵守法规和市场。 这些控制非常灵活，可以修改以满足Luma安全和治理团队的要求，使他们能够自信地满足区域和组织管理已知和未知客户数据的要求。

### 数据流画布

保存后，可视化数据流画布会显示从统一配置文件映射到您选择的三个目标的区段。

![image](assets/luma-flow.png)

## 跨设备身份拼合

Sarah在她的移动设备上浏览了一个社交媒体网站，她看到了一个Luma广告。 这让她想起了她购物车里留下的东西。

稍后，她打开电子邮件，看到重新定位的电子邮件。 她从电子邮件中选择了指向Luma的链接。

通过链接，Sarah将转到移动设备Luma主页，在那里她看到了由Adobe Target提供的高度个性化体验。

* 她作为铜牌成员受到欢迎。
* 她看到“礼物”的信息。
* 她还看到“免费赠品包装”讯息，这是她铜牌会员资格福利的一部分。
* 基于她对跑步的喜爱，她仍然成为英雄形象中的目标。

她买了这件毛衣，增加了礼品包装，并写了一张礼品单。 她还可以选择记住这个活动，并收到明年的提醒，以便在这个时候收到礼物。 她说是的，并计划于次年发起电子邮件促销活动，提醒她再买一件礼物。

多亏了受众抑制功能，Sarah不会成为男士毛衣的攻击目标。

## 分析用户档案

Luma营销人员使用Adobe Experience Platform查看Real-Time CDP功能板上的礼品馈送区段。 他们看到这项计划随着时间推移而不断取得的成果，并看到其发展壮大。 客户对优惠做出响应并花费更多金钱。

通过这些洞察，营销人员能够针对此信号采取行动，通过在CDP中提供此数据以及将Sarah等客户附加到区段来推动这一行动。

Luma使用此CDP数据来提高忠诚度和客户满意度。
