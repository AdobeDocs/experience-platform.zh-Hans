---
keywords: Experience Platform；主页；热门主题；查询服务；查询服务；Aqua Data Studio;Aqua Data Studio；连接到查询服务；
solution: Experience Platform
title: 将Aqua Data Studio连接到查询服务
topic-legacy: connect
description: 本文档将介绍将Aqua Data Studio与Adobe Experience Platform查询服务连接的步骤。
exl-id: 4770e221-48a7-45d8-80a4-60b5cbc0ec33
source-git-commit: 75e97efcb68439f1b837af93b62c96f43e5d7a31
workflow-type: tm+mt
source-wordcount: '487'
ht-degree: 0%

---

# 连接 [!DNL Aqua Data Studio] 查询服务

本文档介绍了连接的步骤 [!DNL Aqua Data Studio] 与Adobe Experience Platform [!DNL Query Service].

## 快速入门

本指南要求您已拥有 [!DNL Aqua Data Studio] 并熟悉如何导航其界面。 有关 [!DNL Aqua Data Studio] 可在 [官方 [!DNL Aqua Data Studio] 文档](https://www.aquaclusters.com/app/home/project/public/aquadatastudio/wikibook/Documentation21.1/page/0/Aqua-Data-Studio-21-1).

>[!NOTE]
>
>有 [!DNL Windows] 和 [!DNL macOS] 版本 [!DNL Aqua Data Studio]. 本指南中的屏幕截图是使用 [!DNL macOS] 桌面应用程序。 版本之间的UI可能存在细微差异。

获取连接所需的凭据 [!DNL Aqua Data Studio] 要Experience Platform，您必须拥有 [!UICONTROL 查询] 工作区。 如果您当前没有访问 [!UICONTROL 查询] 工作区。

## 注册服务器 {#register-server}

安装后 [!DNL Aqua Data Studio]，则必须先注册服务器。 从主菜单中，选择 **[!DNL Server]**，后跟 **[!DNL Register Server]**.

![“Register Server（注册服务器）”下拉菜单突出显示。](../images/clients/aqua-data-studio/register-server.png)

的 **[!DNL Register Server]** 对话框。 在 **[!DNL General]** 选项卡，选择 **[!DNL PostgreSQL]** 从左侧的列表中。 在显示的对话框中，提供有关服务器设置的以下详细信息。

- **[!DNL Name]**:连接的名称。 建议您提供一个用于识别连接的友好名称。
- **[!DNL Login Name]**:登录名是您的平台组织ID。 它以 `ORG_ID@AdobeOrg`.
- **[!DNL Password]**:这是在 [!DNL Query Service] 凭据功能板。
- **[!DNL Host and Port]**:主机端点及其端口 [!DNL Query Service]. 必须使用端口80连接 [!DNL Query Service].
- **[!DNL Database]:** 将使用的数据库。 将值用于Platform UI凭据 `dbname`: `prod:all`.

![的 [!DNL Aqua Data Studio] “常规”选项卡，其中突出显示了必填输入字段。](../images/clients/aqua-data-studio/register-server-general-tab.png)

### [!DNL Query Service] 凭据

要查找您的凭据，请登录到 [!DNL Platform] UI和选择 **[!UICONTROL 查询]** 从左侧导航，然后是 **[!UICONTROL 凭据]**. 有关查找登录凭据、主机、端口和数据库名称的完整说明，请阅读 [凭据指南](../ui/credentials.md).

[!DNL Query Service] 此外，还提供了未过期的凭据，以便能够与第三方客户端进行一次性设置。 请参阅相关文档 [有关如何生成和使用未过期凭据的完整说明](../ui/credentials.md#non-expiring-credentials).

### 设置SSL模式

接下来，选择 **[!DNL Driver]** 选项卡。 在 **[!DNL Parameters]**，请将值设置为 `?sslmode=require`

>[!IMPORTANT]
>
>请参阅 [[!DNL Query Service] SSL文档](./ssl-modes.md) 了解对与Adobe Experience Platform查询服务的第三方连接的SSL支持，以及如何使用 `verify-full` SSL模式。

![的 [!DNL Aqua Data Studio] “参数”字段突出显示的“驱动程序”选项卡。](../images/clients/aqua-data-studio/register-server-driver-tab.png)

输入连接详细信息后，选择 **[!DNL Test Connection]** 以确保凭据正常工作。 如果连接测试成功，请选择 **[!DNL Save]** 注册服务器。 确认对话框显示确认连接，并且连接显示在仪表板上。 您现在可以连接到服务器并查看其架构对象。

## 后续步骤

现在，您已连接到 [!DNL Query Service]，则可以使用 **[!DNL Query Analyzer]** within [!DNL Aqua Data Studio] 执行和编辑SQL语句。 有关如何编写和运行查询的详细信息，请阅读 [运行查询指南](../best-practices/writing-queries.md).
