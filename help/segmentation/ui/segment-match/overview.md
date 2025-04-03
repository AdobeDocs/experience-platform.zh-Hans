---
keywords: Experience Platform；主页；热门主题；分段；区段匹配；区段匹配
solution: Experience Platform
title: 区段匹配概述
description: 区段匹配是Adobe Experience Platform中的区段共享服务，它允许两个或更多Experience Platform用户以安全、受管理和隐私友好的方式交换区段数据。
exl-id: 4e6ec2e0-035a-46f4-b171-afb777c14850
source-git-commit: 0a9028beca36b46d6228c0038366bbac5d32603c
workflow-type: tm+mt
source-wordcount: '1978'
ht-degree: 3%

---

# [!DNL Segment Match] 概述

Adobe Experience Platform区段匹配是一项区段共享服务，允许两个或更多Experience Platform用户以安全、受管且隐私友好的方式交换区段数据。 [!DNL Segment Match]使用Experience Platform隐私标准和个人标识符，例如经过哈希处理的电子邮件、经过哈希处理的电话号码以及设备标识符（如IDFA和GAID）。

通过[!DNL Segment Match]，您可以：

* 管理身份重叠流程。
* 查看预共享估计。
* 应用数据使用标签以控制是否可与合作伙伴共享数据。
* 在发布馈送后维护共享的受众生命周期管理，并通过添加、删除和取消共享的功能继续动态交换数据。

[!DNL Segment Match]使用身份重叠过程以确保以安全和注重隐私的方式完成区段共享。 **重叠标识**&#x200B;是您的区段和所选合作伙伴的区段均匹配的标识。 在发送者和接收者之间共享区段之前，身份重叠过程检查命名空间中的重叠，并且在发送者和接收者之间检查同意情况。 为了共享区段，必须传递两次重叠检查。

以下部分提供了有关[!DNL Segment Match]的更多信息，包括有关设置及其端到端工作流的详细信息。

## 设置

以下各节概述了如何设置和配置[!DNL Segment Match]：

### 设置身份数据和命名空间 {#namespaces}

开始使用[!DNL Segment Match]的第一步是确保您正在根据支持的身份命名空间引入数据。

身份命名空间是[Adobe Experience Platform Identity Service](../../../identity-service/home.md)的组件。 每个客户身份都包含一个关联的命名空间，用于指示身份的上下文。 例如，命名空间可以将“name<span>@email.com”的值区分为电子邮件地址或“443522”区分为数字CRM ID。

完全限定的身份包括ID值和命名空间。 跨配置文件片段匹配记录数据时（例如，当[!DNL Real-Time Customer Profile]合并配置文件数据时），标识值和命名空间必须匹配。

在[!DNL Segment Match]的上下文中，共享数据时在重叠流程中使用命名空间。

支持的命名空间列表如下：

| 命名空间 | 描述 |
| --------- | ----------- |
| 电子邮件（SHA256，小写） | 预哈希电子邮件地址的命名空间。使用SHA256进行哈希处理之前，此命名空间中提供的值将转换为小写。 在规范化电子邮件地址之前，需要修剪前导空格和尾随空格。 此设置不能进行追溯性更改。 Experience Platform提供两种方法，通过[`setCustomerIDs`](https://experienceleague.adobe.com/docs/id-service/using/reference/hashing-support.html#hashing-support)和通过[数据准备](../../../data-prep/functions.md#hashing)来支持数据收集中的哈希处理。 |
| 电话(SHA256_E.164) | 表示需要使用 SHA256 和 E.164 格式进行哈希处理的原始电话号码的命名空间。 |
| ECID | 表示Experience Cloud ID (ECID)值的命名空间。 此命名空间还可以由以下别名引用：“Adobe Marketing Cloud ID”、“Adobe Experience Cloud ID”、“Adobe Experience Platform ID”。 有关详细信息，请参阅[ECID概述](../../../identity-service/features/ecid.md)。 |
| Apple IDFA（广告商的ID） | 表示广告商的Apple ID的命名空间。 有关详细信息，请参阅以下有关[基于兴趣的广告](https://support.apple.com/en-us/HT202074)的文档。 |
| Google Ad ID | 表示Google Advertising ID的命名空间。 有关详细信息，请参阅以下有关[Google Advertising ID](https://support.google.com/googleplay/android-developer/answer/6048248?hl=en)的文档。 |

### 设置同意配置

您必须提供同意配置并将其默认值设置为`opt-in`或`opt-out`以进行同意检查。

选择加入和选择退出同意检查确定默认情况下您能否在同意共享用户数据的情况下进行操作。 如果同意配置默认设置为`opt-out`，则除非用户明确选择退出，否则可以共享用户数据。 如果默认设置为`opt-in`，则无法共享用户数据，除非用户明确选择加入。

[!DNL Segment Match]的默认同意配置设置为`opt-out`。 要为您的数据强制实施选择加入模型，请向您的Adobe客户团队发送电子邮件请求。

有关用于设置数据共享同意值的`share`属性的更多信息，请参阅以下有关[隐私和同意字段组](../../../xdm/field-groups/profile/consents.md)的文档。 有关用于捕获消费者同意收集和使用隐私、个性化和营销偏好设置相关数据的特定字段组的信息，请参阅以下[隐私同意、Personalization和营销偏好设置GitHub示例](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/consent/consent-preferences.schema.md)。

### 配置数据使用标签

您必须建立的最后一个先决条件是配置新的数据使用标签以防止数据共享。 通过数据使用标签，您可以管理允许通过[!DNL Segment Match]共享的数据。

数据使用标签允许您根据应用于该数据的使用策略对数据集和字段进行分类。 您可以随时应用标签，灵活地选择管理数据的方式。 最佳实践鼓励在将数据摄取到Experience Platform中后立即为其设置标签，或者当数据在Experience Platform中可用时立即为其设置标签。

[!DNL Segment Match]使用C11标签，这是特定于[!DNL Segment Match]的合同标签，您可以手动将其添加到任何数据集或属性，以确保它们从[!DNL Segment Match]合作伙伴共享进程中排除。 C11标签表示不应在[!DNL Segment Match]进程中使用的数据。 在确定要从[!DNL Segment Match]中排除的数据集和/或字段并相应地添加C11标签后，[!DNL Segment Match]工作流将自动强制使用该标签。 [!DNL Segment Match]自动启用[!UICONTROL 限制数据共享]核心策略。 有关如何将数据使用标签应用于数据集的特定说明，请参阅有关[在UI中管理数据使用标签的教程](../../../data-governance/labels/user-guide.md)。

有关数据使用标签及其定义的列表，请参阅[数据使用标签术语表](../../../data-governance/labels/reference.md)。 有关数据使用策略的信息，请参阅[数据使用策略概述](../../../data-governance/policies/overview.md)。

### 了解[!DNL Segment Match]权限

有两个权限与[!DNL Segment Match]关联：

| 权限 | 描述 |
| --- | --- |
| 管理受众共享连接 | 此权限允许您完成伙伴握手过程，该过程连接两个组织以启用[!DNL Segment Match]流。 |
| 管理受众共享 | 此权限允许您通过活动合作伙伴（管理员用户已通过&#x200B;**[!UICONTROL 受众共享连接]**&#x200B;访问权限连接的合作伙伴）创建、编辑和发布信息源（用于[!DNL Segment Match]的数据包）。 |

有关访问控制和权限的详细信息，请参阅[访问控制概述](../../../access-control/home.md)。

## [!DNL Segment Match]端到端工作流

设置身份数据和命名空间、同意配置和数据使用标签后，即可开始使用[!DNL Segment Match]及其功能。

### 管理合作伙伴

在Experience Platform UI中，从左侧导航中选择&#x200B;**[!UICONTROL 区段]**，然后从顶部标题中选择&#x200B;**[!UICONTROL 馈送]**。

![segments-feed.png](./images/segments-feed.png)

[!UICONTROL 信息源]页面包含从合作伙伴收到的信息源列表以及您共享的信息源。 要查看现有合作伙伴列表或建立与新合作伙伴的连接，请选择&#x200B;**[!UICONTROL 管理合作伙伴]**。

![manage-partners.png](./images/manage-partners.png)

两个合作伙伴之间的连接是一种“双向握手”，作为一种自助方式，用户可在沙盒级别将其Experience Platform组织连接在一起。 需要建立连接，以通知Experience Platform已签订协议，并且Experience Platform可以促进您与合作伙伴之间共享服务。

>[!NOTE]
>
>你和你的伴侣之间的“双向握手”纯粹是一种联系。 在此过程中不会交换任何数据。

您可以在[!UICONTROL 管理合作伙伴]屏幕的主界面中查看与现有合作伙伴的连接列表。 右边栏上是[!UICONTROL 共享设置]面板，它为您提供了生成新的[!UICONTROL 连接ID]的选项，以及一个输入框，您可以在其中输入合作伙伴的[!UICONTROL 连接ID]。

![建立 — 连接.png](./images/establish-connection.png)

要创建新的[!UICONTROL 连接ID]，请在[!UICONTROL 共享设置]下选择&#x200B;**[!UICONTROL 重新生成]**，然后选择新生成的ID旁边的复制图标。

![share-setting.png](./images/share-setting.png)

若要使用合作伙伴的[!UICONTROL 连接ID]连接合作伙伴，请在[!UICONTROL 连接合作伙伴]下的输入框中输入其唯一ID值，然后选择&#x200B;**[!UICONTROL 请求]**。

![connect-partner.png](./images/connect-partner.png)

### 创建馈送 {#create-feed}

>[!CONTEXTUALHELP]
>id="platform_segment_match_marketing"
>title="受限的营销用例"
>abstract="受限的营销用例有助于为您的合作伙伴提供指导，确保根据您的数据治理限制正确使用共享区段。"
>text="Learn more in documentation"

**馈送**&#x200B;是一组数据（区段）、如何公开或使用该数据的规则以及确定如何将数据与合作伙伴的数据进行匹配的配置。 可通过[!DNL Segment Match]独立管理馈送并与其他Experience Platform用户交换。

要创建新馈送，请从[!UICONTROL 馈送]仪表板中选择&#x200B;**[!UICONTROL 创建馈送]**。

![create-feed.png](./images/create-feed.png)

信息源的基本设置包括名称、描述以及有关营销用例和身份设置的配置。 提供信息源的名称和描述，然后应用要将数据从中排除的营销用例。 您可以从列表中选择多个用例，其中包括：

* [!UICONTROL Analytics]
* [!UICONTROL 与PII合并]
* [!UICONTROL 跨站点定位]
* [!UICONTROL 数据科学]
* [!UICONTROL 电子邮件定位]
* [!UICONTROL 导出到第三方]
* [!UICONTROL 现场广告]
* [!UICONTROL 现场个性化]
* [!UICONTROL 区段匹配]
* [!UICONTROL 单一身份个性化]

最后，为信息源选择适当的身份命名空间。 有关[!DNL Segment Match]支持的特定命名空间的信息，请参阅[身份数据和命名空间表](#namespaces)。 完成后，选择&#x200B;**[!UICONTROL 下一步]**。

![受众共享.png](./images/audience-sharing.png)

建立信息源的设置后，从第一方区段列表中选择要共享的区段。 您可以从列表中选择多个区段，也可以使用右边栏管理选定区段的列表。 完成后，选择&#x200B;**[!UICONTROL 下一步]**。

![select-segments.png](./images/select-segments.png)

此时将显示[!UICONTROL 共享]页面，该页面为您提供了一个用于选择要与其共享信息源的合作伙伴的界面。 在此步骤中，您还可以查看预共享重叠估计报表，并查看您与合作伙伴之间按命名空间划分的重叠身份数，以及同意共享数据的重叠身份数。

选择&#x200B;**[!UICONTROL 按区段分析]**&#x200B;以查看估算报告。

![analyze.png](./images/analyze.png)

利用重叠估计报表，可在共享信息源之前管理每个合作伙伴和每个区段的重叠和同意检查。

| 量度 | 描述 |
| ------- | ----------- |
| 经同意的估计身份 | 符合为贵组织配置的同意要求的重叠身份总数。 |
| 估计的重叠身份 | 符合所选区段资格并与所选合作伙伴匹配的身份数。 这些身份按命名空间显示，不代表单个配置文件身份。 重叠估计基于轮廓草图。 |

完成后，选择&#x200B;**[!UICONTROL 关闭]**。

![overlap-report.png](./images/overlap-report.png)

选择合作伙伴并查看重叠估计报告后，选择&#x200B;**[!UICONTROL 下一步]**&#x200B;以继续。

![共享.png](./images/share.png)

将显示[!UICONTROL 审核]步骤，允许您在共享和发布新馈送之前对其进行审核。 此步骤包括有关您应用的身份设置的详细信息，以及有关您选择的营销用例、区段和合作伙伴的信息。

选择&#x200B;**[!UICONTROL 完成]**&#x200B;以继续。

![review.png](./images/review.png)

### 更新馈送

要添加或删除区段，请从[!UICONTROL 馈送]页面中选择&#x200B;**[!UICONTROL 创建馈送]**，然后选择&#x200B;**[!UICONTROL 现有馈送]**。 在显示的现有馈送列表中，选择要更新的馈送，然后选择&#x200B;**[!UICONTROL 下一步]**。

![信息源列表](./images/feed-list.png)

将显示区段列表。 在此处，您可以向信息源添加新区段，并可以使用右边栏删除不再需要的任何区段。 管理完信息源中的区段后，选择&#x200B;**[!UICONTROL 下一步]**，然后按照上述步骤完成更新的信息源。

![更新](./images/update.png)

>[!NOTE]
>
>当您从共享信息源中添加或删除区段时，接收合作伙伴必须通过在其接收信息源列表中重新启用[!DNL Profile]切换来确认更改。

### 接受传入馈送

要查看传入馈送，请从[!UICONTROL 馈送]页面的标题中选择&#x200B;**[!UICONTROL 已接收]**，然后从列表中选择要查看的馈送。 要接受馈送，请选择&#x200B;**[!UICONTROL 为配置文件]**&#x200B;启用，并等待片刻让状态从[!UICONTROL 待处理]更新为[!UICONTROL 已启用]。

![已接收.png](./images/received.png)

接受共享馈送后，您可以开始使用共享数据来构建新区段。

## 后续步骤

通过阅读本文档，您已了解[!DNL Segment Match]、其功能和端到端工作流程。 要了解有关其他Platform服务的更多信息，请参阅以下文档：

* [[!DNL Segmentation Service]](../../home.md)
* [[!DNL Identity Service]](../../../identity-service/home.md)
* [[!DNL Real-Time Customer Profile] 概述](../../../profile/home.md)
