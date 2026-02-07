---
title: XDM业务人员组件架构字段组
description: 了解XDM业务人员组件架构字段组。
badgeB2B: label="B2B edition" type="Informative" url="https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=zh-Hans#rtcdp-editions" newtab=true
exl-id: 965b89f4-59f5-43f4-8778-3549e15b44d4
source-git-commit: 3fafccef44823b80938db96a7751edbff5a2fd02
workflow-type: tm+mt
source-wordcount: '516'
ht-degree: 2%

---

# [!UICONTROL XDM Business Person Components]架构字段组

>[!AVAILABILITY]
>
>此字段组仅适用于有权访问Real-Time CDP B2B edition的组织。

[!UICONTROL XDM Business Person Components]是[[!DNL XDM Individual Profile] 类](../../classes/individual-profile.md)的标准架构字段组，可捕获人员的多个源记录以及人员分段所需的其他属性。

在Real-Time CDP的B2B edition中通过[实时客户个人资料](../../../profile/home.md)为某个人创建个人资料时，用于创建该个人资料的信息可能来自许多源记录。 例如，如果某人供职于两家不同的公司，则许多CRM系统将创建该人的有意重复副本，以便其中一个副本与公司A关联，而另一个副本与公司B关联。将数据引入Adobe Experience Platform时，此字段组用于将这些不同的源记录合并到单个表示形式中。

字段组提供了一个根级别`personComponents`字段，该字段是一个对象数组。 数组中的每个对象表示不同的源记录。

>[!IMPORTANT]
>
>必须按照[源文档](../../../rtcdp/sources/b2b.md)中所述的摄取模式操作。 不能保证其他字段映射方法有效。
>
>例如，`personComponents`数组的每个对象在标准摄取模式期间单独提交，然后由Experience Platform添加到数组。 手动将对象数组添加到业务人员组件将返回错误。
>为B2B数据创建架构时，应使用自动生成实用程序。 有关如何使用[B2B命名空间和架构自动生成实用程序](../../../sources/connectors/adobe-applications/marketo/marketo-namespaces.md)的说明，请参阅文档。 如果您未使用自动生成实用程序，并且打算手动映射数据模型，请确保在映射数据之前阅读有关[Adobe Real-Time Customer Data Platform B2B edition XDM类](../../../rtcdp/schemas/b2b.md)的文档。
>
>有关B2B数据的推荐工作流程的信息，请参阅[端到端教程](../../../rtcdp/b2b-tutorial.md)。

![](../../images/field-groups/business-person-components.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `sourceAccountKey` | [[!UICONTROL B2B Source]](../../data-types/b2b-source.md) | 与人员关联的帐户的复合标识符。 |
| `sourceConvertedContactKey` | [[!UICONTROL B2B Source]](../../data-types/b2b-source.md) | 如果此商机已转化，则为相关联系人的复合标识符。 |
| `sourceExternalKey` | [[!UICONTROL B2B Source]](../../data-types/b2b-source.md) | 人员数据源自的源系统的复合标识符。 |
| `sourcePersonKey` | [[!UICONTROL B2B Source]](../../data-types/b2b-source.md) | 人员的复合标识符。 |
| `workEmail` | [[!UICONTROL Email address]](../../data-types/b2b-source.md) | 人员的工作电子邮件ID。 |
| `personGroupID` | 字符串 | 人员的组标识符。 |
| `personScore` | 字符串 | CRM系统为人员生成的分数。 |
| `personSource` | 字符串 | 人员数据源自的源系统的基于字符串的唯一标识符。 |
| `personStatus` | 字符串 | 人员的当前营销或销售状态。 |
| `personType` | 字符串 | B2B上下文中的人员类型。 |
| `sourceAccountID` | 字符串 | 源系统中与人员关联的帐户的唯一基于字符串的标识符。 此字段被系统用作外键，以查找此人供职的不同公司。 |
| `sourceConvertedContactID` | 字符串 | 如果此商机已转化，则为相关联系人提供的基于字符串的唯一标识符。 |
| `sourceExternalID` | 字符串 | 人员数据源自的源系统的基于字符串的唯一标识符。 |
| `sourcePersonID` | 字符串 | 人员的基于字符串的唯一标识符。 |

{style="table-layout:auto"}

有关字段组的更多详细信息，请参阅公共XDM存储库：

* [填充示例](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/b2b-person-components.example.1.json)
* [完整架构](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/b2b-person-components.schema.json)
