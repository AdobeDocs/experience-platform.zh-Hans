---
keywords: Experience Platform；入门；内容ai；商务ai；内容和商务ai
solution: Experience Platform, Intelligent Services
title: 内容和商务AI快速入门
topic: Getting started
description: 内容和商务AI利用Adobe I/OAPI。 要调用Adobe I/OAPI和I/O控制台集成，您必须先完成身份验证教程。
translation-type: tm+mt
source-git-commit: ece2ae1eea8426813a95c18096c1b428acfd1a71
workflow-type: tm+mt
source-wordcount: '596'
ht-degree: 0%

---


# 内容和商务AI快速入门

>[!NOTE]
>
>Content and Commerce AI为测试版。 文档可能会更改。

[!DNL Content and Commerce AI] 利用Adobe I/OAPI。要调用Adobe I/OAPI和I/O控制台集成，您必须先完成[身份验证教程](https://www.adobe.com/go/platform-api-authentication-en)。

但是，当您进入&#x200B;**添加API**&#x200B;步骤时，API位于Experience Cloud而不是Adobe Experience Platform下，如以下屏幕截图所示：

![添加内容和商务AI](./images/add-api.png)

完成身份验证教程后，将为所有Adobe I/OAPI调用中的每个所需标头提供值，如下所示：

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {IMS_ORG}`

## 创建邮递员环境（可选）

在Adobe开发人员控制台中设置项目和API后，您可以选择下载邮递员的环境文件。 在项目左边栏&#x200B;**[!UICONTROL API]**&#x200B;下，选择&#x200B;**[!UICONTROL 内容和商务AI]**。 此时将打开一个新选项卡，其中包含一个标有“[!DNL Try it out]”的卡。 选择&#x200B;**Download for Postman**&#x200B;以下载用于配置邮递员环境的JSON文件。

![下载postman](./images/add-to-postman.png)

下载文件后，打开Postman并选择右上方的&#x200B;**齿轮图标**&#x200B;以打开&#x200B;**管理环境**&#x200B;对话框。

![齿轮图标](./images/select-gear-icon.png)

接下来，从&#x200B;**管理环境**&#x200B;对话框中选择&#x200B;**导入**。

![导入](./images/import.png)

系统会重定向您并要求您从计算机中选择环境文件。 选择您之前下载的JSON文件，然后选择&#x200B;**打开**&#x200B;以加载环境。

![](./images/choose-your-file.png)

![](./images/click-open.png)

您将被重定向回&#x200B;*管理环境*&#x200B;选项卡，并填充新环境名称。 选择要视图的环境名称，并编辑Postman中可用的变量。 您仍需要手动填充`JWT_TOKEN`和`ACCESS_TOKEN`。 完成[身份验证教程](https://www.adobe.com/go/platform-api-authentication-en)时应已获取这些值。

![](./images/re-direct.png)

完成后，您的变量应类似于下面的屏幕截图。 选择&#x200B;**更新**&#x200B;以完成环境设置。

![](./images/final-environment.png)

您现在可以从右上角的下拉菜单中选择您的环境，并自动填充保存的任何值。 随时重新编辑这些值即可更新您的所有API调用。

![示例](./images/select-environment.png)

有关使用Postman使用Adobe I/OAPI的详细信息，请参见[上的“使用Postman进行Adobe I/OJWT验证的中”帖子](https://medium.com/adobetech/using-postman-for-jwt-authentication-on-adobe-i-o-7573428ffe7f)。

## 读取示例API调用

本指南提供示例API调用，以演示如何格式化请求。 这包括路径、必需的标头和格式正确的请求负载。 还提供API响应中返回的示例JSON。 有关示例API调用文档中使用的约定的信息，请参阅Experience Platform疑难解答指南中的[如何阅读示例API调用](../../landing/troubleshooting.md)一节。

## 后续步骤 {#next-steps}

获得所有凭据后，即可为[!DNL Content and Commerce AI]设置自定义工作器。 以下文档有助于理解可扩展性框架和环境设置。

要进一步了解可扩展性框架，请阅读可扩展性](https://docs.adobe.com/content/help/en/asset-compute/using/extend/understand-extensibility.html)开始文档的简介。 [本文档概述了先决条件和配置要求。

要进一步了解如何设置[!DNL Content and Commerce AI]的环境，请阅读[设置开发者环境的指南](https://docs.adobe.com/content/help/en/asset-compute/using/extend/setup-environment.html)进行开始。 此文档提供允许您为Asset compute服务进行开发的设置说明。