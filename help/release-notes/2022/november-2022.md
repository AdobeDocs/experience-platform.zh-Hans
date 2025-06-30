---
title: Adobe Experience Platform 发行说明（2022 年 11 月）
description: Adobe Experience Platform 2022 年 11 月发行说明。
exl-id: 1048cfae-6e7a-4d05-a004-c5c095a17fc4
source-git-commit: 2e41a1716e057cd33e4635c11ba9c3cfc185418a
workflow-type: tm+mt
source-wordcount: '312'
ht-degree: 62%

---

# Adobe Experience Platform 发行说明

**发行日期： 2022年11月23日**

Adobe Experience Platform 中现有功能的更新：

- [数据收集](#data-collection)
- [Experience Data Model (XDM)](#xdm)
- [源](#sources)

## 数据收集 {#data-collection}

Adobe Experience Platform 提供一套技术，通过这些技术，可收集客户端客户体验数据，并将它发送到 Adobe Experience Platform Edge Network，从中可充实、转换数据和将数据分发到 Adobe 或非 Adobe 目标。

**新增功能或更新后的功能**

| 功能 | 描述 |
| --- | --- |
| 用于事件转发的[!DNL AWS]扩展 | 您现在可以使用[事件转发](../../tags/ui/event-forwarding/overview.md)扩展将数据发送到[!DNL Amazon Web Services] ([!DNL AWS])。 有关更多信息，请参阅[[!DNL AWS] 扩展概述](../../tags/extensions/server/aws/overview.md)。 |
| 用于事件转发的[!DNL Google Ads Enhanced Conversions]扩展 | 您现在可以使用[事件转发](../../tags/ui/event-forwarding/overview.md)扩展将转化数据发送到[!DNL Google Ads]。 有关更多信息，请参阅[[!DNL Google Ads Enhanced Conversions] 扩展概述](../../tags/extensions/server/google-ads-enhanced-conversions/overview.md)。 |
| 用于事件转发的[!DNL Microsoft Azure]扩展 | 您现在可以使用[事件转发](../../tags/ui/event-forwarding/overview.md)扩展将数据发送到[!DNL Microsoft Azure]。 有关更多信息，请参阅[[!DNL Microsoft Azure] 扩展概述](../../tags/extensions/server/azure/overview.md)。 |

有关Experience Platform数据收集功能的详细信息，请参阅[数据收集概述](../../collection/home.md)。

## Experience Data Model (XDM) {#xdm}

XDM 是一种开源规范，可为导入 Adobe Experience Platform 的数据提供通用结构和定义（架构）。通过遵守 XDM 标准，所有客户体验数据都可以合并到一个通用的呈现中，以更快、更加集成的方式提供见解。您可以从客户行为中获得有价值的见解，通过区段定义客户受众，并使用客户属性实现个性化目的。

**新增功能或更新后的功能**

| 功能 | 描述 |
| --- | --- |
| 直接添加到架构时向自定义类分配字段 | 在[将单个字段直接添加到架构](../../xdm/ui/resources/schemas.md#add-individual-fields)时，以前只能将该字段作为其父级资源分配给字段组。 现在，除了字段组之外，您还可以[将该字段分配给自定义类](../../xdm/ui/resources/schemas.md#add-to-class)作为其父资源。 |

{style="table-layout:auto"}

有关 Experience Platform 中 XDM 的详细信息，请查看 [XDM 系统概述](../../xdm/home.md)。
