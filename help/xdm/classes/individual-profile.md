---
keywords: Experience Platform；主题；热门主题；模式;模式;XDM；个人用户档案；字段；模式;模式；标识映射；标识映射；标识映射；模式设计；映射；映射；合并模式;合并
solution: Experience Platform
title: XDM个人用户档案类
topic: overview
description: 此文档概述了XDM单个用户档案类。
translation-type: tm+mt
source-git-commit: f2238d35f3e2a279fbe8ef8b581282102039e932
workflow-type: tm+mt
source-wordcount: '388'
ht-degree: 0%

---


# [!DNL XDM Individual Profile] class

[!DNL XDM Individual Profile] 是标准XDM类，它构成了已识别和部分已识别个体的属性和兴趣的单一表示(或“用户档案”)。

用户档案可以包括匿名行为信号（如浏览器cookie）和高度识别的用户档案，这些包含详细信息，如姓名、出生日期、地点和电子邮件地址。 随着用户档案的增长，它将成为一个可靠的存储库，其中存储着个人信息、身份、联系信息和个人通信偏好。 有关在平台生态系统中使用此类的详细信息，请参阅[XDM概述](../home.md#data-behaviors)。

[!DNL XDM Individual Profile]类本身提供几个系统生成的值，这些值在摄取数据时自动填充，而所有其他字段必须通过使用[兼容的mixins](#mixins)来添加：

![](../images/classes/individual-profile.png)

| 属性 | 描述 |
| --- | --- |
| `_repo` | 包含以下[!UICONTROL DateTime]字段的对象： <ul><li>`createDate`:在数据存储中创建资源的日期和时间，如首次摄取数据时。</li><li>`modifyDate`:上次修改资源的日期和时间。</li></ul> |
| `_id` | 记录的唯一、由系统生成的字符串标识符。 此字段用于跟踪单个记录的唯一性、防止重复数据并在下游服务中查找该记录。 由于此字段是系统生成的，因此在数据获取过程中不应为其提供显式值。<br><br>必须区分的是，该 **领域** 不代表与个人有关的身份，而是记录数据本身。与人有关的身份数据应降级到[身份字段](../schema/composition.md#identity)。 |
| `createdByBatchID` | 导致创建记录的所摄取批的ID。 |
| `modifiedByBatchID` | 导致记录更新的上一个摄取的批次的ID。 |
| `repositoryCreatedBy` | 创建记录的用户的ID。 |
| `repositoryLastModifiedBy` | 上次修改记录的用户的ID。 |

## 兼容混音{#mixins}

>[!NOTE]
>
>几个混音的名称已经更改。 有关详细信息，请参阅[mixin name updates](../mixins/name-updates.md)上的文档。

Adobe提供多个标准混音以用于[!DNL XDM Individual Profile]类。 以下是该类最常用混音的列表:

* [[!UICONTROL IdentityMap]](../mixins/profile/identitymap.md)
* [[!UICONTROL 人口统计详细信息]](../mixins/profile/person-details.md)
* [[!UICONTROL 个人联系人详细信息]](../mixins/profile/personal-details.md)
* [[!UICONTROL 工作联系人详细信息]](../mixins/profile/work-details.md)
* [[!UICONTROL 细分会员资格详细信息]](../mixins/profile/segmentation.md)