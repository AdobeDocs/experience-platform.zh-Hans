---
keywords: Experience Platform；主页；热门主题；模式;模式;XDM；个人用户档案；字段；模式;模式；标识映射；标识映射；模式设计；映射；映射；合并模式;合并
solution: Experience Platform
title: XDM个人用户档案类
topic-legacy: overview
description: 本文档概述了XDM单个用户档案类。
exl-id: 83b22462-79ce-4024-aa50-a9bd800c0f81
source-git-commit: 9fbb40a401250496761dcce63a3f033a8746ae7e
workflow-type: tm+mt
source-wordcount: '452'
ht-degree: 0%

---

# [!DNL XDM Individual Profile] class

[!DNL XDM Individual Profile] 是一个标准的体验数据模型(XDM)类，它构成了个人的单一表示形式(或“用户档案”)。具体而言，该类（及其兼容的混合）捕获与您的品牌进行互动的已识别和部分识别的个人的属性和兴趣。

用户档案可以包括匿名行为信号（如浏览器cookie）和包含详细信息（如姓名、出生日期、位置和电子邮件地址）的高度识别的用户档案。 随着用户档案的增长，它将成为个人个人信息、身份、联系信息和通信首选项的可靠存储库。 有关在平台生态系统中使用此类的详细信息，请参阅[ XDM概述](../home.md#data-behaviors)。

[!DNL XDM Individual Profile]类本身提供了几个系统生成的值，这些值在摄取数据时自动填充，而所有其他字段必须通过使用[兼容的模式字段组](#field-groups)添加：

![](../images/classes/individual-profile.png)

| 属性 | 描述 |
| --- | --- |
| `_repo` | 包含以下[!UICONTROL DateTime]字段的对象： <ul><li>`createDate`:在数据存储中创建资源的日期和时间，例如首次摄取数据的时间。</li><li>`modifyDate`:上次修改资源的日期和时间。</li></ul> |
| `_id` | 记录的唯一标识符。 此字段用于跟踪单个记录的唯一性、防止重复数据并在下游服务中查找该记录。<br><br>必须指出的是，这一 **领域** 不代表与个人有关的身份，而是数据本身的记录。应将与个人有关的身份数据归入[身份字段](../schema/composition.md#identity)。 |
| `createdByBatchID` | 导致创建记录的所摄取批的ID。 |
| `modifiedByBatchID` | 导致记录更新的上次收录批的ID。 |
| `personID` | 与此记录相关的个人的唯一标识符。 除非此字段也指定为[标识字段](../schema/composition.md#identity)，否则此字段不一定表示与该人相关的身份。 |
| `repositoryCreatedBy` | 创建记录的用户的ID。 |
| `repositoryLastModifiedBy` | 上次修改记录的用户的ID。 |

## 兼容字段组{#field-groups}

>[!NOTE]
>
>多个字段组的名称已更改。 有关详细信息，请参阅[字段组名称更新](../field-groups/name-updates.md)上的文档。

Adobe提供多个标准字段组，以用于[!DNL XDM Individual Profile]类。 以下是某类一些常用字段组的列表:

* [[!UICONTROL IdentityMap]](../field-groups/profile/identitymap.md)
* [[!UICONTROL 人口统计详细信息]](../field-groups/profile/demographic-details.md)
* [[!UICONTROL 个人联系人详细信息]](../field-groups/profile/personal-contact-details.md)
* [[!UICONTROL 工作联系人详细信息]](../field-groups/profile/work-contact-details.md)
* [[!UICONTROL 区段会员资格详细信息]](../field-groups/profile/segmentation.md)

有关[!DNL XDM Individual Profile]的所有兼容字段组的完整列表，请参阅[ XDM GitHub存储库](https://github.com/adobe/xdm/tree/master/components/mixins/profile)。
