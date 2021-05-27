---
keywords: Experience Platform；主页；热门主题；架构；架构；XDM；单个配置文件；字段；架构；架构；标识映射；标识映射；架构设计；映射；并集架构；并集架构
solution: Experience Platform
title: XDM个人配置文件类
topic-legacy: overview
description: 本文档概述了XDM Individual Profile类。
exl-id: 83b22462-79ce-4024-aa50-a9bd800c0f81
source-git-commit: 39d04cf482e862569277211d465bb2060a49224a
workflow-type: tm+mt
source-wordcount: '455'
ht-degree: 1%

---

# [!DNL XDM Individual Profile] class

[!DNL XDM Individual Profile] 是一个标准的体验数据模型(XDM)类，它构成个人的单个表示形式（或“用户档案”）。具体而言，类（及其兼容的mixin）可捕获已识别和部分已识别与您的品牌进行交互的个人的属性和兴趣。

配置文件可以包含匿名行为信号（如浏览器Cookie）和高度识别的配置文件，其中包含详细信息（如名称、出生日期、位置和电子邮件地址）。 随着用户档案的增长，它将成为个人的个人信息、身份、联系方式和通信首选项的可靠存储库。 有关在平台生态系统中使用此类的更多高级信息，请参阅[XDM概述](../home.md#data-behaviors)。

[!DNL XDM Individual Profile]类本身提供了几个系统生成的值，这些值在摄取数据时自动填充，而所有其他字段必须通过使用[兼容的架构字段组](#field-groups)来添加：

![](../images/classes/individual-profile.png)

| 属性 | 描述 |
| --- | --- |
| `_repo` | 包含以下[!UICONTROL DateTime]字段的对象： <ul><li>`createDate`:在数据存储中创建资源的日期和时间，例如首次摄取数据时。</li><li>`modifyDate`:上次修改资源的日期和时间。</li></ul> |
| `_id` | 记录的唯一标识符。 此字段用于跟踪单个记录的唯一性，防止重复数据，并在下游服务中查找该记录。<br><br>必须明确的是，此字段不 **会** 显示与个人相关的身份，而是显示数据本身的记录。与人员相关的身份数据应被降级到[标识字段](../schema/composition.md#identity)。 |
| `createdByBatchID` | 导致创建记录的摄取批次的ID。 |
| `modifiedByBatchID` | 导致记录更新的上次摄取的批处理的ID。 |
| `personID` | 与此记录相关的个人的唯一标识符。 除非该字段也被指定为[identity字段](../schema/composition.md#identity)，否则该字段不一定表示与人员相关的身份。 |
| `repositoryCreatedBy` | 创建记录的用户的ID。 |
| `repositoryLastModifiedBy` | 上次修改记录的用户ID。 |

{style=&quot;table-layout:auto&quot;}

## 兼容的字段组{#field-groups}

>[!NOTE]
>
>多个字段组的名称已更改。 有关详细信息，请参阅[字段组名称更新](../field-groups/name-updates.md)上的文档。

Adobe提供了多个用于[!DNL XDM Individual Profile]类的标准字段组。 以下是类的一些常用字段组的列表：

* [[!UICONTROL IdentityMap]](../field-groups/profile/identitymap.md)
* [[!UICONTROL 人口统计详细信息]](../field-groups/profile/demographic-details.md)
* [[!UICONTROL 个人联系详细信息]](../field-groups/profile/personal-contact-details.md)
* [[!UICONTROL 工作联系人详细信息]](../field-groups/profile/work-contact-details.md)
* [[!UICONTROL 区段成员资格详细信息]](../field-groups/profile/segmentation.md)

有关[!DNL XDM Individual Profile]的所有兼容字段组的完整列表，请参阅[XDM GitHub存储库](https://github.com/adobe/xdm/tree/master/components/mixins/profile)。
