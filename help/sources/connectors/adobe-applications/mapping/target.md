---
keywords: Experience Platform;home;popular topics;target mapping;Target mapping
solution: Experience Platform
title: 目标映射字段
topic: overview
description: 下表概述了体验事件模式的字段（*XDM ExperienceEvent字段*），以及应将其映射到的相应目标字段(目标请求字段)。 还提供了一些映射的附加说明。
translation-type: tm+mt
source-git-commit: 6934bfeee84f542558894bbd4ba5759891cd17f3
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 0%

---


# 目标映射字段

Adobe Experience Platform允许您通过目标源连接器获取Adobe Target数据。 使用连接器时，目标字段中的所有数据都必须映射 [到与XDM ExperienceEvent类关联](../../../../xdm/home.md) 的体验数据模型(XDM)字段。

下表概述了体验事件模式(*XDM ExperienceEvent字段*)的字段，以及应将其映射到的相应目标字段(*目标请求字段*)。 还提供了一些映射的附加说明。

>[!NOTE]
>
>请向左／向右滚动以视图表的完整内容。

| XDM ExperienceEvent字段 | 目标请求字段 | 注释 |
| ------------------------- | -------------------- | ----- |
| **`id`** | 唯一请求标识符 |
| **`dataSource`** |  | 已配置为“1”，适用于所有客户端。 |
| `dataSource._id` | 无法随请求一起传入的系统生成的值。 | 此数据源的唯一ID。 这将由创建数据源的个人或系统提供。 |
| `dataSource.code` | 无法随请求一起传入的系统生成的值。 | 完整@id的快捷方式。 可以使用代码或@id中的至少一个。 有时，此代码称为数据源集成代码。 |
| `dataSource.tags` | 无法随请求一起传入的系统生成的值。 | 标记用于指示由给定数据源表示的别名如何由使用这些别名的应用程序进行解释。<br><br>示例：<br><ul><li>`isAVID`:表示分析访客ID的数据源。</li><li>`isCRSKey`:表示应用作CRS中键的别名的数据源。</li></ul>创建数据源时设置标记，但引用给定数据源时，这些标记也包含在管道消息中。 |
| **`timestamp`** | 事件时间戳 |
| **`channel`** | `context.channel` | 只适用于视图投放。 选项为“web”和“mobile”，默认为“web”。 |
| **`endUserIds`** |
| `endUserIds.experience.tntId` | `tntId/mboxPC` |
| `endUserIds.experience.mcId` | `marketingCloudVisitorId` |
| **`environment`** |
| `environment.browserDetails.userAgent` | `mboxRequest.userAgent` |
| `environment.browserDetails.viewPortHeight` | `mboxRequest.browserHeight` |
| `environment.browserDetails.viewPortWidth` | `mboxRequest.browserWidth` |
| `environment.operatingSystem` | `deviceAtlas.osName` |
| `environment.operatingSystemVersion` | `deviceAtlas.osVersion` |
| `environment.viewportHeight` | `mboxRequest.screenHeight` |
| `environment.viewportWidth` | `mboxRequest.screenWidth` |
| `environment.colorDepth` | `mboxRequest.colorDepth` |
| `environment.carrier` | 根据请求的IP地址解析移动运营商名称。 |
| `environment.ipV4` | `mboxRequest.ipAddress` （如果采用V4格式） |
| `environment.ipV6` | `mboxRequest.ipAddress` （如果采用V6格式） |
| **`experience`** |
| `experience.target.clientCode` | `mboxRequest.client` |
| `experience.target.mboxName` | `mboxRequest.mboxName` |
| `experience.target.mboxVersion` | `mboxRequest.mboxVersion` |
| `experience.target.sessionId` | `mboxRequest.sessionId` |
| `experience.target.environmentID` | 目标为客户定义的环境（如dev、qa或prod）进行的内部映射。 |
| `experience.target.supplementalDataID` | 用于将目标事件与Analytics事件拼接的标识符 |
| `experience.target.pageDetails.pageId` | `mboxRequest.pageId` |
| `experience.target.pageDetails.pageScore` | `mboxRequest.mboxPageValue` |
| `experience.target.activities` | 列表符合访客资格的活动（阵列） |
| `experience.target.activities[i].activityID` | 符合条件的活动的任何给定访客的ID |
| `experience.target.activities[i].version` | 符合条件的任何给定活动的版本 |
| `experience.target.activities[i].activityEvents` | 包括用户用此活动点击的事件的详细信息。 |
| **`device`** |
| `device.typeIDService` | `XDMDevice.Device.TypeIDService.typeIDService_deviceatlas` |
| `device.type` | 以下属性之一( `deviceAtlas` 或NULL): <ul><li>`type_mobile`</li><li>`type_tablet`</li><li>`type_desktop`</li><li>`type_ereader`</li><li>`type_television`</li><li>`type_settop`</li><li>`type_mediaplayer`</li></ul> |
| `device.typeID` | （空字符串） |
| `device.manufacturer` | `deviceAtlas.manufacturer` |
| `device.model` | `deviceAtlas.model` |
| `device.modelNumber` | （空字符串） |
| `device.screenHeight` | `deviceAtlas.displayHeight` |
| `device.screenWidth` | `deviceAtlas.displayWidth` |
| `device.colorDepth` | `deviceAtlas.displayColorDepth` |
| **`placeContext`** |
| `placeContext.geo.id` | 随机UUID（必填） |
| `placeContext.geo.city` | 根据请求的IP地址解析城市名称。 |
| `placeContext.geo.countryCode` | 根据请求的IP地址解析国家／地区代码。 |
| `placeContext.geo.dmaId` | 根据请求的IP地址解析的指定市场区域代码。 |
| `placeContext.geo.postalCode` | 根据请求的IP地址解析的邮政编码。 |
| `placeContext.geo.stateProvince` | 根据请求的IP地址解析的州或省。 |
| `placeContext.localTime` | `mboxRequest.offsetTime` + `mboxRequest.currentServerTime` |
| **`commerce`** |  | 仅在请求中存在订单详细信息时进行设置。 |
| `commerce.order.priceTotal` | `mboxRequest.orderTotal` |
| `commerce.order.purchaseOrderNumber` | `mboxRequest.orderId` |
| `commerce.order.purchaseID` | `mboxRequest.orderId` |
| **`web`** |
| `web.withWebPageDetails.url` | `mboxURL.context.address.url` |
| `web.webReferrer.url` | `mboxReferrer.context.address.url` |
| **`identityMap`** |
| `identityMap.TNTID` | `tntId.mboxPC` |
| `identityMap.ECID` | `marketingCloudVisitorId` |
