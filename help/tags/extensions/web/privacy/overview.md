---
title: Adobe隐私扩展概述
description: 了解Adobe Experience Platform中的Adobe隐私标记扩展。
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '534'
ht-degree: 75%

---

# Adobe隐私扩展概述

>[!NOTE]
>
>Adobe Experience Platform Launch已在Adobe Experience Platform中重新命名为一套数据收集技术。 因此，在产品文档中推出了一些术语更改。 有关术语更改的统一参考，请参阅以下[文档](../../../term-updates.md)。

Adobe Privacy 扩展提供了用于收集和移除由 Adobe 解决方案分配给最终用户的用户 ID 的功能。

## 在安装期间配置解决方案

从扩展目录安装 Adobe Privacy 扩展时，系统会提示您选择要更新的解决方案。目前，您可以更新以下解决方案：

* Analytics (AA)
* Audience Manager (AAM)
* Target
* 访客服务
* AdCloud
* 选择一个或多个解决方案，然后选择“Update”。
* 选择并配置解决方案后，选择“Save”。Adobe Privacy 扩展将会添加到已安装的扩展列表中。

   每个解决方案的选项如下所述。

### Analytics

![](../../../images/ext-privacy-aa.jpg)

默认情况下，您必须通过输入字符串或选择数据元素来提供报表包。

要配置其他项目，请选择&#x200B;**[!UICONTROL 选择项目]**，选择要配置的项目，然后选择&#x200B;**[!UICONTROL 添加]**&#x200B;并输入请求的参数或数据元素。

### Audience Manager

![](../../../images/ext-privacy-aam.jpg)

选择&#x200B;**[!UICONTROL 选择项目]**，选择要配置的项目，然后选择&#x200B;**[!UICONTROL 添加]**&#x200B;并输入请求的参数或数据元素。 目前，您只能配置 `aamUUIDCookieName`。

### Target

![](../../../images/ext-privacy-target.jpg)

输入 Target 客户端代码。

### 访客服务

![](../../../images/ext-privacy-visitor.jpg)

输入您的 IMS 组织 ID。

### AdCloud

![](../../../images/ext-privacy-adcloud.jpg)

没有要为 AdCloud 配置的特定参数。

## 配置 Adobe Privacy 扩展

安装该扩展后，您可以禁用或删除它。在已安装扩展的Adobe隐私卡上选择&#x200B;**[!UICONTROL 配置]**，然后选择&#x200B;**[!UICONTROL 禁用]**&#x200B;或&#x200B;**[!UICONTROL 卸载]**。

## 操作

使用 Adobe Privacy 扩展配置规则时，可以使用以下操作。

### Retrieve Identities

满足事件和条件后，检索为访客存储的身份信息。

输入要将数据传递到的 JavaScript 函数的名称。此函数或方法将处理检索到的身份信息。是存储、显示身份信息，还是将这些信息发送到 Adobe GDPR API，这将由您掌控。

### Remove Identities

满足事件和条件后，移除为访客存储的身份信息。

输入要将数据传递到的 JavaScript 函数的名称。此函数或方法将处理检索到的身份信息。是存储、显示身份信息，还是将这些信息发送到 Adobe GDPR API，这将由您掌控。

### Retrieve Then Remove Identies

满足事件和条件后，检索为访客存储的身份信息，然后移除该信息。

## 教程：配置 Privacy 扩展

下面显示了一个展示如何设置数据元素并将其用于 Privacy 扩展的简短示例。

1. 创建一个名为 `privacyFunc` 的数据元素。

   ```JavaScript
   window.privacyFunc = function(a,b){
       console.log(a,b);
   }
   return window.privacyFunc
   ```

1. 创建一个规则以在库加载（页面顶部）时运行，并通过 Adobe Privacy 扩展执行操作。选择 `privacyFunc` 作为数据元素。

   * **扩展：** Adobe Privacy
   * **操作类型：**检索标识
此操作类型显示已创建、删除或未删除的标识。
   * **名称：**&#x200B;检索标识

1. 更新开发库，然后发布并进行测试。
