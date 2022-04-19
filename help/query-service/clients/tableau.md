---
keywords: Experience Platform；主页；热门主题；表格；表格；查询服务；查询服务；连接到查询服务；
solution: Experience Platform
title: 将 Tableau 连接到查询服务
topic-legacy: connect
description: 本文档将介绍如何将Tableau与Adobe Experience Platform查询服务连接。
exl-id: f380aacd-5091-41bc-97ca-593e0b1670fd
source-git-commit: ad3e1b0de6dd3b82cc82f0dc3d0f36b12cd3899e
workflow-type: tm+mt
source-wordcount: '233'
ht-degree: 3%

---

# 连接 [!DNL Tableau] 查询服务

本文档介绍将Tableau与Adobe Experience Platform连接的步骤 [!DNL Query Service].

>[!NOTE]
>
> 本指南假定您已拥有 [!DNL Tableau] 并熟悉如何导航其界面。 有关 [!DNL Tableau] 可在 [官方 [!DNL Tableau] 文档](https://help.tableau.com/current/pro/desktop/en-us/default.htm).

连接 [!DNL Tableau] to [!DNL Query Service]，打开 [!DNL Tableau]和 **[!DNL To a Server]** 部分选择 **[!DNL More]** 后跟 **[!DNL PostgreSQL]**

![](../images/clients/tableau/open-connection.png)

您现在可以输入值以连接Adobe Experience Platform。 有关查找数据库名称、主机、端口和登录凭据的详细信息，请阅读 [凭据指南](../ui/credentials.md). 要查找您的凭据，请登录到 [!DNL Platform]，然后选择 **[!UICONTROL 查询]**，后跟 **[!UICONTROL 凭据]**.

确保已检查 **[!UICONTROL 需要SSL]** 框中，选择是否在尝试连接之前。

>[!IMPORTANT]
>
>请参阅 [[!DNL Query Service] SSL文档](./ssl-modes.md) 了解对与Adobe Experience Platform查询服务的第三方连接的SSL支持，以及如何使用 `verify-full` SSL模式。

填写所有凭据后，选择 **[!DNL Sign In]** 继续。

![](../images/clients/tableau/sign-in.png)

您现在已连接到Adobe Experience Platform，并在侧面显示表的列表。

![](../images/clients/tableau/connected.png)

## 后续步骤

现在你已经连接了 [!DNL Query Service]，您可以使用 [!DNL Tableau] 来编写查询。 有关如何编写和运行查询的详细信息，请阅读 [运行查询](../best-practices/writing-queries.md).
