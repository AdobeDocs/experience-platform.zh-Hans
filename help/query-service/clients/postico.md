---
keywords: Experience Platform；主页；热门主题；查询服务；查询服务；postico;Postico；连接到查询服务；
solution: Experience Platform
title: 将Postico连接到查询服务
description: 本文档包含用于安装备份客户端Postico for Adobe Experience Platform查询服务的链接。
exl-id: a19abfc8-b431-4e57-b44d-c6130041af4a
source-git-commit: 58eadaaf461ecd9598f3f508fab0c192cf058916
workflow-type: tm+mt
source-wordcount: '291'
ht-degree: 0%

---

# 连接 [!DNL Postico] 到查询服务(Mac)

本文档介绍了连接的步骤 [!DNL Postico] 与Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> 本指南假定您已拥有 [!DNL Postico] 并熟悉如何导航其界面。 有关 [!DNL Postico] 可在 [官方 [!DNL Postico] 文档](https://eggerapps.at/postico/docs).
> 
> 此外， [!DNL Postico] is **仅** 可在macOS设备上获取。

连接 [!DNL Postico] 要查询服务，请打开 [!DNL Postico] 选择 **[!DNL New Favorite]**.

![的 [!DNL Postico] 突出显示了新收藏夹的UI。](../images/clients/postico/open-postico.png)

您现在可以输入值以连接Adobe Experience Platform。

有关查找数据库名称、主机、端口和登录凭据的详细信息，请阅读 [凭据指南](../ui/credentials.md). 要查找您的凭据，请登录到 [!DNL Platform]，然后选择 **[!UICONTROL 查询]**，后跟 **[!UICONTROL 凭据]**.

插入凭据后，选择 **[!DNL Connect]** 与查询服务连接。

![突出显示连接的“新建收藏夹”对话框。](../images/clients/postico/authentication-details.png)

连接到Platform后，您将能够看到以前与查询服务建立的所有关系的列表。

![中的连接列表 [!DNL Postico] UI。](../images/clients/postico/show-queries.png)

## 创建SQL语句

要创建新的SQL查询，请选择并打开“SQL查询”。

![的 [!DNL Postico] 突出显示了SQL查询快捷键的UI。](../images/clients/postico/create-query.png)

随即会出现一个框，您可以在此处键入要执行的查询。 完成后，选择 **[!DNL Execute Statement]** 以运行查询。

![突出显示了Execute语句的SQL编辑器。](../images/clients/postico/run-statement.png)

将出现一个表格，其中显示了完成查询运行的结果。

![示例查询的结果表。](../images/clients/postico/query-results.png)

## 后续步骤

现在你已经连接了 [!DNL Query Service]，您可以使用 [!DNL Postico] 来编写查询。 有关如何编写和运行查询的详细信息，请阅读 [运行查询指南](../best-practices/writing-queries.md).
