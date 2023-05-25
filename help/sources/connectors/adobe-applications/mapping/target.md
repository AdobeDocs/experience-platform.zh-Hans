---
keywords: Experience Platform；主页；热门主题；目标映射；目标映射
solution: Experience Platform
title: 将Adobe Target事件数据映射到XDM
description: 了解如何将Adobe Target事件字段映射到体验数据模型(XDM)架构，以便在Adobe Experience Platform中使用。
exl-id: dab08ab6-6c1c-460a-bb52-8dcdb5709a34
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '479'
ht-degree: 0%

---

# 目标映射字段映射

Adobe Experience Platform允许您通过Target源连接器摄取Adobe Target数据。 使用连接器时，必须将Target字段中的所有数据映射到 [体验数据模型(XDM)](../../../../xdm/home.md) 与XDM ExperienceEvent类关联的字段。

下表概述了体验事件架构(*XDM ExperienceEvent字段*)以及它们应映射到的相应Target字段(*Target请求字段*)。 此外，还针对某些映射提供了其他说明。

>[!NOTE]
>
>请向左/向右滚动以查看表格的全部内容。

| XDM ExperienceEvent字段 | Target请求字段 | 注释 |
| ------------------------- | -------------------- | ----- |
| **`id`** | 唯一请求标识符 |
| **`dataSource`** |  | 已为所有客户端配置为“1”。 |
| `dataSource._id` | 系统生成的值，无法随请求一起传递。 | 此数据源的唯一ID。 这将由创建数据源的个人或系统提供。 |
| `dataSource.code` | 系统生成的值，无法随请求一起传递。 | 全@id的快捷方式。 可以使用代码或@id中的至少一个。 有时，此代码称为数据源集成代码。 |
| `dataSource.tags` | 系统生成的值，无法随请求一起传递。 | 标记用于指示应用程序应如何解释由给定数据源表示的别名。<br><br>示例：<br><ul><li>`isAVID`：表示Analytics访客ID的数据源。</li><li>`isCRSKey`：表示应在CRS中用作键的别名的数据源。</li></ul>标记在创建数据源时设置，但在引用给定数据源时也包含在管道消息中。 |
| **`timestamp`** | 事件时间戳 |
| **`channel`** | `context.channel` | 仅适用于视图投放。 选项为“Web”和“mobile”，默认选项为“Web”。 |
| **`endUserIds`** |
| `endUserIds.experience.tntId` | `tntId/mboxPC` |
| `endUserIds.experience.mcId` | `marketingCloudVisitorId` | Experience CloudID (ECID)也称为MCID，它将继续用在命名空间中。 |
| **`environment`** |
| `environment.browserDetails.userAgent` | `mboxRequest.userAgent` |
| `environment.browserDetails.viewPortHeight` | `mboxRequest.browserHeight` |
| `environment.browserDetails.viewPortWidth` | `mboxRequest.browserWidth` |
| `environment.operatingSystem` | `deviceAtlas.osName` |
| `environment.operatingSystemVersion` | `deviceAtlas.osVersion` |
| `environment.viewportHeight` | `mboxRequest.screenHeight` |
| `environment.viewportWidth` | `mboxRequest.screenWidth` |
| `environment.colorDepth` | `mboxRequest.colorDepth` |
| `environment.carrier` | 根据请求的IP地址解析的移动运营商名称。 |
| `environment.ipV4` | `mboxRequest.ipAddress` （如果采用V4格式） |
| `environment.ipV6` | `mboxRequest.ipAddress` （如果采用V6格式） |
| **`experience`** |
| `experience.target.clientCode` | `mboxRequest.client` |
| `experience.target.mboxName` | `mboxRequest.mboxName` |
| `experience.target.mboxVersion` | `mboxRequest.mboxVersion` |
| `experience.target.sessionId` | `mboxRequest.sessionId` |
| `experience.target.environmentID` | Target为客户定义的环境（如开发、qa或生产）提供的内部映射。 |
| `experience.target.supplementalDataID` | 用于将Target事件与Analytics事件拼合的标识符 |
| `experience.target.pageDetails.pageId` | `mboxRequest.pageId` |
| `experience.target.pageDetails.pageScore` | `mboxRequest.mboxPageValue` |
| `experience.target.activities` | 访客符合条件的活动列表（数组） |
| `experience.target.activities[i].activityID` | 访客符合条件的任何给定活动的ID |
| `experience.target.activities[i].version` | 访客符合条件的任何给定活动的版本 |
| `experience.target.activities[i].activityEvents` | 包含用户通过此事件点击的活动事件的详细信息。 |
| **`device`** |
| `device.typeIDService` | `XDMDevice.Device.TypeIDService.typeIDService_deviceatlas` |
| `device.type` | 的以下属性之一 `deviceAtlas` （或NULL）： <ul><li>`type_mobile`</li><li>`type_tablet`</li><li>`type_desktop`</li><li>`type_ereader`</li><li>`type_television`</li><li>`type_settop`</li><li>`type_mediaplayer`</li></ul> |
| `device.typeID` | （空字符串） |
| `device.manufacturer` | `deviceAtlas.manufacturer` |
| `device.model` | `deviceAtlas.model` |
| `device.modelNumber` | （空字符串） |
| `device.screenHeight` | `deviceAtlas.displayHeight` |
| `device.screenWidth` | `deviceAtlas.displayWidth` |
| `device.colorDepth` | `deviceAtlas.displayColorDepth` |
| **`placeContext`** |
| `placeContext.geo.id` | 随机UUID（必需） |
| `placeContext.geo.city` | 根据请求的IP地址解析的城市名称。 |
| `placeContext.geo.countryCode` | 根据请求的IP地址解析的国家代码。 |
| `placeContext.geo.dmaId` | 已根据请求的IP地址解析指定的市场区号。 |
| `placeContext.geo.postalCode` | 根据请求的IP地址解析邮政编码。 |
| `placeContext.geo.stateProvince` | 已根据请求的IP地址解析的州或省。 |
| `placeContext.localTime` | `mboxRequest.offsetTime` + `mboxRequest.currentServerTime` |
| **`commerce`** |  | 仅当请求中存在订单详细信息时设置。 |
| `commerce.order.priceTotal` | `mboxRequest.orderTotal` |
| `commerce.order.purchaseOrderNumber` | `mboxRequest.orderId` |
| `commerce.order.purchaseID` | `mboxRequest.orderId` |
| **`web`** |
| `web.withWebPageDetails.url` | `mboxURL.context.address.url` |
| `web.webReferrer.url` | `mboxReferrer.context.address.url` |
| **`identityMap`** |
| `identityMap.TNTID` | `tntId.mboxPC` |
| `identityMap.ECID` | `marketingCloudVisitorId` |

{style="table-layout:auto"}
