---
keywords: Experience Platform；快速入门；内容人工智能；商务人工智能；内容和商务人工智能
solution: Intelligent Services
title: 内容和商务AI快速入门
topic-legacy: Getting started
description: 内容和商务AI利用Adobe I/OAPI。 要调用Adobe I/OAPI和I/O控制台集成，您必须先完成身份验证教程。
exl-id: e7b0e9bb-a1f1-479c-9e9b-46991f2942e2
source-git-commit: 16120a10f8a6e3fd7d2143e9f52a822c59a4c935
workflow-type: tm+mt
source-wordcount: '592'
ht-degree: 0%

---

# 内容和商务AI快速入门

>[!NOTE]
>
>Content and Commerce AI是测试版。 文档可能会发生更改。

[!DNL Content and Commerce AI] 利用Adobe I/OAPI。 要调用Adobe I/OAPI和I/O控制台集成，您必须先完成 [身份验证教程](https://www.adobe.com/go/platform-api-authentication-en).

但是，当您 **添加API** 步骤中，API位于Experience Cloud下，而不是Adobe Experience Platform下，如以下屏幕截图所示：

![添加内容和商务AI](./images/add-api.png)

完成身份验证教程可为所有Adobe I/OAPI调用中每个所需标头的值，如下所示：

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {IMS_ORG}`

## 创建Postman环境（可选）

在Adobe开发人员控制台中设置项目和API后，您可以选择下载适用于Postman的环境文件。 在 **[!UICONTROL API]** 在项目的左边栏中，选择 **[!UICONTROL 内容和商务人工智能]**. 此时会打开一个新选项卡，其中包含一个标有“[!DNL Try it out]&quot; 选择 **适用于Postman的下载** 下载用于配置Postman环境的JSON文件。

![下载postman](./images/add-to-postman.png)

下载文件后，打开Postman并选择 **齿轮图标** 在右上方打开 **管理环境** 对话框。

![齿轮图标](./images/select-gear-icon.png)

接下来，选择 **导入** 从 **管理环境** 对话框。

![导入](./images/import.png)

系统会重定向您，并要求您从计算机中选择环境文件。 选择之前下载的JSON文件，然后选择 **打开** 来加载环境。

![](./images/choose-your-file.png)

![](./images/click-open.png)

系统会将您重定向回 *管理环境* 选项卡，并填充新的环境名称。 选择环境名称以查看和编辑Postman中可用的变量。 您仍需要手动填充 `JWT_TOKEN` 和 `ACCESS_TOKEN`. 在完成 [身份验证教程](https://www.adobe.com/go/platform-api-authentication-en).

![](./images/re-direct.png)

完成后，您的变量应类似于下面的屏幕截图。 选择 **更新** 完成环境设置。

![](./images/final-environment.png)

现在，您可以从右上角的下拉菜单中选择您的环境，并自动填充保存的任何值。 只需随时重新编辑值，以更新所有API调用。

![示例](./images/select-environment.png)

有关使用Postman使用Adobe I/OAPI的更多信息，请参阅 [在Adobe I/O上使用Postman进行JWT身份验证](https://medium.com/adobetech/using-postman-for-jwt-authentication-on-adobe-i-o-7573428ffe7f).

## 读取示例API调用

本指南提供了示例API调用，以演示如何设置请求的格式。 这包括路径、所需标头以及格式正确的请求负载。 还提供了API响应中返回的示例JSON。 有关示例API调用文档中使用的约定的信息，请参阅 [如何阅读示例API调用](../../landing/troubleshooting.md) (位于Experience Platform疑难解答指南中)。

## 后续步骤 {#next-steps}

拥有所有凭据后，您便可以为 [!DNL Content and Commerce AI]. 以下文档有助于了解扩展性框架和环境设置。

要进一步了解扩展性框架，请首先阅读 [扩展性简介](https://experienceleague.adobe.com/docs/asset-compute/using/extend/understand-extensibility.html) 文档。 本文档概述了先决条件和配置要求。

了解有关为 [!DNL Content and Commerce AI]，请首先阅读 [设置开发人员环境](https://experienceleague.adobe.com/docs/asset-compute/using/extend/setup-environment.html). 本文档提供了允许您为Asset compute服务开发的设置说明。
