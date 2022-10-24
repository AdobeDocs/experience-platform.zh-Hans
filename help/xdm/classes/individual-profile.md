---
keywords: Experience Platform；主页；热门主题；架构；架构；XDM；单个配置文件；字段；架构；架构；标识映射；标识映射；架构设计；映射；并集架构；并集架构
solution: Experience Platform
title: XDM个人配置文件类
topic-legacy: overview
description: 本文档概述了XDM Individual Profile类。
exl-id: 83b22462-79ce-4024-aa50-a9bd800c0f81
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '598'
ht-degree: 1%

---

# [!DNL XDM Individual Profile] class

[!DNL XDM Individual Profile] 是一个标准的体验数据模型(XDM)类，它构成个人的单个表示形式（或“用户档案”）。 具体而言，类（及其兼容的字段组）可捕获已识别和部分已识别与您的品牌进行交互的个人的属性和兴趣。

用户档案可以包含匿名行为信号（如浏览器Cookie）和高度识别的用户档案，这些用户档案包含详细信息（如名称、出生日期、位置和电子邮件地址）。 随着用户档案的增长，它将成为个人的个人信息、身份、联系方式和通信首选项的可靠存储库。 有关在平台生态系统中使用此类的更多高级信息，请参阅 [XDM概述](../home.md#data-behaviors).

的 [!DNL XDM Individual Profile] 类本身提供了几个系统生成的值，这些值在摄取数据时会自动填充，而所有其他字段都必须通过使用 [兼容架构字段组](#field-groups):

![](../images/classes/individual-profile.png)

| 属性 | 描述 |
| --- | --- |
| `_repo` | 包含以下项的对象 [!UICONTROL DateTime] 字段： <ul><li>`createDate`:在数据存储中创建资源的日期和时间，例如首次摄取数据时。</li><li>`modifyDate`:上次修改资源的日期和时间。</li></ul> |
| `_id` | 记录的唯一字符串标识符。 此字段用于跟踪单个记录的唯一性，防止重复数据，并在下游服务中查找该记录。 在某些情况下， `_id` 可以 [通用唯一标识符(UUID)](https://tools.ietf.org/html/rfc4122) 或 [全局唯一标识符(GUID)](https://docs.microsoft.com/en-us/dotnet/api/system.guid?view=net-5.0).<br><br>如果从源连接流式传输数据或直接从Parquet文件摄取数据，则应通过关联使记录具有唯一性的特定字段组合（如主ID、时间戳、记录类型等）来生成此值。 拼接值必须是 `uri-reference` 格式化的字符串，这意味着必须删除任何冒号字符。 之后，连接值应使用SHA-256或您选择的其他算法进行哈希处理。<br><br>要区分这一点很重要 **此字段不表示与个人相关的身份**，而是数据本身的记录。 与个人有关的身份数据应降级为 [身份字段](../schema/composition.md#identity) 由兼容的字段组提供。 |
| `createdByBatchID` | 导致创建记录的摄取批次的ID。 |
| `modifiedByBatchID` | 导致记录更新的上次摄取的批处理的ID。 |
| `personID` | 与此记录相关的个人的唯一标识符。 此字段不一定表示与人员相关的身份，除非它还被指定为 [标识字段](../schema/composition.md#identity). |
| `repositoryCreatedBy` | 创建记录的用户的ID。 |
| `repositoryLastModifiedBy` | 上次修改记录的用户ID。 |

{style=&quot;table-layout:auto&quot;}

## 兼容的字段组 {#field-groups}

>[!NOTE]
>
>多个字段组的名称已更改。 请参阅 [字段组名称更新](../field-groups/name-updates.md) 以了解更多信息。

Adobe提供了多个与 [!DNL XDM Individual Profile] 类。 以下是类的一些常用字段组的列表：

* [[!UICONTROL 同意和首选项]](../field-groups/profile/consents.md)
* [[!UICONTROL 人口统计详细信息]](../field-groups/profile/demographic-details.md)
* [[!UICONTROL IdentityMap]](../field-groups/profile/identitymap.md)
* [[!UICONTROL 忠诚度详细信息]](../field-groups/profile/loyalty-details.md)
* [[!UICONTROL 个人联系详细信息]](../field-groups/profile/personal-contact-details.md)
* [[!UICONTROL 区段成员资格详细信息]](../field-groups/profile/segmentation.md)
* [[!UICONTROL 电信订购]](../field-groups/profile/telecom-subscription.md)
* [[!UICONTROL 工作联系人详细信息]](../field-groups/profile/work-contact-details.md)
* [[!UICONTROL XDM业务人员组件]](../field-groups/profile/business-person-components.md)\*
* [[!UICONTROL XDM业务人员详细信息]](../field-groups/profile/business-person-details.md)\*

*\*此字段组仅适用于有权访问B2B版Adobe Real-time Customer Data Platform的组织。*

有关的所有兼容字段组的完整列表 [!DNL XDM Individual Profile]，请参阅 [XDM GitHub存储库](https://github.com/adobe/xdm/tree/master/components/fieldgroups/profile).
