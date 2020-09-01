---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Google Cloud存储连接器
topic: overview
translation-type: tm+mt
source-git-commit: 1bb896f7629d7b71b94dd107eeda87701df99208
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 0%

---


# Google Cloud存储连接器

Adobe Experience Platform为AWS等云提供商提 [!DNL Google Cloud Platform]供本 [!DNL Azure]机连接，允许您从这些系统获取数据。

云存储源无需下载、格式化 [!DNL Platform] 或上传即可将您自己的数据导入其中。 摄取的数据可格式化为XDM JSON、XDM镶木地板或分隔。 流程的每个步骤都集成到源工作流中。 [!DNL Platform] 允许您从批中导入 [!DNL Google Cloud Storage] 数据。

## IP地址允许列表

在使用源连接器之前，必须将以下IP地址添加到允许列表。 如果无法向允许列表添加特定于区域的IP地址，则在使用源时可能会导致错误或性能不佳。

### 美国东部地区

- `20.41.2.0/23`
- `20.41.4.0/26`
- `20.44.17.80/28`
- `20.49.102.16/29`
- `40.70.148.160/28`
- `52.167.107.224/28`

### 西欧地区

- `13.69.67.192/28`
- `13.69.107.112/28`
- `13.69.112.128/28`
- `40.74.24.192/26`
- `40.74.26.0/23`
- `40.113.176.232/29`
- `52.236.187.112/28`

### 澳大利亚东部

- `13.70.74.144/28`
- `20.37.193.0/25`
- `20.37.193.128/26`
- `20.37.198.224/29`
- `40.79.163.80/28`
- `40.79.171.160/28`

## 连接帐户的入门项目设 [!DNL Google Cloud Storage] 置

要连接到，您必 [!DNL Platform]须首先为您的帐户启用互操作 [!DNL Google Cloud Storage] 性。 要访问互操作性设置，请打 [!DNL Google Cloud Platform] 开并从导 **[!UICONTROL 航面板]** 的存储 **[!UICONTROL 选项中选]** 择“设置”。

![](../../images/tutorials/create/google-cloud-storage/nav.png)

将显 **[!UICONTROL 示]** “设置”页。 从此处，您可以看到有关您的项目ID [!DNL Google] 的信息以及有关您帐户的详 [!DNL Google Cloud Storage] 细信息。 要访问互操作性设置，请 **[!UICONTROL 从顶部]** 标题中选择互操作性。

![](../../images/tutorials/create/google-cloud-storage/project-access.png)

“互 **[!UICONTROL 操作性]** ”页包含有关身份验证、访问密钥以及与用户帐户关联的默认项目的信息。 如果尚未建立可互操作访问的默认项目，则可以从“可互操作访问的默认项目”部 **[!UICONTROL 分设置一个项目]** 。 如果已建立默认项目，则此部分将显示一条确认消息，指明项目已设置为默认项目。

要为用户帐户生成新的访问密钥ID和密钥访问密钥，请选 **[!UICONTROL 择创建密钥]**。

![](../../images/tutorials/create/google-cloud-storage/interoperability.png)

您可以使用新生成的访问密钥ID和秘密访问密钥将您的帐户 [!DNL Google Cloud Storage] 连接到 [!DNL Platform]。

## 连接 [!DNL Google Cloud Storage] 到 [!DNL Platform]

以下文档提供了如何使用API [!DNL Google Cloud Storage] 或 [!DNL Platform] 用户界面连接的信息：

### 使用API

- [使用Flow Service API创建Google Cloud存储连接器](../../tutorials/api/create/cloud-storage/google.md)
- [使用Flow Service API浏览云存储系统](../../tutorials/api/explore/cloud-storage.md)
- [使用流服务API收集云存储数据](../../tutorials/api/collect/cloud-storage.md)

### 使用UI

- [在UI中创建Google Cloud存储源连接器](../../tutorials/ui/create/cloud-storage/google-cloud-storage.md)
- [在UI中为云存储连接器配置数据流](../../tutorials/ui/dataflow/batch/cloud-storage.md)