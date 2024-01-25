---
title: Identity Service和实时客户资料
description: 了解Identity Service与Real-Time Customer Profile之间的关系
exl-id: 09961b8e-f736-4fcc-ac53-88b55cca7d55
source-git-commit: 45170c78b9d15c7cc9d71f2d0dab606ea988a783
workflow-type: tm+mt
source-wordcount: '658'
ht-degree: 1%

---

# 了解Identity Service与Real-time Customer Profile之间的关系

>[!IMPORTANT]
>
> 本页假定合并策略正在使用身份图。 有关实时客户配置文件中合并策略的更多信息，请阅读上的文档 [合并策略和身份拼接](../profile/merge-policies/overview.md#identity-stitching).

虽然您可以将Identity Service和Real-time Customer Profile结合使用，但Adobe Experience Platform的两个功能本身并不相同。

* 您可以使用Identity Service生成和维护标识图，以将各个客户的不同标识整合在一起。
* 您可以使用Real-time Customer Profile将不同的配置文件片段整合在一起，并创建合并的配置文件。 此过程需要使用身份图。

本文档概述了Identity Service与Real-time Customer Profile之间的异同、区别和关系。

## Identity Service与实时客户资料

Identity Service和Real-time Customer Profile之间的主要区别如下：

| | 身份服务 | 实时客户配置文件 |
| --- | --- |--- |
| **用途** | <ul><li>可以使用Identity Service创建和管理身份图。</li></ul> | 您可以使用实时客户档案执行以下操作： <ul><li>创建客户配置文件的360度视图。</li><li>查看和管理用户档案</li><li>细分用户档案以创建受众。</li></ul> |
| **输入** | <ul><li>要使用Identity Service，您必须摄取至少有两个标记为标识的字段的记录数据或时间序列事件。 然后，您标记为身份的字段会被引入到Identity Service中。</li></ul> | **要合并配置文件，您必须提供**： <ul><li>配置文件片段：表示给定数据集中该ID的唯一主标识以及相应的记录或事件数据。</li><li>身份图：配置文件引用给定客户配置文件的身份图，以识别具有相同主身份的所有配置文件片段。</li></ul> **对于区段鉴别，您必须提供**： <ul><li>合并的用户档案：合并的用户档案是客户的单一视图，其中不同的配置文件片段和身份收集到一个全面的视图中。</li></ul> |
| **进程** | <ul><li>在摄取至少两个身份后，Identity Service会将这些身份链接在一起。</li></ul> | <ul><li>Real-time Customer Profile在引用其相应的身份图时合并配置文件片段。</li><li>根据分段标准确定用户档案的区段资格条件</li></ul> |
| **输出** | <ul><li>结果是一个标识图，它是一组与个人相关的标识。</li></ul> | <ul><li>结果是一个合并的配置文件，它是对给定客户的单一而全面的视图。</li><li>定义了区段成员资格的用户档案</li></ul> |

{style="table-layout:auto"}

>[!BEGINSHADEBOX]

## 如何创建合并的用户档案？

请阅读以下步骤，以更好地了解创建合并用户档案的过程：

* 首先，Real-time Customer Profile引用身份图并检索所有身份。
* 接下来，配置文件检索与每个身份相关的所有配置文件片段。
* 成功后， Profile than会合并所有现有事件和属性。
   * 如果需要，应用优先规则以确定要使用的属性或事件

![详细介绍Identity服务和配置文件合并工作方式的流程图。](./images/identity-settings/identity-and-profile.png)

>[!ENDSHADEBOX]

### 将字段标记为标识意味着什么？

将字段标记为标识或指定该字段是Experience Platform将该特定字段摄取到Identity服务的指令。 然后，这种指定允许在Real-time Customer Profile中合并配置文件片段。 如果没有与身份关联的配置文件片段，则不要将其指定为身份。

#### 了解主要标识和次要标识

将字段标记为标识后，可以将其定义为主标识或辅助标识。 主要和次要身份是Real-time Customer Profile中的概念。

* 主标识（有时称为“主键”）是其中存储配置文件片段的标识。
* 如果给定数据行中只有一个身份，则该单一身份将被指定为主身份。
* 如果有两个或多个标识，则将其中一个标识指定为主标识，其余标识指定为辅助标识。

Identity Service仅摄取指定为标识的字段。 Identity Service不存储有关某个标识是主标识还是辅助标识的信息。
