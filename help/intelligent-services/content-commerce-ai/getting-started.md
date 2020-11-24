---
keywords: Experience Platform;getting started;content ai;commerce ai;content and commerce ai
solution: Experience Platform
title: 内容和商务AI快速入门
topic: Getting started
description: 内容和商务AI利用AdobeI/O API。 要调用AdobeI/O API和I/O控制台集成，您必须先完成身份验证教程。
translation-type: tm+mt
source-git-commit: 2be04547b96e1a6c293cc63e782fe1b3259619ba
workflow-type: tm+mt
source-wordcount: '576'
ht-degree: 0%

---


# 内容和商务AI快速入门

>[!NOTE]
>
>Content and Commerce AI为测试版。 文档可能会更改。

[!DNL Content and Commerce AI] 利用AdobeI/O API。 要调用AdobeI/O API和I/O控制台集成，您必须先完成身份验证 [教程](../../tutorials/authentication.md)。

但是，当您转到“添 **加API** ”步骤时，API位于Experience Cloud而不是Adobe Experience Platform下，如以下屏幕截图所示：

![添加内容和商务AI](./images/add-api.png)

完成身份验证教程后，将为所有AdobeI/O API调用中的每个所需标头提供值，如下所示：

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {IMS_ORG}`

## 创建邮递员环境（可选）

在Adobe开发人员控制台中设置项目和API后，您可以选择下载邮递员的环境文件。 在 **[!UICONTROL API]** （项目的左边栏）下，选择 **[!UICONTROL “内容和商务AI”]**。 此时将打开一个新选项卡，其中包含一个标有“”[!DNL Try it out]的卡。 选 **择“下载邮递员** ”以下载用于配置邮递员环境的JSON文件。

![下载postman](./images/add-to-postman.png)

下载文件后，打开Postman并选择右 **上方** 的齿轮图标以打开“管 **理环境** ”对话框。

![齿轮图标](./images/select-gear-icon.png)

然后，从“管 **理环境** ”对话框 **中选择“导入** ”。

![导入](./images/import.png)

系统会重定向您并要求您从计算机中选择环境文件。 选择您之前下载的JSON文件，然后选择 **打开** 以加载环境。

![](./images/choose-your-file.png)

![](./images/click-open.png)

您将被重定向回“管 *理环境* ”选项卡，并填充新环境名称。 选择要视图的环境名称，并编辑Postman中可用的变量。 您仍需要手动填充 `JWT_TOKEN` 和 `ACCESS_TOKEN`。 完成身份验证教程时应已获 [取这些值](../../tutorials/authentication.md)。

![](./images/re-direct.png)

完成后，您的变量应类似于下面的屏幕截图。 选择 **更新** ，以完成设置环境。

![](./images/final-environment.png)

您现在可以从右上角的下拉菜单中选择您的环境，并自动填充保存的任何值。 随时重新编辑这些值即可更新您的所有API调用。

![示例](./images/select-environment.png)

有关使用邮递员使用AdobeI/O API的详细信息，请参阅在AdobeI/O上使 [用邮递员进行JWT身份验证的中级帖子](https://medium.com/adobetech/using-postman-for-jwt-authentication-on-adobe-i-o-7573428ffe7f)。

## 读取示例API调用

本指南提供示例API调用，以演示如何格式化请求。 这包括路径、必需的标头和格式正确的请求负载。 还提供API响应中返回的示例JSON。 有关示例API调用文档中使用的惯例的信息，请参阅Experience Platform疑 [难解答指南中有关如何阅读示例API调](../../landing/troubleshooting.md) 用的章节。

## 后续步骤 {#next-steps}

获得所有凭据后，即可为设置自定义工作器 [!DNL Content and Commerce AI]。 以下文档有助于理解可扩展性框架和环境设置。

要进一步了解可扩展性框架，请阅读可扩展性 [文档简介进行开始](https://docs.adobe.com/content/help/en/asset-compute/using/extend/understand-extensibility.html) 。 本文档概述了先决条件和配置要求。

要进一步了解如何设置环境, [!DNL Content and Commerce AI]请阅读开发人员开始 [设置指南来进行环境](https://docs.adobe.com/content/help/en/asset-compute/using/extend/setup-environment.html)。 此文档提供允许您为Asset compute服务进行开发的设置说明。