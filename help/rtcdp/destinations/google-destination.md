---
title: Google目标
seo-title: Google目标
description: Adobe实时CDP与Google集成，使您能跨DV360、Google Ad Manager、Google AdWords和Google AdX执行和激活数据。
seo-description: Adobe实时CDP与Google集成，使您能跨DV360、Google Ad Manager、Google AdWords和Google AdX执行和激活数据。
translation-type: tm+mt
source-git-commit: 5396bee00044e5046bd768a863fceca0aec1d24e

---


# Google目标

## 概述

Adobe实时CDP与Google集成，使您能跨DV360、Google Ad Manager、Google AdWords Display和Google AdX执行和激活数据。

## 目标规范

请注意Google目标的以下详细信息：

* 您可以将以下身份 [发送到](https://www.adobe.io/apis/experienceplatform/home/profile-identity-segmentation/profile-identity-segmentation-services.html#!api-specification/markdown/narrative/technical_overview/identity_namespace_overview/identity_namespace_overview.md) Google目标：Google **Cookie ID、IDFA、GAID**。
* 激活的受众是在Google平台中以编程方式创建的。
* Adobe实时CDP当前不包含用于验证成功激活的度量标准。 请参阅Google中的受众计数，以验证集成并了解数据中断。

## 先决条件

### 白名单

在Adobe实时CDP中连接Google目标之前，您必须联系Google，要求将您的帐户列入白名单。 联系Google并提供以下信息：

* **帐户ID** :这是Adobe在Google上的帐户ID。 联系Adobe支持以获取此ID。
* **客户ID** :这是Adobe在Google上的客户帐户ID。 联系Adobe支持以获取此ID。
* **合作伙伴ID** :这是你和谷歌的三位数合作伙伴ID;
* **网络ID** :这是你在谷歌的账户；
* **受众链接ID** :这是你在谷歌的账户；
* 您的帐户类型。 这可以是邀请 **者**、 **邀请合作伙伴**、 **DFP**、 ******** AdWords、AdX广告词。


## 连接目标

1. 在“ **[!UICONTROL 连接”>“目标]**”中，选择“Google”，然后选择“ **[!UICONTROL 创建目标”]**。
   ![Connect Google目标](/help/rtcdp/destinations/assets/google-destination.png)

2. 在连接目标向导中，填写目标的基本信息。
   ![基本信息Google](/help/rtcdp/destinations/assets/google-basic-information.png)
* **名称**:填写此目标的首选名称。
* **说明**:可选。 例如，您可以提及要为此目标使用哪个营销活动。
* **帐户类型**:根据您在Google上的帐户，选择一个选项：
   * 用 `Invite advertiser` 于Google DV360
   * 用 `Invite partner` 于Google DV360
   * 用 `DFP by Google` 于Google广告管理器
   * 用 `AdWords` 于Google AdWords显示
   * 用 `AdX buyer` 于Google AdX
* **帐户ID**:使用Google填写您的帐户ID。

>[!NOTE]
>
>设置Google目标时，请与Google客户经理或Adobe代表联系，了解您的帐户属于哪种产品类型。 对于Google DV360，请询问您的Google客户经理您的帐户属于哪种产品类型。 

## 将区段激活到Google

有关如何将区段激活到Google的说明，请参阅将数 [据激活到目标](/help/rtcdp/destinations/activate-destinations.md)。