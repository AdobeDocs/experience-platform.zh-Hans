---
title: Web SDK安装概述
description: 了解如何安装Experience Platform Web SDK。
keywords: web sdk安装；安装web sdk；internet explorer；promise；npm包
exl-id: b1de7ca1-d0d2-4661-a273-a1acf29afcd5
source-git-commit: a490c429047f5e5997d69f30a51e6b78debe2d5d
workflow-type: tm+mt
source-wordcount: '229'
ht-degree: 0%

---

# Web SDK安装概述

有三种受支持的方法可以使用Adobe Experience Platform Web SDK：

1. **[Web SDK标记扩展](/help/tags/extensions/client/web-sdk/overview.md)**： Adobe建议使用此方法。 在网站上安装标记加载器，然后使用Adobe Experience Platform数据收集UI配置实施。
1. **[Web SDK JavaScript库](library.md)**：引用CDN托管的库文件，或使用您自己的基础架构托管库文件。 调用网站上代码中的库。
1. **[NPM](npm.md)**：使用NPM包管理器在您的站点上安装Web SDK。

## 先决条件

在使用或安装Web SDK之前，您必须满足以下要求：

* 必须首先配置Adobe Experience Platform中的架构。 这些设置包括任何必要的架构、身份和数据流。
* 您必须配置正确的权限才能访问相应的工具。 例如，如果贵组织决定使用标记扩展，则您必须拥有访问数据收集UI的正确权限。 有关详细信息，请参阅[数据收集权限](../../permissions.md)。
* 建议使用第一方域(CNAME)。 如果您已经拥有Adobe Analytics的CNAME，则可以使用该名称。 开发中的测试不需要使用CNAME，但Adobe建议在发布到生产环境之前使用一个CNAME。 有关详细信息，请参阅[第一方设备ID](../../use-cases/identity/first-party-device-ids.md)。
