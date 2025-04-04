---
keywords: Experience Platform；主页；热门主题；架构；架构；XDM；个人配置文件；字段；架构；架构；身份映射；身份映射；架构设计；映射；映射；合并架构；合并
solution: Experience Platform
title: XDM个人配置文件类
description: 了解XDM Individual Profile类。
exl-id: 83b22462-79ce-4024-aa50-a9bd800c0f81
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '553'
ht-degree: 0%

---

# [!DNL XDM Individual Profile]类

[!DNL XDM Individual Profile]是一个标准体验数据模型(XDM)类，它构成个人的单一呈现（或“个人资料”）。 具体而言，类（及其兼容的字段组）捕获与您的品牌互动的已识别和部分识别的个人的属性和兴趣。

用户档案的范围可以从匿名行为信号（如浏览器Cookie），到包含姓名、出生日期、位置和电子邮件地址等详细信息的高度识别用户档案。 随着个人资料的增长，它将成为包含个人信息、身份、联系人详细信息和个人通信偏好设置的强大存储库。 有关在Experience Platform生态系统中使用此类的更多高级信息，请参阅[XDM概述](../home.md#data-behaviors)。

![XDM个人配置文件类的架构图。](../images/classes/individual-profile.png)

| 属性 | 描述 |
| --- | --- |
| `_repo` | 包含以下[!UICONTROL 日期时间]字段的对象： <ul><li>`createDate`：在数据存储中创建资源的日期和时间，如首次摄取数据的时间。</li><li>`modifyDate`：上次修改资源的日期和时间。</li></ul> |
| `_id` | 记录的唯一字符串标识符。 此字段用于跟踪单个记录的唯一性，防止数据重复，并在下游服务中查找该记录。 在某些情况下，`_id`可以是[通用唯一标识符(UUID)](https://tools.ietf.org/html/rfc4122)或[全局唯一标识符(GUID)](https://docs.microsoft.com/en-us/dotnet/api/system.guid?view=net-5.0)。<br><br>如果从源连接流式传输数据或直接从Parquet文件中摄取，则应当通过连接使记录唯一的字段组合（如主ID、时间戳、记录类型等）来生成此值。 连接值必须为`uri-reference`格式字符串，这意味着必须删除任何冒号字符。 之后，应该使用SHA-256或您选择的其他算法对拼接值进行哈希处理。<br><br>请务必注意，**此字段不表示与个人**&#x200B;相关的身份，而是数据本身的记录。 与人员相关的身份数据应委托给兼容字段组提供的[身份字段](../schema/composition.md#identity)。 |
| `createdByBatchID` | 导致创建记录的摄取批次的ID。 |
| `modifiedByBatchID` | 导致更新记录的上次摄取批次的ID。 |
| `personID` | 与此记录相关的个人的唯一标识符。 此字段不一定表示与人员相关的身份，除非也指定为[身份字段](../schema/composition.md#identity)。 |
| `repositoryCreatedBy` | 创建记录的用户的ID。 |
| `repositoryLastModifiedBy` | 上次修改记录的用户的ID。 |

{style="table-layout:auto"}

## 兼容的字段组 {#field-groups}

>[!NOTE]
>
>多个字段组的名称已更改。 有关详细信息，请参阅有关[字段组名称更新](../field-groups/name-updates.md)的文档。

Adobe提供了多个标准字段组以用于[!DNL XDM Individual Profile]类。 以下是类的一些常用字段组的列表：

* [[!UICONTROL 同意和偏好设置]](../field-groups/profile/consents.md)
* [[!UICONTROL 人口统计详细信息]](../field-groups/profile/demographic-details.md)
* [[!UICONTROL IdentityMap]](../field-groups/profile/identitymap.md)
* [[!UICONTROL 忠诚度详细信息]](../field-groups/profile/loyalty-details.md)
* [[!UICONTROL 个人联系人详细信息]](../field-groups/profile/personal-contact-details.md)
* [[!UICONTROL 区段成员资格详细信息]](../field-groups/profile/segmentation.md)
* [[!UICONTROL 电信订阅]](../field-groups/profile/telecom-subscription.md)
* [[!UICONTROL 工作联系人详细信息]](../field-groups/profile/work-contact-details.md)
* [[!UICONTROL XDM业务人员组件]](../field-groups/profile/business-person-components.md)\*
* [[!UICONTROL XDM业务人员详细信息]](../field-groups/profile/business-person-details.md)\*

*\*此字段组仅适用于有权访问Adobe Real-Time Customer Data PlatformB2B edition的组织。*

有关[!DNL XDM Individual Profile]的所有兼容字段组的完整列表，请参阅[XDM GitHub存储库](https://github.com/adobe/xdm/tree/master/components/fieldgroups/profile)。
