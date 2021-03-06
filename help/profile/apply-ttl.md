---
keywords: Experience Platform；主页；热门主题；数据集；数据集；生存时间；ttl；生存时间；
solution: Experience Platform
title: 数据集的实时性
description: 本文档为Adobe Experience Platform的配置文件存储中的数据集提供了有关生存时间(TTL)的常规指导。
source-git-commit: 878c04c688268f8cf1850c3e8d40f958a6d2d69b
workflow-type: tm+mt
source-wordcount: '459'
ht-degree: 0%

---


# 配置文件服务生存时间(TTL)

用户可以通过配置文件服务对配置文件存储中的数据应用生存时间(TTL)。 TTL是一种机制，用于限制数据在数据集内存留的时间。 这样，您就可以自动从配置文件存储区中删除对您的用例不再有用的数据。

当前，配置文件仅支持体验事件TTL。

## 体验事件TTL

体验事件TTL允许您对启用了“实时客户配置文件”的数据集应用TTL，以从配置文件存储中删除不再有效的数据。

>[!NOTE]
>
>要在数据集上启用体验事件TTL，您需要联系支持人员。

在启用了配置文件的数据集上启用Experience Event TTL后，Platform将通过两步流程自动将TTL过期值应用于体验事件数据：

1. 摄取到数据集的所有新数据都将在摄取时应用TTL过期值。
2. 数据集中的所有现有数据都将具有TTL过期值，该值将作为一次性回填系统作业进行逆向应用。 在数据集上放置TTL过期值后，运行系统作业后，将立即删除早于TTL过期值的事件。 所有其他事件一旦从事件时间戳达到其TTL过期值，就会立即被删除。

>[!NOTE]
>
>应用TTL后，任何早于TTL天数的数据都将被永久删除&#x200B;**，并且无法恢复。**
> 
>此外，请确保区段的回顾窗口位于TTL边界内。 否则，应用TTL后，区段结果可能会不正确。 例如，如果您应用的TTL为30天，并且有一个区段尝试查看最多45天前的数据，则该区段会生成错误的“配置文件”。
> 
>因此，您应尽可能保留所有数据集的相同TTL，以避免分段逻辑中不同数据集中不同TTL值的影响。

例如，如果您在5月15日应用了30天的TTL值，则会执行以下步骤：

1. 所有新事件在摄取时的TTL值都将为30天。
2. 所有时间戳早于4月15日的现有事件，都将随系统作业立即删除。
3. 所有时间戳晚于4月15日的现有事件在其事件时间戳后30天将具有TTL过期值。 因此，如果某个事件的时间戳为4月18日，则该事件将在该时间戳的日期（即5月18日）后三十天被删除。

