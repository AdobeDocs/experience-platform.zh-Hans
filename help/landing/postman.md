---
keywords: Experience Platform；主页；热门主题；Adobe Experience Platform;api指南；平台api指南；平台简介；开发人员指南
solution: Experience Platform
title: Adobe Experience Platform邮递员
topic: api指南
description: 此文档包含概述如何设置邮递环境、导入邮递员集合以及每个平台服务可用集合列表的步骤。
translation-type: tm+mt
source-git-commit: effc8fef666ffbf62c2e0874d048245f19c12111
workflow-type: tm+mt
source-wordcount: '552'
ht-degree: 0%

---


# Adobe Experience Platform邮递员

Postman是一个用于API开发的协作平台，它允许您使用预设变量设置环境、共享API集合、简化CRUD请求等。 大多数平台API服务都有Postman集合，可用于协助进行API调用。

## 如何设置邮递员环境进行Experience Platform

以下视频指南概述了如何创建和设置您的邮递环境。 邮递员环境包含您对以下提供的各种集合进行API调用所需的所有标头。 设置后，任何值过期（如`ACCESS_TOKEN`）时，您都可以更新环境中的当前值，此新值将用于所有集合。

>[!VIDEO](https://video.tv.adobe.com/v/28832)

## 邮递员集合{#collections}

可通过访问[Experience Platform邮递员示例GitHub存储库](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/experience-platform)找到包含所有可用邮递员集合的文件夹。 或者，在Adobe I/O的[API参考文档](http://www.adobe.com/go/platform-api-reference-en)中，可以在每个Swagger文件中找到Postman集合链接。

要下载Postman集合，请从GitHub页面中选择&#x200B;**[!DNL Raw]**&#x200B;以在新选项卡中加载原始JSON文件。 然后，右键单击并选择&#x200B;**[!DNL Save as]**&#x200B;将文件保存到您选择的本地目标。

![原始JSON](./images/api-guide/raw-collection.PNG)

## 导入Postman集合{#import}

要使用[邮递员集合](#collections)，您需要设置环境。 完成环境设置后，选择右上角的&#x200B;**[!DNL Manage Environments]**&#x200B;选择器。

![管理环境选择器](./images/api-guide/environment-selector.png)

将出现一个快显窗口，并显示您当前的所有环境。 要导入集合，请选择&#x200B;**[!DNL import]**。

![导入按钮](./images/api-guide/import-collection.png)

系统会要求您选择要导入的文件。 选择要导入的Postman集合文件。 选择后，集合将填充到左边栏的“集合”选项卡下。

![已填充集合](./images/api-guide/imported-collection.png)

每个集合具有不同的键值对，执行成功的CRUD操作可能需要这些键值对。 请查看服务的[API开发人员指南](api-guide.md#api-guides)，了解所需的值、提示和查看示例。

要进一步了解邮递员UI及其可用功能，请访问[邮递员文档](https://learning.postman.com/docs/getting-started/navigating-postman/)。

### 使用Postman生成访问令牌以供非生产用途

>[!WARNING]
>
>如Adobe I/O访问令牌生成Postman集合中所述，表示的生成方法适用于&#x200B;**非生产用途**。 本地签名从第三方主机加载JavaScript库，远程签名将私钥发送到由Adobe拥有和操作的Web服务。 虽然Adobe不存储此私钥，但生产密钥绝不应与任何人共享。

以下视频使用[Adobe I/O访问令牌生成集合](https://github.com/adobe/experience-platform-postman-samples/blob/master/apis/ims/Adobe%20IO%20Access%20Token%20Generation.postman_collection.json)，可从公共GitHub存储库下载。

>[!VIDEO](https://video.tv.adobe.com/v/29698/?quality=12&learn=on)

## 后续步骤

此文档介绍了Postman环境、集合以及如何导入集合。 现在，您已准备好Postman，请访问[平台入门指南](api-guide.md)，了解所需的标头、示例以及每个平台服务都可用的[API指南](api-guide.md#api-guides)列表。