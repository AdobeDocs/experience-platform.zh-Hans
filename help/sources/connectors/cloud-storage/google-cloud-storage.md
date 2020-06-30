---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Google Cloud存储连接器
topic: overview
translation-type: tm+mt
source-git-commit: 6ffdcc2143914e2ab41843a52dc92344ad51bcfb
workflow-type: tm+mt
source-wordcount: '337'
ht-degree: 0%

---


# Google Cloud存储连接器

Adobe Experience Platform为AWS等云提供商提 [!DNL Google Cloud Platform]供本 [!DNL Azure]机连接，允许您从这些系统获取数据。

云存储源无需下载、格式化 [!DNL Platform] 或上传即可将您自己的数据导入其中。 摄取的数据可格式化为XDM JSON、XDM镶木地板或分隔。 流程的每个步骤都集成到源工作流中。 [!DNL Platform] 允许您从批中导入 [!DNL Google Cloud Storage] 数据。

## 连接帐户的入门项目设 [!DNL Google Cloud Storage] 置

要连接到，您必 [!DNL Platform]须首先为您的帐户启用互操作 [!DNL Google Cloud Storage] 性。 要访问互操作性设置，请打 [!DNL Google Cloud Platform] 开并从导 **[!UICONTROL 航面板]** 的存储 **[!UICONTROL 选项中选]** 择“设置”。

![](../../images/tutorials/create/google-cloud-storage/nav.png)

将显 **[!UICONTROL 示]** “设置”页。 从此处，您可以看到有关项目ID的 [!DNL Google] 信息以及有关帐户的详细 [!DNL Google Cloud Storage] 信息。 要访问互操作性设置，请 **[!UICONTROL 从顶部]** 标题中选择互操作性。

![](../../images/tutorials/create/google-cloud-storage/project-access.png)

“互 **[!UICONTROL 操作性]** ”页包含有关身份验证、访问密钥以及与用户帐户关联的默认项目的信息。 如果尚未建立可互操作访问的默认项目，则可以从“可互操作访问的默认项目”部 *[!UICONTROL 分设置一个项目]* 。 如果已建立默认项目，则此部分将显示一条确认消息，指明项目已设置为默认项目。

要为用户帐户生成新的访问密钥ID和密钥访问密钥，请选 **[!UICONTROL 择创建密钥]**。

![](../../images/tutorials/create/google-cloud-storage/interoperability.png)

您可以使用新生成的访问密钥ID和秘密访问密钥将您的帐户 [!DNL Google Cloud Storage] 连接到 [!DNL Platform]。

以下文档提供了如何使用API [!DNL Google Cloud Storage] 或 [!DNL Platform] 用户界面连接的信息：

## 连接 [!DNL Google Cloud Storage] 到 [!DNL Platform]

以下文档提供了如何使用API [!DNL Google Cloud Storage] 或 [!DNL Platform] 用户界面连接的信息：

### 使用API

- [使用Flow Service API创建Google Cloud存储连接器](../../tutorials/api/create/cloud-storage/google.md)
- [使用Flow Service API浏览云存储系统](../../tutorials/api/explore/cloud-storage.md)
- [使用流服务API收集云存储数据](../../tutorials/api/collect/cloud-storage.md)

### 使用UI

- [在UI中创建Google Cloud存储源连接器](../../tutorials/ui/create/cloud-storage/google-cloud-storage.md)
- [在UI中为云存储连接器配置数据流](../../tutorials/ui/dataflow/batch/cloud-storage.md)