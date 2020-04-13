---
title: Facebook目标
seo-title: Facebook目标
description: 激活Facebook活动的用户档案，根据散列电子邮件进行受众定位、个性化和抑制。
seo-description: 激活Facebook活动的用户档案，根据散列电子邮件进行受众定位、个性化和抑制。
translation-type: tm+mt
source-git-commit: bfcbc56f05fa1c3b5fafd57b1166e50130b6007d

---


# （测试版）Facebook目标

>[!IMPORTANT]
>
>Adobe Real-time CDP中的Facebook目标当前处于测试版中，并且并非所有用户都可使用。 文档和功能可能会发生变化。

## 概述

激活Facebook活动的用户档案，根据散列电子邮件进行受众定位、个性化和抑制。

## 目标规范

### 激活类型

区段导出——您导出的是区段(受众)的所有成员及其标识符（名称、电话号码等）在Facebook目标中使用

## 先决条件

在将受众区段发送到之前， [!DNL Facebook]请确保满足以下要求：

1. 您 [!DNL Facebook] 的用户帐户必须为您 **计划使用的广告帐户启用“管理活动** ”权限。
2. 将 **Adobe Experience Cloud商业帐户添加为广告合作伙伴**[!DNL Facebook Ad Account]。 使用 `business ID=206617933627973`. 有关详 [细信息，请参阅将合作伙伴添加到您的业务经理](https://www.facebook.com/business/help/1717412048538897) 。
   >[!IMPORTANT]
   > 配置Adobe Experience Cloud的权限时，必须启用“管理 **活动** ”权限。 这是集成所必需的 [!DNL Adobe Real-time CDP] 选项。
3. 阅读并签署 [!DNL Facebook Custom Audiences] 服务条款。 为此，请转到 `https://business.facebook.com/ads/manage/customaudiences/tos/?act=[accountID]`您的 `accountID` 位置 [!DNL Facebook Ad Account ID]。


## 连接目标

要连接Facebook目标，请参阅社交网络 [目标身份验证工作流](/help/rtcdp/destinations/social-network-destinations-workflow.md)。


## 将区段激活到Facebook

有关如何将区段激活到Facebook的说明，请参阅将数 [据激活到目标](/help/rtcdp/destinations/activate-destinations.md)。