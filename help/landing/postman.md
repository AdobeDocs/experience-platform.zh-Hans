---
keywords: Experience Platform；主页；热门主题；Adobe Experience Platform;API指南；平台API指南；平台简介；开发人员指南
solution: Experience Platform
title: Postman在Adobe Experience Platform
description: 本文档包含概述如何设置Postman环境、导入Postman收藏集以及每个Platform服务可用收藏集列表的步骤。
exl-id: a09b3875-97f5-47f1-a562-52decbce67b1
source-git-commit: 5a14eb5938236fa7186d1a27f28cee15fe6558f6
workflow-type: tm+mt
source-wordcount: '545'
ht-degree: 0%

---

# Postman在Adobe Experience Platform

Postman是一个API开发协作平台，它允许您使用预设变量设置环境、共享API收藏集、简化CRUD请求等。 大多数Platform API服务都有Postman集合，可用于协助进行API调用。

## 如何设置Postman环境以进行Experience Platform

以下视频指南概述了如何创建和设置Postman环境。 Postman环境包含对下面提供的各种集合进行API调用所需的所有标头。 设置后，值随时过期(例如 `ACCESS_TOKEN`)，则您可以更新环境中的当前值，并且此新值将在所有收藏集中使用。

>[!VIDEO](https://video.tv.adobe.com/v/28832)

## Postman收藏集 {#collections}

可通过访问以下网站找到包含所有可用Postman收藏集的文件夹： [Experience PlatformPostman示例GitHub存储库](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/experience-platform). 或者，Postman收集链接位于 [API参考文档](https://www.adobe.com/go/platform-api-reference-en) Adobe I/O。

要下载Postman收藏集，请选择 **[!DNL Raw]** 从GitHub页面，在新选项卡中加载原始JSON文件。 然后，右键单击并选择 **[!DNL Save as]** 将文件保存到您选择的本地目标。

![原始JSON](./images/api-guide/raw-collection.PNG)

## 导入Postman集合 {#import}

为了利用 [Postman收藏集](#collections)，则需要设置环境。 完成环境设置后，选择 **[!DNL Manage Environments]** 选择器。

![管理环境选择器](./images/api-guide/environment-selector.png)

此时会出现一个弹出窗口，其中显示了您当前的所有环境。 要导入收藏集，请选择 **[!DNL import]** .

![导入按钮](./images/api-guide/import-collection.png)

系统会要求您选择要导入的文件。 选择要导入的Postman集合文件。 选择收藏集后，收藏集会填充在收藏集选项卡下的左边栏中。

![填充集合](./images/api-guide/imported-collection.png)

每个集合具有不同的键值对，执行成功CRUD操作可能需要这些键值对。 请查看服务的 [API开发人员指南](api-guide.md#api-guides) 以了解所需的值、提示和查看示例。

要进一步了解Postman UI及其可用功能，请访问 [Postman文档](https://learning.postman.com/docs/getting-started/navigating-postman/).

### 使用Postman生成用于非生产用途的访问令牌

>[!WARNING]
>
>如Identity Management Service(IMS)Postman集合中所述，表示的生成方法适合 **非生产用途**. 本地签名从第三方主机加载JavaScript库，远程签名将私钥发送到由Adobe拥有和运行的Web服务。 虽然Adobe不存储此私钥，但生产密钥绝不应与任何人共享。

以下视频使用 [Identity Management Service(IMS)Postman收集](https://github.com/adobe/experience-platform-postman-samples/blob/master/apis/ims/Identity%20Management%20Service.postman_collection.json) 可从公共GitHub存储库下载。

>[!VIDEO](https://video.tv.adobe.com/v/29698/?quality=12&learn=on)

## 后续步骤

本文档介绍了Postman环境、收藏集以及如何导入收藏集。 现在，您已准备好Postman，请访问 [平台快速入门指南](api-guide.md) 有关所需标题、示例和 [API指南](api-guide.md#api-guides) 适用于每个平台服务。
