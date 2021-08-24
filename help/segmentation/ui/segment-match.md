---
keywords: Experience Platform；主页；热门主题；分段；区段匹配；区段匹配
solution: Experience Platform
title: 区段匹配概述
topic-legacy: overview
description: 区段匹配是Adobe Experience Platform中的一项区段共享服务，允许两个或更多Platform用户以安全、受管理和隐私友好的方式交换区段数据。
source-git-commit: ee59da6c075573af366403e1059b5318fb924d21
workflow-type: tm+mt
source-wordcount: '1982'
ht-degree: 1%

---


# （测试版）[!DNL Segment Match]概述

>[!IMPORTANT]
>
>[!DNL Segment Match] 当前为测试版。文档和功能可能会发生变化。

Adobe Experience Platform区段匹配是一项区段共享服务，允许两个或更多Platform用户以安全、受管理和隐私友好的方式交换区段数据。 [!DNL Segment Match] 使用平台隐私标准和个人标识符，如经过哈希处理的电子邮件、经过哈希处理的电话号码，以及设备标识符（如IDFA和GAID）。

通过[!DNL Segment Match]，您可以：

* 管理身份重叠流程。
* 查看共享前估计。
* 应用数据使用标签以控制是否可以与合作伙伴共享数据。
* 在发布信息源后维护共享的受众生命周期管理，并通过添加、删除和取消共享的功能继续动态交换数据。

[!DNL Segment Match] 使用身份重叠流程确保以安全且注重隐私的方式完成区段共享。**重叠的标识**&#x200B;是在您的区段和选定合作伙伴的区段中具有匹配项的标识。 在发送者和接收者之间共享区段之前，身份重叠过程会检查命名空间中的重叠以及发送者和接收者之间的同意检查。 要共享区段，必须通过两个重叠检查。

以下各节提供了有关[!DNL Segment Match]的详细信息，包括有关设置及其端到端工作流的详细信息。

## 设置

以下各节概述了如何设置和配置[!DNL Segment Match]:

### 设置身份数据和命名空间 {#namespaces}

开始使用[!DNL Segment Match]的第一步是确保根据支持的身份命名空间摄取数据。

身份命名空间是[Adobe Experience Platform Identity Service](../../identity-service/home.md)的组件。 每个客户身份都包含一个指示身份上下文的关联命名空间。 例如，命名空间可以将“name<span>@email.com”值区分为电子邮件地址或“443522”值作为数字CRM ID。

完全限定的标识包括ID值和命名空间。 当在配置文件片段之间匹配记录数据时（例如，当[!DNL Real-time Customer Profile]合并配置文件数据时），标识值和命名空间必须匹配。

在[!DNL Segment Match]的上下文中，共享数据时会在重叠过程中使用命名空间。

支持的命名空间列表如下所示：

| 命名空间 | 描述 |
| --------- | ----------- |
| 电子邮件（SHA256，小写） | 预哈希电子邮件地址的命名空间。 在使用SHA256进行哈希处理之前，此命名空间中提供的值将转换为小写。 在电子邮件地址被标准化之前，需要裁剪前导和尾随空格。 此设置不能以追溯方式更改。 有关更多信息，请参阅以下关于[SHA256哈希处理支持](https://experienceleague.adobe.com/docs/id-service/using/reference/hashing-support.html?lang=en#hashing-support)的文档。 |
| 电话(SHA256_E.164) | 表示需要使用SHA256和E.164格式进行哈希处理的原始电话号码的命名空间。 |
| ECID | 表示Experience CloudID(ECID)值的命名空间。 此命名空间也可以由以下别名引用：“Adobe Marketing Cloud ID”、“Adobe Experience Cloud ID”、“Adobe Experience Platform ID”。 有关更多信息，请参阅[ECID概述](../../identity-service/ecid.md) 。 |
| Apple IDFA（广告商的ID） | 表示广告商的Apple ID的命名空间。 有关更多信息，请参阅以下关于[基于兴趣的广告](https://support.apple.com/en-us/HT202074)的文档。 |
| Google广告ID | 表示Google广告ID的命名空间。 有关更多信息，请参阅[Google广告ID](https://support.google.com/googleplay/android-developer/answer/6048248?hl=en)上的以下文档。 |

### 设置同意配置

您必须提供同意配置，并将其默认值设置为`opt-in`或`opt-out`才能进行同意检查。

选择加入和选择退出同意检查决定您是否可以在获得同意的情况下运行以在默认情况下共享用户数据。 如果同意配置默认设置为`opt-in`，则可以共享用户数据，除非用户明确选择禁用。 如果默认设置为`opt-out`，则无法共享用户数据，除非用户明确选择。

[!DNL Segment Match]的默认同意配置设置为`opt-out`。 要为您的数据强制实施选择加入模型，请向您的Adobe客户经理发送电子邮件请求。

有关用于设置数据共享同意值的`share`属性的更多信息，请参阅以下关于[隐私和同意字段组](../../xdm/field-groups/profile/consents.md)的文档。 有关用于捕获消费者对收集和使用与隐私、个性化和营销首选项相关数据的同意的特定字段组的信息，请参阅以下[隐私、个性化和营销首选项的同意GitHub示例](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/consent/consent-preferences.schema.md)。

### 配置数据使用情况标签

您必须建立的最后一个先决条件是配置新的数据使用标签以防止数据共享。 通过数据使用标签，您可以管理允许通过[!DNL Segment Match]共享哪些数据。

数据使用情况标签允许您根据应用于该数据的使用策略对数据集和字段进行分类。 标签可随时应用，从而在您选择如何管理数据方面提供了灵活性。 最佳实践是：在将数据摄取到Experience Platform中后，或当数据在Platform中可用时，立即为数据设置标签。

[!DNL Segment Match] 使用C11标签，这是特定于的合同标签，您可 [!DNL Segment Match] 以手动将其添加到任何数据集或属性，以确保将其排除在合作 [!DNL Segment Match] 伙伴共享流程之外。C11标签表示不应在[!DNL Segment Match]进程中使用的数据。 在确定要从[!DNL Segment Match]中排除的数据集和/或字段并相应地添加了C11标签后，[!DNL Segment Match]工作流将自动强制实施该标签。 [!DNL Segment Match] 自动启用“限 [!UICONTROL 制数据共] 享核心”策略。有关如何将数据使用情况标签应用于数据集的特定说明，请参阅[在UI](../../data-governance/labels/user-guide.md)中管理数据使用情况标签的教程。

有关数据使用标签及其定义的列表，请参阅[数据使用标签术语表](../../data-governance/labels/reference.md)。 有关数据使用策略的信息，请参阅[数据使用策略概述](../../data-governance/policies/overview.md)。

### 了解[!DNL Segment Match]权限

有两个权限与[!DNL Segment Match]关联：

| 权限 | 描述 |
| --- | --- |
| 管理受众共享连接 | 此权限允许您完成合作伙伴握手过程，该过程会连接两个IMS组织以启用[!DNL Segment Match]流。 |
| 管理受众共享 | 此权限允许您与活动合作伙伴（已由管理员用户通过&#x200B;**[!UICONTROL 受众共享连接]**&#x200B;访问权限连接的合作伙伴）一起创建、编辑和发布信息源（用于[!DNL Segment Match]的数据包）。 |

有关访问控制和权限的更多信息，请参阅[访问控制概述](../../access-control/home.md) 。

## [!DNL Segment Match] 端到端工作流

设置身份数据和命名空间、同意配置和数据使用标签后，即可开始使用[!DNL Segment Match]及其功能。

### 管理合作伙伴

在Platform UI中，从左侧导航中选择&#x200B;**[!UICONTROL 区段]**，然后从顶部标题中选择&#x200B;**[!UICONTROL 馈送]**。

![segments-feed.png](../images/ui/segment-match/segments-feed.png)

[!UICONTROL 信息源]页面包含从合作伙伴处收到的信息源列表以及您共享的信息源。 要查看现有合作伙伴的列表或与新合作伙伴建立连接，请选择&#x200B;**[!UICONTROL 管理合作伙伴]**。

![manage-partners.png](../images/ui/segment-match/manage-partners.png)

两个合作伙伴之间的连接是一种“双向握手”，它充当用户在沙盒级别将其Platform组织连接在一起的自助服务方法。 需要建立连接，才能告知Platform已经建立协议，并且Platform可以帮助您与合作伙伴共享服务。

>[!NOTE]
>
>你和你的伴侣之间的“双向握手”完全是一种联系。 在此过程中不会交换任何数据。

您可以在[!UICONTROL 管理合作伙伴]屏幕的主界面中查看与现有合作伙伴的连接列表。 右边栏上是[!UICONTROL 共享设置]面板，该面板提供了用于生成新的[!UICONTROL 连接ID]的选项，以及一个输入框，您可以在其中输入合作伙伴的[!UICONTROL 连接ID]。

![sutalish-connection.png](../images/ui/segment-match/establish-connection.png)

要创建新的[!UICONTROL 连接ID]，请在[!UICONTROL 共享设置]下选择&#x200B;**[!UICONTROL 重新生成]**，然后选择新生成的ID旁边的复制图标。

![share-setting.png](../images/ui/segment-match/share-setting.png)

要使用[!UICONTROL 连接ID]连接合作伙伴，请在[!UICONTROL 连接合作伙伴]下的输入框中输入其唯一ID值，然后选择&#x200B;**[!UICONTROL 请求]**。

![connect-partner.png](../images/ui/segment-match/connect-partner.png)

### 创建馈送

**信息源**&#x200B;是数据（区段）的分组、数据如何公开或使用的规则，以及确定数据如何与合作伙伴数据匹配的配置。 可以通过[!DNL Segment Match]独立管理信息源并与其他平台用户交换信息源。

要创建新馈送，请从[!UICONTROL 馈送]功能板中选择&#x200B;**[!UICONTROL 创建馈送]**。

![create-feed.png](../images/ui/segment-match/create-feed.png)

信息源的基本设置包括有关营销用例和身份设置的名称、描述和配置。 为您的信息源提供名称和描述，然后应用您希望将数据从中排除的营销用例。 您可以从列表中选择多个用例，这些用例包括：

* [!UICONTROL Analytics]
* [!UICONTROL 与PII组合]
* [!UICONTROL 跨站点定位]
* [!UICONTROL 数据科学]
* [!UICONTROL 电子邮件定位]
* [!UICONTROL 导出到第三方]
* [!UICONTROL 现场广告]
* [!UICONTROL 现场个性化]
* [!UICONTROL 区段匹配]
* [!UICONTROL 单个身份个性化]

最后，为您的信息源选择适当的身份命名空间。 有关[!DNL Segment Match]支持的特定命名空间的信息，请参阅[标识数据和命名空间表](#namespaces)。 完成后，选择&#x200B;**[!UICONTROL Next]**。

![audience-sharing.png](../images/ui/segment-match/audience-sharing.png)

建立信息源设置后，从第一方区段列表中选择要共享的区段。 您可以从列表中选择多个区段，然后使用右边栏管理选定区段的列表。 完成后，选择&#x200B;**[!UICONTROL Next]**。

![select-segments.png](../images/ui/segment-match/select-segments.png)

此时会显示[!UICONTROL 共享]页面，该页面为您提供一个界面来选择要与之共享信息源的合作伙伴。 在此步骤中，您还可以查看预共享重叠估计报告，并按您与合作伙伴之间的命名空间查看重叠身份的数量，以及同意共享数据的重叠身份的数量。

选择&#x200B;**[!UICONTROL 按区段分析]**&#x200B;以查看估计报告。

![analyze.png](../images/ui/segment-match/analyze.png)

重叠估计报表允许您在共享信息源之前，管理每个合作伙伴和每个区段的重叠和同意检查。

| 量度 | 描述 |
| ------- | ----------- |
| 经同意的估计身份 | 符合为您的组织配置的同意要求的重叠身份总数。 |
| 估计重叠恒等式 | 符合选定区段资格且与选定合作伙伴具有匹配项的身份数。 这些标识按命名空间显示，而不代表单个配置文件标识。 重叠估计基于配置文件草图。 |

完成后，选择&#x200B;**[!UICONTROL 关闭]**。

![overlap-report.png](../images/ui/segment-match/overlap-report.png)

选择合作伙伴并查看重叠估计报告后，请选择&#x200B;**[!UICONTROL 下一步]**&#x200B;以继续。

![share.png](../images/ui/segment-match/share.png)

此时会显示[!UICONTROL 查看]步骤，允许您在共享和发布新信息源之前查看新信息源。 此步骤包括有关您应用的身份设置的详细信息，以及有关您选择的营销用例、区段和合作伙伴的信息。

选择&#x200B;**[!UICONTROL 完成]**&#x200B;以继续。

![review.png](../images/ui/segment-match/review.png)

### 更新馈送

要添加或删除区段，请从[!UICONTROL 馈送]页面中选择&#x200B;**[!UICONTROL 创建馈送]**，然后选择&#x200B;**[!UICONTROL 现有馈送]**。 在显示的现有馈送列表中，选择要更新的馈送，然后选择&#x200B;**[!UICONTROL Next]**。

![信息源列表](../images/ui/segment-match/feed-list.png)

此时会显示区段列表。 从此处，您可以向信息源添加新区段，并且可以使用右边栏删除不再需要的任何区段。 完成对信息源中区段的管理后，请选择&#x200B;**[!UICONTROL 下一步]**，然后按照上述步骤完成更新的信息源。

![更新](../images/ui/segment-match/update.png)

>[!NOTE]
>
>在从共享馈送添加或删除区段时，接收合作伙伴必须通过在其接收馈送列表中重新启用[!DNL Profile]切换开关来确认更改。

### 接受传入的馈送

要查看传入的馈送，请从[!UICONTROL 馈送]页面的标题中选择&#x200B;**[!UICONTROL 已接收]**，然后从列表中选择要查看的馈送。 要接受馈送，请选择&#x200B;**[!UICONTROL 为配置文件]**&#x200B;启用，并允许稍后将状态从[!UICONTROL Pending]更新为[!UICONTROL Enabled]。

![received.png](../images/ui/segment-match/received.png)

接受共享馈送后，您可以开始使用共享数据来构建新区段。

## 后续步骤

通过阅读本文档，您对[!DNL Segment Match]、其功能及其端到端工作流有了了解。 请参阅以下文档，了解有关其他Platform服务的更多信息：

* [[!DNL Segmentation Service]](../home.md)
* [[!DNL Identity Service]](../../identity-service/home.md)
* [[!DNL Real-time Customer Profile] 概述](../../profile/home.md)
