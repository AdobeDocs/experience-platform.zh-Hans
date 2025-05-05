---
keywords: Experience Platform；主页；热门主题；Adobe Experience Platform；API指南；平台API指南；平台简介；开发人员指南
solution: Experience Platform
title: Adobe Experience Platform中的Postman
description: 本文档包含概述如何设置Postman环境、导入Postman收藏集的步骤，以及每个Experience Platform服务的可用收藏集列表。
role: Developer
feature: API
exl-id: a09b3875-97f5-47f1-a562-52decbce67b1
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '524'
ht-degree: 0%

---

# Adobe Experience Platform中的Postman

Postman是API开发的协作平台，允许您使用预设变量设置环境、共享API收藏集、简化CRUD请求等。 大多数Experience Platform API服务都具有Postman收藏集，这些收藏集可用于协助进行API调用。

## 如何为Experience Platform设置Postman环境

以下视频指南概述了如何创建和设置Postman环境。 Postman环境包含您对下面提供的各种收藏集进行API调用所需的所有标头。 设置后，每当某个值过期（如`ACCESS_TOKEN`）时，您都可以更新环境中的当前值，此新值将在您的所有收藏集中使用。

>[!VIDEO](https://video.tv.adobe.com/v/31668?captions=chi_hans)

## Postman收藏集 {#collections}

访问[Experience Platform Postman示例GitHub存储库](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/experience-platform)，即可找到包含所有可用Postman收藏集的文件夹。 或者，也可以在Adobe I/O上的[API参考文档](https://www.adobe.com/go/platform-api-reference-en)中的每个Swagger文件中找到Postman收藏集链接。

要下载Postman收藏集，请从GitHub页面中选择&#x200B;**[!DNL Raw]**&#x200B;以在新选项卡中加载原始JSON文件。 然后，右键单击并选择&#x200B;**[!DNL Save as]**&#x200B;以将文件保存到您选择的本地目标。

![原始JSON](./images/api-guide/raw-collection.PNG)

## 导入Postman收藏集 {#import}

为了利用[Postman收藏集](#collections)，您需要设置一个环境。 完成环境设置后，选择右上角的&#x200B;**[!DNL Manage Environments]**&#x200B;选择器。

![管理环境选择器](./images/api-guide/environment-selector.png)

此时会出现一个弹出窗口，其中显示所有当前环境。 要导入收藏集，请选择&#x200B;**[!DNL import]** 。

![导入按钮](./images/api-guide/import-collection.png)

系统会要求您选择要导入的文件。 选择要导入的Postman收藏集文件。 选中后，收藏集将填充到左边栏中的收藏集选项卡下。

![填充集合](./images/api-guide/imported-collection.png)

每个集合都有不同的键值对，成功执行CRUD操作可能需要这些键值对。 请查看服务的[API开发人员指南](api-guide.md#api-guides)，了解所需的值、提示并查看示例。

要了解有关Postman UI及其可用功能的更多信息，请访问[Postman文档](https://learning.postman.com/docs/getting-started/navigating-postman/)。

### 使用Postman生成访问令牌以供非生产使用

>[!WARNING]
>
>如Identity Management服务(IMS) Postman集合中所述，所表示的生成方法适用于&#x200B;**非生产使用**。 本地签名从第三方主机加载JavaScript库，而远程签名将私钥发送到Adobe拥有和运营的Web服务。 虽然Adobe不存储此私钥，但绝不应该与任何人共享生产密钥。

以下视频使用[Identity Management服务(IMS) Postman收藏集](https://github.com/adobe/experience-platform-postman-samples/blob/master/apis/ims/Identity%20Management%20Service.postman_collection.json)，该收藏集可从公共GitHub存储库下载。

>[!VIDEO](https://video.tv.adobe.com/v/32725/?quality=12&learn=on&captions=chi_hans)

## 后续步骤

本文档介绍了Postman环境、收藏集以及如何导入收藏集。 现在您已准备好Postman，请访问[Experience Platform快速入门指南](api-guide.md)，了解有关每个Experience Platform服务可用的所需标头、示例和[API指南](api-guide.md#api-guides)列表的信息。
