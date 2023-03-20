---
keywords: Experience Platform；主页；热门主题；命名空间；命名空间；命名空间；身份命名空间；身份命名空间；身份命名空间；身份；身份；身份；身份服务；身份服务
solution: Experience Platform
title: 身份命名空间概述
description: 身份命名空间是 Identity Service 的组件，充当与身份相关的上下文指示器。例如，它们将值“name@email.com”区分为电子邮件地址或“443522”作为数字CRM ID。
exl-id: 86cfc7ae-943d-4474-90c8-e368afa48b7c
source-git-commit: 482de6a50d14b9de095014b070ce400a2fd273cc
workflow-type: tm+mt
source-wordcount: '1681'
ht-degree: 7%

---

# 身份命名空间概述

身份命名空间是 [[!DNL Identity Service]](./home.md) 作为身份相关背景的指标。 例如，它们会区分“name”的值<span>@email.com”作为电子邮件地址，或“443522”作为数字CRM ID。

## 快速入门

使用身份命名空间需要了解所涉及的各种Adobe Experience Platform服务。 开始使用命名空间之前，请查阅以下服务的文档：

- [[!DNL Real-Time Customer Profile]](../profile/home.md):根据来自多个来源的汇总数据，实时提供统一的客户用户档案。
- [[!DNL Identity Service]](./home.md):通过跨设备和系统桥接身份，更好地了解各个客户及其行为。
- [[!DNL Privacy Service]](../privacy-service/home.md):身份命名空间用于法律隐私法规(如《通用数据保护条例》(GDPR))的合规请求中。 每个隐私请求都是相对于命名空间发出的，以便确定哪些消费者的数据应受到影响。

## 了解身份命名空间

完全限定的标识包括ID值和命名空间。 在配置文件片段之间匹配记录数据时，如 [!DNL Real-Time Customer Profile] 合并配置文件数据，标识值和命名空间必须匹配。

例如，两个配置文件片段可能包含不同的主ID，但它们共享“Email”命名空间的相同值，因此 [!DNL Platform] 能够了解这些片段实际上是同一个人，并将数据汇总到个人的标识图中。

![](images/identity-service-stitching.png)

### 身份类型 {#identity-types}

>[!CONTEXTUALHELP]
>id="platform_identity_create_namespace"
>title="指定标识类型"
>abstract="标识类型控制数据是否存储到标识图形中。非人员标识符不会被存储，所有其他标识类型都会被存储。"
>text="Learn more in documentation"

数据可以由多种不同的身份类型来标识。 标识类型在创建标识命名空间时指定，并控制数据是否持久保留到标识图以及如何处理该数据的任何特殊说明。 除 **非人员标识符** 请按照拼合命名空间及其相应ID值的相同行为，将这些值拼合到标识图群集。 使用 **非人员标识符**.

在 [!DNL Platform]:

| 身份类型 | 描述 |
| --- | --- |
| Cookie ID | Cookie ID可识别Web浏览器。 这些身份对于扩展至关重要，并且构成了身份图的大多数。 但是，从本质上讲，它们会迅速衰减，并随着时间的推移而失去价值。 |
| 跨设备ID | 跨设备ID可识别个人ID，并且通常会将其他ID绑定在一起。 示例包括登录ID、CRM ID和忠诚度ID。 这表示 [!DNL Identity Service] 以灵敏地处理这个值。 |
| 设备ID | 设备ID可识别硬件设备，如IDFA(iPhone和iPad)、GAID(Android)和RIDA(Roku)，并可由家庭中的多人共享。 |
| 电子邮件地址 | 电子邮件地址通常与单个人员关联，因此可用于在不同渠道中识别该人员。 此类型的身份包括个人身份信息(PII)。 这表示 [!DNL Identity Service] 以灵敏地处理这个值。 |
| 非人员标识符 | 非人员ID用于存储需要命名空间但未连接到人员群集的标识符。 例如，产品SKU、与产品、组织或商店相关的数据。 |
| 电话号码 | 电话号码通常与单个人员关联，因此可用于在不同渠道中识别该人员。 此类型的身份包括PII。 这表示 [!DNL Identity Service] 以灵敏地处理这个值。 |

### 标准命名空间 {#standard}

Experience Platform提供了多个适用于所有组织的身份命名空间。 这些命名空间称为标准命名空间，可使用 [!DNL Identity Service] API或通过平台UI。

平台内的所有组织都可以使用以下标准命名空间：

| 显示名称 | 描述 |
| ------------ | ----------- |
| AdCloud | 表示AdobeAdCloud的命名空间。 |
| Adobe Analytics（旧版ID） | 表示Adobe Analytics的命名空间。 请参阅以下文档(位于 [Adobe Analytics命名空间](https://experienceleague.adobe.com/docs/analytics/admin/data-governance/gdpr-namespaces.html?lang=en#namespaces) 以了解更多信息。 |
| Apple IDFA（广告商的ID） | 表示广告商的Apple ID的命名空间。 请参阅以下文档(位于 [基于兴趣的广告](https://support.apple.com/en-us/HT202074) 以了解更多信息。 |
| Apple推送通知服务 | 表示使用Apple推送通知服务收集的身份的命名空间。 请参阅以下文档(位于 [Apple推送通知服务](https://developer.apple.com/library/archive/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/APNSOverview.html#//apple_ref/doc/uid/TP40008194-CH8-SW1) 以了解更多信息。 |
| CORE | 表示Adobe Audience Manager的命名空间。 此命名空间也可以通过其旧名称引用：“Adobe AudienceManager”。 请参阅以下文档(位于 [Audience ManagerID](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-privacy/data-privacy-reference/data-privacy-ids.html?lang=en#aam-ids) 以了解更多信息。 |
| ECID | 表示ECID的命名空间。 此命名空间也可以由以下别名引用：“Adobe Marketing Cloud ID”、“Adobe Experience Cloud ID”、“Adobe Experience Platform ID”。 请参阅以下文档(位于 [ECID](./ecid.md) 以了解更多信息。 |
| 电子邮件 | 表示电子邮件地址的命名空间。 此类命名空间通常与单个人员关联，因此可用于跨不同渠道识别该人员。 |
| 电子邮件（SHA256，小写） | 预哈希电子邮件地址的命名空间。 在使用SHA256进行哈希处理之前，此命名空间中提供的值将转换为小写。 在电子邮件地址被标准化之前，需要裁剪前导和尾随空格。 此设置不能以追溯方式更改。 请参阅以下文档(位于 [SHA256哈希处理支持](https://experienceleague.adobe.com/docs/id-service/using/reference/hashing-support.html?lang=en#hashing-support) 以了解更多信息。 |
| Firebase Cloud消息传送 | 表示使用Google Firebase Cloud Messaging收集的推送通知身份的命名空间。 请参阅以下文档(位于 [Google Firebase Cloud Messaging](https://firebase.google.com/docs/cloud-messaging) 以了解更多信息。 |
| Google广告ID(GAID) | 表示Google广告ID的命名空间。 请参阅以下文档(位于 [Google Advertising ID](https://support.google.com/googleplay/android-developer/answer/6048248?hl=en) 以了解更多信息。 |
| Google Click ID | 表示Google点击ID的命名空间。 请参阅以下文档(位于 [Google广告中的点击跟踪](https://developers.google.com/adwords/api/docs/guides/click-tracking) 以了解更多信息。 |
| Phone | 表示电话号码的命名空间。 此类命名空间通常与单个人员关联，因此可用于跨不同渠道识别该人员。 |
| 电话(E.164) | 表示需要以E.164格式进行哈希处理的原始电话号码的命名空间。 E.164格式包含一个加号(`+`)、国际国家/地区电话代码、地区代码和电话号码。 例如：`(+)(country code)(area code)(phone number)`。 |
| 电话(SHA256) | 表示需要使用SHA256进行哈希处理的电话号码的命名空间。 必须删除符号、字母和任何前导零。 您还必须添加国家/地区调用代码作为前缀。 |
| 电话(SHA256_E.164) | 表示需要使用SHA256和E.164格式进行哈希处理的原始电话号码的命名空间。 |
| TNTID | 表示Adobe Target的命名空间。 请参阅以下文档(位于 [Target](https://experienceleague.adobe.com/docs/target/using/target-home.html?lang=en) 以了解更多信息。 |
| Windows AID | 表示Windows广告ID的命名空间。 请参阅以下文档(位于 [Windows广告ID](https://docs.microsoft.com/en-us/uwp/api/windows.system.userprofile.advertisingmanager.advertisingid?view=winrt-19041) 以了解更多信息。 |

### 查看身份命名空间 {#view-identity-namespaces}

>[!CONTEXTUALHELP]
>id="platform_identity_view_integration_identities"
>title="查看集成标识"
>abstract="集成身份是用于连接其他系统的命名空间，不用于标识解析或拼接标识。<br>默认情况下，这些标识是隐藏的。使用切换功能来查看集成命名空间。"

要在UI中查看身份命名空间，请选择 **[!UICONTROL 标识]** 在左侧导航中，然后选择 **[!UICONTROL 浏览]**.

![浏览器](./images/browse.png)

身份命名空间列表会显示在页面的主界面中，其中显示了有关其名称、身份符号、上次更新日期以及它们是标准命名空间还是自定义命名空间的信息。 右边栏包含有关 [!UICONTROL 身份图强度].

![标识](./images/identities.png)

平台还提供命名空间以用于集成。 这些命名空间默认处于隐藏状态，因为它们用于与其他系统连接，而不用于拼合身份。 要查看集成命名空间，请选择 **[!UICONTROL 查看集成标识]**.

![view-integration-identities](./images/view-integration-identities.png)

从列表中选择标识命名空间以查看有关特定命名空间的信息。 选择身份命名空间会更新右边栏中的显示，以显示与您选择的身份命名空间相关的元数据，包括摄取的身份数和失败和跳过的记录数。

![select-namespace](./images/select-namespace.png)

## 管理自定义命名空间 {#manage-namespaces}

根据您的组织数据和用例，您可能需要自定义命名空间。 自定义命名空间可使用 [[!DNL Identity Service]](./api/create-custom-namespace.md) API或通过UI。

要使用UI创建自定义命名空间，请导航到 **[!UICONTROL 标识]** 工作区，选择 **[!UICONTROL 浏览]**，然后选择 **[!UICONTROL 创建身份命名空间]**.

![select-create](./images/select-create.png)

的 **[!UICONTROL 创建身份命名空间]** 对话框。 提供唯一 **[!UICONTROL 显示名称]** 和 **[!UICONTROL 身份符号]** 然后，选择要创建的身份类型。 您还可以添加可选描述以添加有关命名空间的更多信息。 除 **非人员标识符** 遵循与拼合相同的行为。 如果您选择 **非人员标识符** 作为创建命名空间时的身份类型，不会进行拼合。 有关每种身份类型的特定信息，请参阅 [身份类型](#identity-types).

完成后，选择 **[!UICONTROL 创建]**.

>[!IMPORTANT]
>
>您定义的命名空间对您的组织是私有的，并且需要唯一的身份符号才能成功创建。

![create-identity-namespace](./images/create-identity-namespace.png)

与标准命名空间类似，您可以从 **[!UICONTROL 浏览]** 选项卡，以查看其详细信息。 但是，使用自定义命名空间，您还可以从详细信息区域编辑其显示名称和描述。

>[!NOTE]
>
>创建命名空间后，无法删除该命名空间，也无法更改其标识符和类型。

## 身份数据中的命名空间

提供身份的命名空间取决于您用于提供身份数据的方法。 有关提供数据身份数据的详细信息，请参阅 [提供身份数据](./home.md#supplying-identity-data-to-identity-service) 在 [!DNL Identity Service] 概述。

## 后续步骤

现在，您已了解身份命名空间的主要概念，接下来可以开始了解如何使用 [身份图查看器](./ui/identity-graph-viewer.md).
