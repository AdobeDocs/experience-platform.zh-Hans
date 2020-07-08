---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 与Aqua Data Studio连接
topic: connect
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '257'
ht-degree: 0%

---


# 与Aqua Data Studio连接

此文档通过步骤将Aqua Data Studio与Adobe Experience Platform查询服务连接。

安装Aqua Data Studio后，必须先注册服务器。 在主菜单中，单击“服 **务器**”，然后单击“ **注册服务器”**。

![](../images/clients/aqua-data-studio/register-server.png)

出现“ *注册服务器* ”对话框。 在“ *常规* ”选项卡 **下** ，从左侧的列表中选择PostgreSQL。 在显示的对话框中，提供以下服务器设置的详细信息。

- **名称**: 连接的名称。
- **登录名和口令**: 将使用的登录凭据。 用户名采用的形式 `ORG_ID@AdobeOrg`。
- **主机和端口**: 主机端点及其查询服务端口。
- **数据库：** 将使用的数据库。

>[!NOTE]
>
>有关查找登录凭据、主机、端口和数据库名称的详细信息，请访 [问平台上的凭据页](https://platform.adobe.com/query/configuration)。 要查找凭据，请登录平台，单击 **查询**，然后单 **击凭据**。

![](../images/clients/aqua-data-studio/register-server-general-tab.png)

选择“驱动 **程序** ”选项卡。 在“ *参数*”下，将值设置为 `?sslmode=require`

![](../images/clients/aqua-data-studio/register-server-driver-tab.png)

输入连接详细信息后，单击“ **测试连接** ”以确保凭据正常工作。 如果连接成功，请单击“保 **存** ”以注册服务器。 成功注册后， *仪表板* 上会显示连接，确认您现在可以连接到服务器并视图其模式对象。

## 后续步骤

现在您已连接到查询服务，可以使用Aqua Data Studio中 *的查询* Analyzer执行和编辑SQL语句。 有关如何编写和运行查询的更多信息，请阅读运 [行查询指南](../creating-queries/creating-queries.md)。