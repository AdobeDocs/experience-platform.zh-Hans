---
title: Adobe Experience Platform 发行说明
description: Adobe Experience Platform 2023年10月版发行说明。
source-git-commit: d024596c7d85139721ef370f9e081911a217d9ba
workflow-type: tm+mt
source-wordcount: '178'
ht-degree: 43%

---

# Adobe Experience Platform 发行说明

**发行日期：2023 年 10 月 25 日**

 Experience Platform 中现有功能的更新：

- [源](#sources)

## 源 {#sources}

Experience Platform 提供 RESTful API 和交互式 UI，可让您轻松为各种数据提供者设置源连接。这些源连接允许您验证并连接到外部存储系统和 CRM 服务、设置运行摄取操作的时间以及管理数据摄取吞吐量。

**新增功能或更新后的功能**

| 功能 | 描述 |
| --- | --- |
| 更新了数据登陆区的身份验证 | 现在，您可以在查看凭据时看到数据登陆区域的指定到期日期。 您必须在到期日期之前刷新令牌才能继续在应用程序中使用它。 如果您未在规定的到期日期之前手动刷新令牌，则它将在您下次检索凭据时自动刷新并提供新令牌。 有关详细信息，请阅读以下文档： [使用数据登陆区](../../sources/tutorials/ui/create/cloud-storage/data-landing-zone.md). |

{style="table-layout:auto"}

要了解有关来源的更多信息，请阅读 [源概述](../../sources/home.md).
