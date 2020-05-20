---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Google Cloud存储连接器
topic: overview
translation-type: tm+mt
source-git-commit: 256a193e56e69078d1c01c622656f0b1a18e73ff
workflow-type: tm+mt
source-wordcount: '377'
ht-degree: 0%

---


# Google Cloud存储连接器

Adobe Experience Platform为AWS、Google Cloud Platform和Azure等云提供商提供本机连接。 您可以将这些系统中的数据引入平台。

云存储源可以将您自己的数据导入平台，而无需下载、格式化或上传。 摄取的数据可格式化为XDM JSON、XDM镶木地板或分隔。 流程的每个步骤都集成到源工作流中。 平台允许您通过批量方式从Google Cloud存储导入数据。

## 连接Google Cloud存储帐户的先决条件设置

要连接到平台，您必须首先为Google Cloud存储帐户启用互操作性。 要访问互操作性设置，请打开Google Cloud Platform，然 **[!UICONTROL 后从导航面]** 板的 **[!UICONTROL “存储]** ”选项中选择“设置”。

![](../../images/tutorials/create/google-cloud-storage/nav.png)

将显 **[!UICONTROL 示]** “设置”页。 从此处，您可以看到有关Google项目ID的信息和有关Google Cloud存储帐户的详细信息。 要访问互操作性设置，请 **[!UICONTROL 从顶部]** 标题中选择互操作性。

![](../../images/tutorials/create/google-cloud-storage/project-access.png)

“互 **[!UICONTROL 操作性]** ”页包含有关身份验证、访问密钥以及与用户帐户关联的默认项目的信息。 如果尚未建立可互操作访问的默认项目，则可以从“可互操作访问的默认项目”部 *[!UICONTROL 分设置一个项目]* 。 如果已建立默认项目，则此部分将显示一条确认消息，指明项目已设置为默认项目。

要为用户帐户生成新的访问密钥ID和密钥访问密钥，请选 **[!UICONTROL 择创建密钥]**。

![](../../images/tutorials/create/google-cloud-storage/interoperability.png)

您可以使用新生成的访问密钥ID和秘密访问密钥将您的Google Cloud存储帐户连接到平台。

以下文档提供了如何使用API或用户界面将Google Cloud存储连接到平台的信息：

## 将Google Cloud存储连接到平台

以下文档提供了如何使用API或用户界面将Google Cloud存储连接到平台的信息：

### 使用API

- [使用Flow Service API创建Google Cloud存储连接器](../../tutorials/api/create/cloud-storage/google.md)
- [使用Flow Service API浏览云存储系统](../../tutorials/api/explore/cloud-storage.md)
- [使用流服务API收集云存储数据](../../tutorials/api/collect/cloud-storage.md)

### 使用UI

- [在UI中创建Google Cloud存储源连接器](../../tutorials/ui/create/cloud-storage/google-cloud-storage.md)
- [在UI中为云存储连接器配置数据流](../../tutorials/ui/dataflow/batch/cloud-storage.md)