---
keywords: Experience Platform；快速入门；内容人工智能；商业人工智能；内容标记
solution: Experience Platform
title: 内容标记快速入门
description: 内容标记利用Adobe I/OAPI。 要调用Adobe I/OAPI和I/O控制台集成，您必须先完成身份验证教程。
exl-id: e7b0e9bb-a1f1-479c-9e9b-46991f2942e2
source-git-commit: a98639851e7245b9cbd6fe42b35b4730dd19c3f8
workflow-type: tm+mt
source-wordcount: '567'
ht-degree: 0%

---

# 内容标记快速入门

[!DNL Content tagging] 利用Adobe I/OAPI。 要调用Adobe I/OAPI和I/O控制台集成，您必须先完成 [身份验证教程](https://www.adobe.com/go/platform-api-authentication-en).

但是，当您转到 **添加API** 步骤，该API位于Experience Cloud下而非Adobe Experience Platform下，如以下屏幕快照所示：

![添加内容标记](./images/add-api-updated.png)

完成身份验证教程将为所有Adobe I/OAPI调用中的每个所需标头提供值，如下所示：

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {ORG_ID}`

## 创建Postman环境（可选）

在Adobe Developer控制台中设置项目和API后，您可以选择下载Postman的环境文件。 下 **[!UICONTROL API]** 在项目的左边栏中，选择 **[!UICONTROL 内容标记]**. 此时将打开一个新选项卡，其中包含标有“[!DNL Try it out]“。 选择 **Postman下载** 下载用于配置Postman环境的JSON文件。

![postman下载](./images/add-to-postman-updated.png)

下载文件后，打开Postman并选择 **齿轮图标** 打开右上方的 **管理环境** 对话框。

![齿轮图标](./images/select-gear-icon.png)

接下来，选择 **导入** 从 **管理环境** 对话框。

![导入](./images/import-updated.png)

系统将重定向您并提示您从计算机中选择环境文件。 选择您之前下载的JSON文件，然后选择 **打开** 以加载环境。

![](./images/choose-your-file.png)

![](./images/click-open.png)

您将被重定向回 *管理环境* 选项卡中填充了新环境名称。 选择环境名称以查看和编辑Postman中可用的变量。 您仍需要手动填充 `JWT_TOKEN` 和 `ACCESS_TOKEN`. 这些值应在完成 [身份验证教程](https://www.adobe.com/go/platform-api-authentication-en).

![](./images/re-direct-updated.png)

完成后，您的变量应当类似于下面的屏幕快照。 选择 **更新** 以完成环境设置。

![](./images/final-environment-updated.png)

您现在可以从右上角的下拉菜单中选择环境，并自动填充保存的任何值。 您只需随时重新编辑这些值，即可更新所有API调用。

![示例](./images/select-environment-updated.png)

有关使用Postman使用Adobe I/OAPI的更多信息，请参阅上的媒体帖子 [在Adobe I/O上使用Postman进行JWT身份验证](https://medium.com/adobetech/using-postman-for-jwt-authentication-on-adobe-i-o-7573428ffe7f).

## 正在读取示例API调用

本指南提供了示例API调用，以演示如何设置请求的格式。 这些资源包括路径、必需的标头和格式正确的请求负载。 此外，还提供了在API响应中返回的示例JSON。 有关示例API调用文档中使用的约定的信息，请参阅以下章节： [如何读取示例API调用](../../landing/troubleshooting.md) 在Experience Platform疑难解答指南中。

## 后续步骤 {#next-steps}

获得所有凭据后，便可以为其设置自定义工作程序 [!DNL Content tagging]. 以下文档有助于了解可扩展性框架和环境设置。

要了解有关可扩展性框架的更多信息，请从阅读 [可扩展性简介](https://experienceleague.adobe.com/docs/asset-compute/using/extend/understand-extensibility.html) 文档。 本文档概述了先决条件和预配要求。

详细了解如何为以下对象设置环境： [!DNL Content tagging]，首先请阅读 [设置开发人员环境](https://experienceleague.adobe.com/docs/asset-compute/using/extend/setup-environment.html). 本文档提供了允许您为Asset compute服务开发的设置说明。
