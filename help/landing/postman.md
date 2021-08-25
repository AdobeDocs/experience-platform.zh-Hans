---
keywords: Experience Platform；主页；热门主题；Adobe Experience Platform;API指南；平台API指南；平台简介；开发人员指南
solution: Experience Platform
title: 邮递员在Adobe Experience Platform
topic-legacy: api guide
description: 本文档包含概述如何设置Postman环境、导入Postman收藏集以及每个Platform服务的可用收藏集列表的步骤。
exl-id: a09b3875-97f5-47f1-a562-52decbce67b1
source-git-commit: a0f4e49192a54075ce7c48620c9729e61ecdfdac
workflow-type: tm+mt
source-wordcount: '550'
ht-degree: 0%

---

# 邮递员在Adobe Experience Platform

Postman是一个API开发协作平台，它允许您使用预设变量设置环境、共享API收藏集、简化CRUD请求等。 大多数Platform API服务都具有Postman集合，可用于协助进行API调用。

## 如何设置Postman环境以进行Experience Platform

以下视频指南概述了如何创建和设置Postman环境。 Postman环境包含对下面提供的各种集合进行API调用所需的所有标头。 设置完成后，每当值过期（例如`ACCESS_TOKEN`）时，您便可以更新环境中的当前值，并且此新值将在您的所有收藏集中使用。

>[!VIDEO](https://video.tv.adobe.com/v/28832)

## 邮递员收藏集 {#collections}

可通过访问[Experience PlatformPostman示例GitHub存储库](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/experience-platform)，找到包含所有可用Postman集合的文件夹。 或者，可以在[API引用文档](https://www.adobe.com/go/platform-api-reference-en)的Adobe I/O上的每个swagger文件中找到Postman收集链接。

要下载Postman集合，请从GitHub页面中选择&#x200B;**[!DNL Raw]** ，以在新选项卡中加载原始JSON文件。 然后，右键单击并选择&#x200B;**[!DNL Save as]**&#x200B;以将文件保存到您选择的本地目标。

![原始JSON](./images/api-guide/raw-collection.PNG)

## 导入Postman集合 {#import}

要使用[Postman集合](#collections)，您需要设置环境。 完成环境设置后，请选择右上角的&#x200B;**[!DNL Manage Environments]**&#x200B;选择器。

![管理环境选择器](./images/api-guide/environment-selector.png)

此时会出现一个弹出窗口，其中显示了您当前的所有环境。 要导入集合，请选择&#x200B;**[!DNL import]** 。

![导入按钮](./images/api-guide/import-collection.png)

系统会要求您选择要导入的文件。 选择要导入的Postman集合文件。 选择收藏集后，收藏集会填充在收藏集选项卡下的左边栏中。

![填充集合](./images/api-guide/imported-collection.png)

每个集合具有不同的键值对，执行成功CRUD操作可能需要这些键值对。 请查看服务的[API开发人员指南](api-guide.md#api-guides) ，了解所需值、提示，并查看示例。

要进一步了解Postman UI及其可用功能，请访问[Postman文档](https://learning.postman.com/docs/getting-started/navigating-postman/)。

### 使用Postman生成用于非生产用途的访问令牌

>[!WARNING]
>
>如Adobe I/O访问令牌生成Postman集合中所述，表示的生成方法适用于&#x200B;**非生产用途**。 本地签名从第三方主机加载JavaScript库，远程签名将私钥发送到由Adobe拥有和运行的Web服务。 虽然Adobe不存储此私钥，但生产密钥绝不应与任何人共享。

以下视频使用[Adobe I/O访问令牌生成集合](https://github.com/adobe/experience-platform-postman-samples/blob/master/apis/ims/Adobe%20IO%20Access%20Token%20Generation.postman_collection.json)，可从公共GitHub存储库下载该集合。

>[!VIDEO](https://video.tv.adobe.com/v/29698/?quality=12&learn=on)

## 后续步骤

本文档介绍了Postman环境、收藏集以及如何导入收藏集。 现在，您已准备好Postman，请访问[平台入门指南](api-guide.md) ，以了解有关所需标头、示例和每个Platform服务可用的[API指南](api-guide.md#api-guides)列表的信息。
