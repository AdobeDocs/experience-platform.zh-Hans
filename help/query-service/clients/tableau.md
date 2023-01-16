---
keywords: Experience Platform；主页；热门主题；表格；表格；查询服务；查询服务；连接到查询服务；
solution: Experience Platform
title: 将 Tableau 连接到查询服务
description: 本文档将介绍如何将Tableau与Adobe Experience Platform查询服务连接。
exl-id: f380aacd-5091-41bc-97ca-593e0b1670fd
source-git-commit: 1d71cc4336747eb258ec2d8dcdc545cb2233692d
workflow-type: tm+mt
source-wordcount: '447'
ht-degree: 1%

---

# 连接 [!DNL Tableau] 查询服务

本文档提供了连接信息 [!DNL Tableau] 与Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> 本指南假定您已拥有 [!DNL Tableau] 并熟悉如何导航其界面。 有关 [!DNL Tableau] 可在 [官方 [!DNL Tableau] 文档](https://help.tableau.com/current/pro/desktop/en-us/default.htm).

有关如何 [使用表格连接到PostgreSQL服务器](https://help.tableau.com/current/pro/desktop/en-us/examples_postgresql.htm) 可从官方的Tableau网站获取。 出现连接设置对话框后，在要与Adobe Experience Platform连接的参数字段中输入您的平台凭据。 下面列出了所需连接参数的列表。

| 连接参数 | 描述 |
|---|---|
| **[!DNL Server]** | SFTP存储位置的地址。 使用Experience Platform的值 **[!UICONTROL 主机]** 凭据。 |
| **[!DNL Port]:** | 的端口 [!DNL Query Service]. 必须使用端口 **80** 或 **5432** 连接 [!DNL Query Service]. |
| **[!DNL Database]** | 要访问的数据库。 使用Experience Platform的值 **[!UICONTROL 数据库]** 凭据： `prod:all`. |
| **[!DNL Authentication]:** | 您选择的用户身份验证方法。 建议您选择 [!DNL Username and Password] 下拉菜单的可用选项。 |
| **[!DNL Username]** | 这是您的平台组织ID。 使用Experience Platform的值 **[!UICONTROL 用户名]** 凭据。 该ID的格式为 `ORG_ID@AdobeOrg`. |
| **[!DNL Password]** | 此字母数字字符串是您的Experience Platform **[!UICONTROL 密码]** 凭据。 如果要使用未过期的凭据，此值是 `technicalAccountID` 和 `credential` 在配置JSON文件中下载。 密码值采用以下形式：{technicalAccountId}:{credential}。 用于未过期凭据的配置JSON文件是在初始化期间一次性下载，Adobe不会保留的副本。 |

有关查找用户名、密码和登录凭据的详细信息，请阅读 [凭据指南](../ui/credentials.md). 要查找您的凭据，请登录到 [!DNL Platform]，然后选择 **[!UICONTROL 查询]**，后跟 **[!UICONTROL 凭据]**.

确保已检查 **[!UICONTROL 需要SSL]** 框中，选择是否在尝试连接之前。 请参阅 [SSL模式文档](./ssl-modes.md) 了解对与Adobe Experience Platform查询服务的第三方连接的SSL支持。

>[!IMPORTANT]
>
>可以对第三方BI工具中的嵌套数据结构进行扁平化处理，以提高其可用性，并减少检索、分析、转换和报告数据所需的工作量。 请参阅[`FLATTEN` 功能](../best-practices/flatten-nested-data.md) 有关在连接到数据库时如何激活此设置的说明。

填写所有凭据后，确认设置以继续。 您现在已连接到Adobe Experience Platform。

## 后续步骤

现在你已经连接了 [!DNL Query Service]，您可以使用 [!DNL Tableau] 来编写查询。 有关如何编写和运行查询的详细信息，请阅读 [运行查询](../best-practices/writing-queries.md).
