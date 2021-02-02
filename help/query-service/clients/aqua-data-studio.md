---
keywords: Experience Platform；主页；热门主题；查询服务；查询服务；Aqua Data Studio;Aqua Data Studio；连接到查询服务；
solution: Experience Platform
title: 与Aqua Data Studio连接
topic: connect
description: 此文档通过步骤将Aqua Data Studio与Adobe Experience Platform查询服务连接。
translation-type: tm+mt
source-git-commit: eac93f3465fa6ce4af7a6aa783cf5f8fb4ac9b9b
workflow-type: tm+mt
source-wordcount: '297'
ht-degree: 1%

---


# [!DNL Aqua Data Studio]

本文档介绍将[!DNL Aqua Data Studio]与Adobe Experience Platform[!DNL Query Service]连接的步骤。

>[!NOTE]
>
> 本指南假定您已经具有访问[!DNL Aqua Data Studio]的权限，并且熟悉如何导航其接口。 有关[!DNL Aqua Data Studio]的详细信息，请参阅[offical [!DNL Aqua Data Studio] 文档](https://www.aquaclusters.com/app/home/project/public/aquadatastudio/wikibook/Documentation21.1/page/0/Aqua-Data-Studio-21-1)。

## 连接[!DNL Aqua Data Studio]与平台

安装[!DNL Aqua Data Studio]后，必须先注册服务器。 从主菜单中，选择&#x200B;**[!DNL Server]**，后跟&#x200B;**[!DNL Register Server]**。

![](../images/clients/aqua-data-studio/register-server.png)

出现&#x200B;**[!DNL Register Server]**&#x200B;对话框。 在&#x200B;**[!DNL General]**&#x200B;选项卡下，从左侧的列表中选择&#x200B;**[!DNL PostgreSQL]**。 在显示的对话框中，提供以下服务器设置的详细信息。

- **[!DNL Name]**:连接的名称。
- **[!DNL Login Name and Password]**:将使用的登录凭据。用户名采用`ORG_ID@AdobeOrg`的形式。
- **[!DNL Host and Port]**:主机端点及其端口 [!DNL Query Service]。必须使用端口80连接[!DNL Query Service]。
- **[!DNL Database]:** 将使用的数据库。

>[!NOTE]
>
>有关查找登录凭据、主机、端口和数据库名称的详细信息，请访问Platform](https://platform.adobe.com/query/configuration)上的[凭据页。 要查找您的凭据，请登录[!DNL Platform]，然后选择&#x200B;**[!UICONTROL 查询]**，后跟&#x200B;**[!UICONTROL 凭据]**。

![](../images/clients/aqua-data-studio/register-server-general-tab.png)

选择 **[!DNL Driver]** 选项卡。在&#x200B;**[!DNL Parameters]**&#x200B;下，将值设置为`?sslmode=require`

![](../images/clients/aqua-data-studio/register-server-driver-tab.png)

输入连接详细信息后，选择&#x200B;**[!DNL Test Connection]**&#x200B;以确保凭据正常工作。 如果连接成功，请选择&#x200B;**[!DNL Save]**&#x200B;注册服务器。 成功注册后，仪表板上会显示连接，确认您现在可以连接到服务器并视图其模式对象。

## 后续步骤

现在已连接到[!DNL Query Service]，您可以使用[!DNL Aqua Data Studio]中的&#x200B;**[!DNL Query Analyzer]**&#x200B;执行和编辑SQL语句。 有关如何编写和运行查询的详细信息，请阅读[运行查询指南](../best-practices/writing-queries.md)。