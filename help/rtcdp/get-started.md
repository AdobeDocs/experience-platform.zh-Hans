---
keywords: RTCDP;CDP；实时客户数据平台；实时客户数据平台；实时cdp;cdp;rtcdp
title: 实时客户数据平台入门
description: 使用此情景作为示例，来设置您的 Real-time Customer Data Platform 实施
translation-type: tm+mt
source-git-commit: 00010d38a5d05800aeac9af8505093fee3593b45
workflow-type: tm+mt
source-wordcount: '2326'
ht-degree: 1%

---


# 实时客户数据平台入门

本入门指南引导您完成实时客户数据平台（实时CDP）的示例实施。 在设置自己的实现时，可以将它作为一个示例。 虽然本指南显示了特定示例，但它链接到您在创建安装程序时可以使用的其他信息。

此示例展示了由Adobe Experience Platform提供支持的实时客户数据平台在以下方面的强大功能：

* 从多个源摄取数据
* 将它们合并到单个[!DNL real-time customer profile]中
* 跨设备提供一致、相关和个性化的体验。

## 用例

运动服装公司Luma一直在努力改善客户体验。 他们有一项新计划，增加与礼品相关的销售。 他们还希望减少过度曝光，如关注客户的烦人广告。

目前，他们在媒体上的支出过多，这些媒体针对访客不愿购买的商品进行重新定位。 例如，Luma不希望将某个物品重新定位给某个人，该物品原本是为某人一次性购买的。

目前，Luma的数据分散在多个来源。 因此，他们面临着重大挑战：

* 营销组织必须与各自拥有数据源的不同团队合作，包括网站、移动应用、忠诚度系统、CRM等。
* 当营销团队获得数据时，数据往往已经过时，与他们对时间敏感的活动不再相关。
* 他们需要统一数据，以便目标一个人，而不是渠道。

因此，Luma有以下业务目标：

* 根据不同的视图来源为消费者创建实时单一数据。
* 利用不同活动和设备间的相关信息个性化营销渠道。

要实现这些目标，营销团队需要能够大规模地管理客户数据。

借助以Adobe Experience Platform为后盾的实时CDP,Luma的营销组织可以：

1. 从不同的平台收集数据并确保数据在下游可供其他营销活动使用。
1. 创建消费者的单一实时视图，不受数据来源的影响。
1. 在每个接触点提供一致、相关和个性化的体验。

## 步骤

本教程包括以下步骤：

1. 构建[客户用户档案](#customer-profile)。
1. [个性](#personalizing-the-user-experience) 化用户体验。
1. 使用[多个数据源](#using-multiple-data-sources)。
1. [配置数据源](#configuring-a-data-source)。
1. [收集特](#bringing-the-data-together-for-a-specific-customer) 定客户的数据。
1. 设置[段](#segments)。
1. 设置[目标](#destinations)。
1. [跨设备拼接用户档案](#cross-device-identity-stitching)。
1. [分析用户档案](#analyzing-the-profile)。

## 客户用户档案

当客户首次访问您的网站时，您对他们一无所知。

![image](assets/luma-site.png)

在导航时，数据会实时捕获并不仅发送到Adobe Analytics的报表包，还会直接发送到Adobe Experience Platform。 在收集数据时，您会开始根据[!DNL Experience Platform's real-time customer profile]中的行为数据，形成消费者的单个视图。

网站的许多访客可能重复以前从Luma购买的客户。  对Luma来说，为满足新客户和重复访客以及已知客户的需求而个性化消息和产品非常重要。

### 新客户的首次访问

例如，一个统一身份的访客导航到Luma站点上的“男人”部分，并视图一对运行运动衫的夫妇。

![图像](assets/luma-sweatshirts.png)

当客户导航以了解有关这些产品的更多信息时，这些产品视图会在Adobe Analytics收集并发送到[!DNL Experience Platform]。

<!--![image](assets/luma-shirt-detail.png)-->

Luma可以将访客的行为映射到Adobe Experience Platform的用户用户档案，并开始汇集更丰富的消费者行为视图。

### 获得更详细的客户视图

随着客户继续与网站互动，将呈现更加清晰的画面。 例如，假定访客将产品添加到购物车并登录。

客户登录时，她将自己标识为莎拉·罗丝。

![图像](assets/luma-login.png)

合并了两个标识：

* 匿名浏览数据
* 与莎拉·罗丝的账户相关的现有数据

在[!DNL Experience Platform]中，两个标识都合并为一个用户档案。 Luma现在对此消费者有统一的视图。

根据网站“男士”部分的匿名访客的浏览行为，可能假定该客户为男性。 现在她登录了，Luma认识了Sarah Rose。 Luma使用[!DNL Real-time Customer Profile]的强大功能来优化跨渠道提供给她的消息。

## 个性化用户体验

Sarah受到欢迎，并感谢她成为铜牌会员，详细了解她的益处以及如何提高地位和积分。

她导航到主页去浏览更多。

![图像](assets/luma-personal.png)

Sarah会根据她在Adobe Experience Platform的[!DNL Real-time Customer Profile]获得动态提供的个性化主页体验。

在Adobe Target,Adobe Sensei推动的个性化让她看到了相关内容，它考虑了她过去购买服装和服装的情况和关联。 Luma还根据她最近的浏览，为男性定制了男性跑步用品目录。

在下一页，Sarah将看到特色产品，并根据她最近查看过的产品推出新的推荐托盘。

这个个性化内容可帮助Sarah快速找到相关项目。 这提高了转化率并提供了更愉悦的客户体验。

### 将客户带回

莎拉分心了，离开了网站，结束了她的研习会。 Luma可以利用她在Adobe Experience Platform的数据帮助她回到网站。

实时客户数据平台由Adobe Experience Platform公司提供支持，专为客户体验管理而构建。 它使组织能够：

* 简化数据集成和激活
* 管理已知和未知的数据使用
* 大规模加速营销使用案例

## 使用多个数据源

Luma团队将所有的行为和客户数据放在一个位置。

![图像](assets/luma-dash.png)

他们可以从以下所有源中收集数据：

* 现有Adobe Experience Cloud解决方案数据
* 非Adobe来源，如Luma的忠诚项目、呼叫中心和销售点系统数据
* 来自Luma数据源的实时流数据
* 来自Adobe解决方案的实时数据（无需新标签）

所有这些来自不同来源的数据都合并为一个统一的客户用户档案。

## 配置数据源

使用[!DNL Real-time Customer Data Platform]将新数据源引入平台。 实时CDP包括一个数据源目录，可以快速、轻松地添加到用户档案。

![图像](assets/luma-source-cat.png)

例如，要获取Luma的CRM数据，请按&#x200B;*CRM*&#x200B;筛选目录，并列出所有包含&#x200B;*CRM*&#x200B;的现成连接器。 要添加[!DNL Microsoft Dynamics CRM]数据：

1. 授权连接。

   ![图像](assets/luma-source-auth.png)

1. 从建议的XDM预映射表列表中选择要导入的内容。

   <!--    ![image](assets/luma-source-import.png) -->

   例如，选择&#x200B;**[!UICONTROL 联系人]**。 预览的联系人数据会自动加载，这样您就可以确保一切看起来都符合预期。

   Adobe Experience Platform通过自动将标准字段映射到[!DNL Experience Data Model](XDM)用户档案模式，从而节省了大量手动工作。

1. 查看字段映射。

   <!--    ![image](assets/luma-source-mapping.png) -->

   例如，多次检查是否正确映射了联系人的电子邮件字段。\
   您可以选择预览数据并执行高级映射。

1. 设置计划。

   ![图像](assets/luma-source-sched.png)

已经完成了。 您刚刚将[!DNL Microsoft CRM]作为数据源添加到[!DNL Experience Platform]中。

### 为使用策略标记所摄取的数据

Luma有许多内部策略限制某些类型收集信息的使用，并且还必须遵守与数据使用相关的法律和隐私相关的顾虑。 使用Adobe Experience Platform[!DNL Data Governance]，预定义的数据使用标签可以应用于数据集（以及这些数据集中的特定字段），从而允许Luma根据特定的使用限制对其数据进行分类。

![](assets/governance-labels.png)

应用数据使用标签后，Luma可以使用[!DNL Data Governance]创建数据使用策略。 数据使用策略是描述允许对包含特定标签的数据执行的操作种类的规则。 当尝试在构成策略违规的实时CDP中执行某个操作时，会阻止该操作，并会发出警报以显示违反了哪些策略以及原因。

## 整合特定客户的数据

在此情景中，搜索Sarah Rose的用户档案。 她的用户档案出现了，她用来登录的电子邮件也出现了。

<!-- ![image](assets/luma-find-profile.png) -->

Luma有关Sarah的所有用户档案信息。 这包括她的个人信息，如地址和电话号码、通信首选项以及她有资格获得的区段。

| 类别 | 描述 |
|---|---|
| 身份 | 显示在[!DNL Platform]中通过Sarah与Luma的交互关联到的身份，这些身份跨越渠道和设备。 将显示网站中的ECID。 她的身份还包括其移动应用程序的ECID、电子邮件ID、最近添加的[!DNL Microsoft Dynamics]数据集的CRM ID，以及从Luma忠诚度系统传入Adobe Experience Platform的忠诚度ID。 |
| 事件 | 显示Sarah与Luma品牌的所有交互数据。 这包括她刚刚查看的物品，她过去查看过的任何东西，她收到的电子邮件，她与呼叫中心的互动，以及每次互动的渠道和设备。 |

实时CDP用户档案将Luma营销团队的工作流程从数周减少到数分钟，并根据这一360度全方位客户视图为个性化解锁了可能。 用户档案将她登录前浏览网站时的行为数据与她现有的客户用户档案相结合，为Sarah创建了全面的视图。

营销团队可以使用这款增强的[!DNL Real-time Customer Profile]，更好地个性化Sarah的体验，并提高她对Luma的品牌忠诚度。

## 区段

强大的Adobe Experience Platform细分功能使营销人员能够根据[!DNL Real-time Customer Profile]中捕获的数据组合属性、事件和现有细分。

<!-- ![image](assets/luma-segments.png) -->

在这种情况下，Sarah最近在网站上的交互行为与她过去的行为不同。 她通常买女装。 但是，她购物车中的物品是男人的大运动衫。

Luma数据科学团队围绕购买倾向创建了模型。 一个模型标识了现有消费者服装类别（例如男性／女性）或尺寸的突然变化。 莎拉在购买行为上的改变表明她不是在为自己购物。

<!-- ![image](assets/luma-gift.png) -->

### 定义区段

修改或创建表示购物车放弃者的区段，这些放弃者似乎正在购买礼品：

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

由于Sarah在购物车中添加了一个明显的礼品项并放弃了它，Luma可以用免费的礼品包装目标她。

## 目标

添加“放弃购物车赠送礼物”区段后，您可以大致了解此区段中有多少人。 您可以对其采取行动，并使其可供渠道个性化。

选择&#x200B;**[!UICONTROL 发送到目标]**。

在实时CDP中，Luma可以无缝地对其受众细分采取行动，以实现个性化。\
在此，我们将看到Luma可以将此目标发送到的所有目标，包括Adobe和非Adobe解决方案：

![图像](assets/luma-dest.png)

### 选择目标

在此方案中，Luma希望通过以下目标的个性化来重新定位此受众:

* Google，用于展示

   <!--* Facebook -->
* Adobe Campaign，用于电子邮件

<!-- ![image](assets/luma-sched-dest.png) -->

### 计划目标

您还可以将区段计划为开始或在特定时间结束。 区段将在计划日期的已配置平台上发布并自动更新。

>[!NOTE]
>
>（可选）如果您选择日期字段，它将自动计划90天外。

选择&#x200B;**[!UICONTROL 保存]**&#x200B;以转到下一页。

当此受众中的客户进行购买时，其对此受众的会员资格会被实时抑制。 他们不再具备资格，因为他们的状态已经改变。

这样，Luma媒体团队的主管就可以省下几十万美元，因为他们没有将库存用于不符合条件的受众。

### 为目标实施数据使用策略

Adobe Experience Platform包括隐私和安全控制，用于确定区段是否可激活到特定目标。 激活根据创建时分配给目标的营销目的以及组织定义的数据使用策略启用或限制。

如果您的活动违反策略，将显示警告。 此警告包含数据世系信息，可帮助您确定违反策略的原因以及解决违规的方法。

通过这些控制，[!DNL Experience Platform]帮助Luma以负责任的方式遵守法规和营销。 这些控制是灵活的，可以修改以满足Luma安全和治理团队的要求，使他们能够自信地满足管理已知和未知客户数据的地区和组织要求。

### 数据流画布

保存时，可视化数据流画布会显示从统一用户档案映射到您选择的三个目标的区段。

![图像](assets/luma-flow.png)

## 跨设备身份拼接

Sarah在移动设备上浏览一个社交媒体网站，她看到一则Luma广告。 这让她想起她在车里留下的物品。

之后，她打开自己的电子邮件，看到重新定位的电子邮件。 她从一封电子邮件中选择了Luma的链接。

该链接将Sarah带到移动Luma主页，她在那里看到由Adobe Target提供动力的高度个性化体验。

* 她被欢迎为铜牌会员。
* 她看到“礼物”的讯息。
* 她还看到“免费礼品包装”信息，这是她获得铜牌会员资格的优势之一。
* 她还是以自己的关联为目标，在英雄形象中。

她买毛衣，加礼物包，写礼物便条。 她还可以选择记住这个事件，明年就收到提醒，在这个时候送礼物。 她说是的，第二年她将在电子邮件活动里提醒她再买一份礼物。

由于受众抑制能力，莎拉不会成为男人毛衣的目标。

## 分析用户档案

Luma营销人员使用Adobe Experience Platform来查看实时CDP仪表板上的礼品提供者部分。 他们视图了这项计划的成果，并看到它正在增长。 客户正在响应优惠，投入更多资金。

这些洞察使营销人员能够针对这一信号采取行动，而这一信号的推动因素是让CDP中提供此数据，并让像Sarah这样的客户加入该细分。

Luma使用此CDP数据来提高忠诚度和客户满意度。
