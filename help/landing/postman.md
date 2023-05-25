---
keywords: Experience Platform；主页；热门主题；Adobe Experience Platform；api指南；平台api指南；平台简介；开发人员指南
solution: Experience Platform
title: Adobe Experience Platform中的Postman
description: 本文档包含概述如何设置Postman环境、导入Postman收藏集的步骤，以及每个Platform服务的可用收藏集列表。
exl-id: a09b3875-97f5-47f1-a562-52decbce67b1
source-git-commit: 5a14eb5938236fa7186d1a27f28cee15fe6558f6
workflow-type: tm+mt
source-wordcount: '545'
ht-degree: 0%

---

# Adobe Experience Platform中的Postman

Postman是API开发的协作平台，允许您使用预设变量设置环境、共享API收藏集、简化CRUD请求等。 大多数Platform API服务都有Postman集合，可用于协助进行API调用。

## 如何设置用于Experience Platform的Postman环境

以下视频指南概述了如何创建和设置Postman环境。 Postman环境包含对下面提供的各种收藏集进行API调用所需的所有标头。 设置后，值在任意时间过期(例如 `ACCESS_TOKEN`)您可以更新环境中的当前值，并且此新值将在您的所有收藏集中使用。

>[!VIDEO](https://video.tv.adobe.com/v/28832)

## Postman收藏集 {#collections}

要找到包含所有可用Postman收藏集的文件夹，请访问 [Experience PlatformPostman示例GitHub存储库](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/experience-platform). 或者，也可以在的每个swagger文件中找到Postman收藏集链接 [API参考文档](https://www.adobe.com/go/platform-api-reference-en) 在Adobe I/O时。

要下载Postman收藏集，请选择 **[!DNL Raw]** 从GitHub页面加载原始JSON文件到新选项卡中。 然后，右键单击并选择 **[!DNL Save as]** 将文件保存到您选择的本地目标。

![原始JSON](./images/api-guide/raw-collection.PNG)

## 导入Postman收藏集 {#import}

为了利用 [Postman收藏集](#collections)，您需要设置一个环境。 完成环境设置后，选择 **[!DNL Manage Environments]** 选择器图标。

![管理环境选择器](./images/api-guide/environment-selector.png)

此时会出现一个弹出窗口，并显示所有当前环境。 要导入收藏集，请选择 **[!DNL import]** .

![导入按钮](./images/api-guide/import-collection.png)

系统会要求您选择要导入的文件。 选择要导入的Postman收藏集文件。 选中后，收藏集将填充到左边栏中的收藏集选项卡下。

![填充集合](./images/api-guide/imported-collection.png)

每个集合都有不同的键值对，成功执行CRUD操作可能需要这些键值对。 请查看服务的 [API开发人员指南](api-guide.md#api-guides) 了解有关所需值、提示和查看示例的信息。

要了解有关Postman UI及其可用功能的更多信息，请访问 [Postman文档](https://learning.postman.com/docs/getting-started/navigating-postman/).

### 使用Postman生成访问令牌以供非生产使用

>[!WARNING]
>
>如Identity Management服务(IMS) Postman集合中所述，所指示的生成方法适用于 **非生产使用**. 本地签名从第三方主机加载JavaScript库，远程签名将私钥发送到Adobe拥有和操作的Web服务。 虽然Adobe不会存储此私钥，但绝不应该与任何人共享生产密钥。

以下视频使用 [Identity Management服务(IMS) Postman收藏集](https://github.com/adobe/experience-platform-postman-samples/blob/master/apis/ims/Identity%20Management%20Service.postman_collection.json) 可以从公共GitHub存储库下载。

>[!VIDEO](https://video.tv.adobe.com/v/29698/?quality=12&learn=on)

## 后续步骤

本文档介绍了Postman环境、收藏集以及如何导入收藏集。 现在您已准备好Postman，请访问 [Platform入门指南](api-guide.md) 有关所需标头、示例和列表的信息 [API指南](api-guide.md#api-guides) 可用于各平台服务。
