---
keywords: Experience Platform;home;popular topics;query service;Query service;Aqua Data Studio;Aqua data studio;connect to query service;
solution: Experience Platform
title: 与Aqua Data Studio连接
topic: connect
description: 此文档通过步骤将Aqua Data Studio与Adobe Experience Platform查询服务连接。
translation-type: tm+mt
source-git-commit: 9fbb6b829cd9ddec30f22b0de66874be7710e465
workflow-type: tm+mt
source-wordcount: '262'
ht-degree: 0%

---


# 连接[!DNL Aqua Data Studio]

此文档介绍将[!DNL Aqua Data Studio]与Adobe Experience Platform[!DNL Query Service]连接的步骤。

安装[!DNL Aqua Data Studio]后，必须先注册服务器。 在主菜单中，单击&#x200B;**[!UICONTROL 服务器]**，然后单击&#x200B;**[!UICONTROL 注册服务器]**。

![](../images/clients/aqua-data-studio/register-server.png)

出现&#x200B;**[!UICONTROL 注册服务器]**&#x200B;对话框。 在&#x200B;**[!UICONTROL 常规]**&#x200B;选项卡下，从左侧的列表中选择&#x200B;**[!UICONTROL PostgreSQL]**。 在显示的对话框中，提供以下服务器设置的详细信息。

- **[!UICONTROL 名称]**:连接的名称。
- **[!UICONTROL 登录名和口令]**:将使用的登录凭据。用户名采用`ORG_ID@AdobeOrg`的形式。
- **[!UICONTROL 主机和端口]**:主机端点及其端口 [!DNL Query Service]。必须使用端口80连接[!DNL Query Service]。
- **[!UICONTROL 数据库]:** 将使用的数据库。

>[!NOTE]
>
>有关查找登录凭据、主机、端口和数据库名称的详细信息，请访问Platform](https://platform.adobe.com/query/configuration)上的[凭据页。 要查找您的凭据，请登录[!DNL Platform]，单击&#x200B;**[!UICONTROL 查询]**，然后单击&#x200B;**[!UICONTROL 凭据]**。

![](../images/clients/aqua-data-studio/register-server-general-tab.png)

选择&#x200B;**[!UICONTROL 驱动程序]**&#x200B;选项卡。 在&#x200B;**[!UICONTROL 参数]**&#x200B;下，将值设置为`?sslmode=require`

![](../images/clients/aqua-data-studio/register-server-driver-tab.png)

输入连接详细信息后，单击&#x200B;**[!UICONTROL 测试连接]**&#x200B;以确保凭据正常工作。 如果连接成功，请单击&#x200B;**[!UICONTROL 保存]**&#x200B;以注册服务器。 成功注册后，连接将显示在&#x200B;**仪表板**&#x200B;上，确认您现在可以连接到服务器并视图其模式对象。

## 后续步骤

现在已连接到[!DNL Query Service]，您可以使用[!DNL Aqua Data Studio]中的&#x200B;**[!UICONTROL 查询分析器]**&#x200B;执行和编辑SQL语句。 有关如何编写和运行查询的详细信息，请阅读[运行查询指南](../best-practices/writing-queries.md)。