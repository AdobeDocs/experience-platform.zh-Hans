---
keywords: Experience Platform；主页；热门主题；命名空间;命名空间;命名空间;命名空间；身份命名空间；身份命名空间；身份；身份；身份；身份；身份；身份服务；身份服务
solution: Experience Platform
title: Adobe Experience Platform Identity Service
topic: overview
description: '身份命名空间是 Identity Service 的组件，充当与身份相关的上下文指示器。例如，它们将值“name@email.com”区分为电子邮件地址或数字CRM ID“443522”。 '
translation-type: tm+mt
source-git-commit: 0547c33e831fe1ac684f55a0e79978cd7f191e65
workflow-type: tm+mt
source-wordcount: '1475'
ht-degree: 2%

---


# 身份命名空间概述

身份命名空间是[[!DNL Identity Service]](./home.md)的一个组件，用作身份相关上下文的指示器。 例如，它们将“name<span>@email.com”的值区分为电子邮件地址，或将“443522”区分为数字CRM ID。

## 入门指南

与身份命名空间合作需要了解所涉的Adobe Experience Platform各项服务。 在开始与命名空间合作之前，请查看以下服务的相关文档：

- [[!DNL Real-time Customer Profile]](../profile/home.md):根据来自多个来源的汇总数据，实时提供统一的客户用户档案。
- [[!DNL Identity Service]](./home.md):通过跨设备和系统桥接身份，更好地视图个别客户及其行为。
- [[!DNL Privacy Service]](../privacy-service/home.md):身份命名空间用于遵守一般数据保护规定(GDPR)，在该规定中，GDPR请求可以与命名空间相关。

## 了解身份命名空间

完全限定的标识包括ID值和命名空间。 在用户档案片段之间匹配记录数据时，如[!DNL Real-time Customer Profile]合并用户档案数据时，标识值和命名空间必须匹配。

例如，两个用户档案片段可能包含不同的主ID，但它们共享“Email”命名空间的相同值，因此[!DNL Platform]能够看到这些片段实际上是同一个人，并将数据整合到个人的标识图中。

![](images/identity-service-stitching.png)

### 身份类型

数据可以由多种不同的标识类型进行标识。 标识类型在创建标识命名空间时指定，并控制数据是否会保留到标识图以及如何处理该数据的任何特殊说明。

[!DNL Platform]中提供以下标识类型：

| 身份类型 | 描述 |
| --- | --- |
| Cookie ID | Cookie ID标识Web浏览器。 这些身份对于扩展是至关重要的，并且构成了身份图的大部分。 然而，从本质上讲，它们会迅速衰退，并随着时间的推移而失去价值。 |
| 跨设备ID | 跨设备ID可识别个人，通常将其他ID绑定在一起。 例如，登录ID、CRM ID和忠诚度ID。 这是[!DNL Identity Service]灵敏地处理该值的指示。 |
| 设备ID | 设备ID可识别硬件设备，如IDFA（iPhone和iPad）、GAID(Android)和RIDA(Roku)，并可由家庭中的多人共享。 |
| 电子邮件地址 | 电子邮件地址通常与单个人关联，因此可用于在不同渠道识别该人。 此类型的身份包括个人身份信息(PII)。 这是[!DNL Identity Service]灵敏地处理该值的指示。 |
| 非人员标识符 | 非人员ID用于存储需要命名空间但未连接到人群集的标识符。 例如，产品SKU、与产品、组织或商店相关的数据。 |
| 电话号码 | 电话号码通常与单个人关联，因此可用于在不同渠道识别该人。 此类型的身份包括PII。 这表示[!DNL Identity Service]能够灵敏地处理该值。 |

### 标准命名空间

Experience Platform提供了可供所有组织使用的多个身份命名空间。 这些命名空间称为标准API，可使用[!DNL Identity Service] API或通过平台UI查看。

以下标准命名空间供平台内的所有组织使用：

| 显示名称 | 描述 |
| ------------ | ----------- |
| AdCloud | 一个命名空间，表示AdobeAdCloud。 |
| Adobe Analytics（传统ID） | 代表Adobe Analytics的命名空间。 有关详细信息，请参见[Adobe Analytics命名空间](https://experienceleague.adobe.com/docs/analytics/admin/data-governance/gdpr-namespaces.html?lang=en#namespaces)上的以下文档。 |
| Apple IDFA（广告商的ID） | 代表广告商Apple ID的命名空间。 有关详细信息，请参阅[基于兴趣的广告](https://support.apple.com/en-us/HT202074)的以下文档。 |
| Apple推送通知服务 | 表示使用Apple推送通知服务收集的身份的命名空间。 有关详细信息，请参阅[Apple推送通知服务](https://developer.apple.com/library/archive/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/APNSOverview.html#//apple_ref/doc/uid/TP40008194-CH8-SW1)的以下文档。 |
| CORE | 代表Adobe Audience Manager的命名空间。 此命名空间也可通过其旧名称引用：“Adobe AudienceManager”。 有关详细信息，请参见[Audience ManagerID](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-privacy/data-privacy-reference/data-privacy-ids.html?lang=en#aam-ids)上的以下文档。 |
| ECID | 表示ECID的命名空间。 此命名空间还可以由以下别名引用：“Adobe Marketing CloudID”、“Adobe Experience CloudID”、“Adobe Experience PlatformID”。 有关详细信息，请参见[ECID](./ecid.md)上的以下文档。 |
| 电子邮件 | 表示电子邮件地址的命名空间。 此类命名空间通常与单个人关联，因此可用于在不同渠道中识别该人。 |
| 电子邮件（SHA256，小写） | 用于预散列电子邮件地址的命名空间。 此命名空间中提供的值在使用SHA256进行哈希处理前转换为小写。 在将电子邮件地址标准化之前，需要修剪前导和尾部空格。 此设置不能逆向更改。 有关详细信息，请参见[SHA256哈希支持](https://experienceleague.adobe.com/docs/id-service/using/reference/hashing-support.html?lang=en#hashing-support)的以下文档。 |
| Firebase Cloud消息传递 | 一个命名空间，它表示使用Google Firebase Cloud Messaging收集的用于推送通知的身份。 有关详细信息，请参阅[Google Firebase Cloud Messaging](https://firebase.google.com/docs/cloud-messaging)上的以下文档。 |
| Google广告ID(GAID) | 表示Google Advertising ID的命名空间。 有关详细信息，请参阅[Google Advertising ID](https://support.google.com/googleplay/android-developer/answer/6048248?hl=en)上的以下文档。 |
| Google点击ID | 表示Google Click ID的命名空间。 有关详细信息，请参阅[单击Google Ads](https://developers.google.com/adwords/api/docs/guides/click-tracking)中的跟踪文档。 |
| Phone | 表示电话号码的命名空间。 此类命名空间通常与单个人关联，因此可用于在不同渠道中识别该人。 |
| 电话(E.164) | 一个命名空间，它表示需要散列化为E.164格式的原始电话号码。 E.164格式包括加号(`+`)、国际国家／地区呼叫代码、本地区代码和电话号码。 例如：`(+)(country code)(area code)(phone number)`。 |
| 电话(SHA256) | 一个命名空间，表示需要使用SHA256散列处理的电话号码。 必须删除符号、字母和任何前导零。 您还必须添加国家／地区调用代码作为前缀。 |
| 电话(SHA256_E.164) | 一个命名空间，表示需要使用SHA256和E.164格式散列处理的原始电话号码。 |
| TNTID | 代表Adobe Target的命名空间。 有关详细信息，请参见[目标](https://experienceleague.adobe.com/docs/target/using/target-home.html?lang=en)的以下文档。 |
| Windows AID | 表示Windows广告ID的命名空间。 有关详细信息，请参阅[Windows广告ID](https://docs.microsoft.com/en-us/uwp/api/windows.system.userprofile.advertisingmanager.advertisingid?view=winrt-19041)上的以下文档。 |

要在UI中视图标准命名空间，请在左侧导航中选择&#x200B;**[!UICONTROL 标识]**，然后选择&#x200B;**[!UICONTROL 浏览]**&#x200B;选项卡以显示组织可以访问的标准标识命名空间列表。 您可以按命名空间的&#x200B;**[!UICONTROL 显示名称]**、**[!UICONTROL 标识符]**&#x200B;或&#x200B;**[!UICONTROL 所有者]**&#x200B;按字母顺序对其排序。 或者，也可以按命名空间的最近更新日期按时间顺序排序。

选择命名空间，在右边栏上查看更多特定信息。

>[!NOTE]
>
>平台还为集成提供命名空间。 默认情况下，这些命名空间是隐藏的，因为它们用于连接其他系统，而不用于拼合身份。 要视图集成命名空间，请选择&#x200B;**[!UICONTROL 视图集成标识]**。

![](./images/browse-namespaces.png)

## 管理自定义命名空间

根据组织数据和使用案例，您可能需要自定义命名空间。 可以使用[[!DNL Identity Service]](./api/create-custom-namespace.md) API或通过UI创建自定义命名空间。

要使用UI创建自定义命名空间，请导航到&#x200B;**[!UICONTROL Identity]**&#x200B;工作区，选择&#x200B;**[!UICONTROL 浏览]**，然后选择&#x200B;**[!UICONTROL 创建标识命名空间]**。

![](./images/create.png)

出现&#x200B;**[!UICONTROL 创建标识命名空间]**&#x200B;对话框。 提供唯一的&#x200B;**[!UICONTROL 显示名称]**&#x200B;和&#x200B;**[!UICONTROL 标识符号]**，然后选择要创建的标识类型。 您还可以添加可选描述以进一步了解命名空间。 完成后，选择&#x200B;**[!UICONTROL 创建]**。

>[!IMPORTANT]
>
>您定义的命名空间对您的组织是私有的，并且需要唯一的标识符才能成功创建。

![](./images/create-namespace.png)

与标准命名空间类似，您可以从&#x200B;**[!UICONTROL 浏览]**&#x200B;选项卡中选择自定义命名空间，以视图其详细信息。 但是，使用自定义命名空间，您还可以从详细信息区域编辑其显示名称和说明。

>[!NOTE]
>
>创建命名空间后，将无法删除它，并且无法更改其标识符和类型。

## 命名空间身份数据

为身份提供命名空间取决于您提供身份数据的方法。 有关提供数据标识数据的详细信息，请参见[!DNL Identity Service]概述中关于提供标识数据](./home.md#supplying-identity-data-to-identity-service)的部分。[

## 后续步骤

现在，您已经了解了身份命名空间的主要概念，可以开始学习如何使用[标识图查看器](./ui/identity-graph-viewer.md)使用标识图。
