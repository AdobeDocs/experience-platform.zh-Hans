---
keywords: Experience Platform；主页；热门主题；Tableau；Tableau；查询服务；查询服务；连接到查询服务；
solution: Experience Platform
title: 将 Tableau 连接到查询服务
description: 本文档介绍了将Tableau与Adobe Experience Platform查询服务连接的步骤。
exl-id: f380aacd-5091-41bc-97ca-593e0b1670fd
source-git-commit: 99cd69234006e6424be604556829b77236e92ad7
workflow-type: tm+mt
source-wordcount: '447'
ht-degree: 1%

---

# 连接 [!DNL Tableau] 查询服务

本文档提供了有关连接的信息 [!DNL Tableau] 使用Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> 本指南假定您已经有权访问 [!DNL Tableau] 并熟悉如何导航其界面。 有关以下内容的更多信息 [!DNL Tableau] 可在以下位置找到： [官方 [!DNL Tableau] 文档](https://help.tableau.com/current/pro/desktop/en-us/default.htm).

操作说明 [使用Tableau连接到PostgreSQL服务器](https://help.tableau.com/current/pro/desktop/en-us/examples_postgresql.htm) 详情请访问Tableau官方网站。 出现连接设置对话框后，在参数字段中输入您的Platform凭据以与Adobe Experience Platform连接。 下面列出了所需的连接参数。

| 连接参数 | 描述 |
|---|---|
| **[!DNL Server]** | SFTP存储位置的地址。 使用Experience Platform的值 **[!UICONTROL 主机]** 凭据。 |
| **[!DNL Port]:** | 的端口 [!DNL Query Service]. 必须使用端口 **80** 或 **5432** 以连接 [!DNL Query Service]. |
| **[!DNL Database]** | 要访问的数据库。 使用Experience Platform的值 **[!UICONTROL 数据库]** 凭据： `prod:all`. |
| **[!DNL Authentication]:** | 您选择的证明用户身份的方法。 建议您选择 [!DNL Username and Password] 从下拉菜单的可用选项中。 |
| **[!DNL Username]** | 这是您的Platform组织ID。 使用Experience Platform的值 **[!UICONTROL 用户名]** 凭据。 ID将采用以下格式 `ORG_ID@AdobeOrg`. |
| **[!DNL Password]** | 该字母数字字符串是您的Experience Platform **[!UICONTROL 密码]** 凭据。 如果要使用未过期的凭据，此值是以下项的连接参数： `technicalAccountID` 和 `credential` 在配置JSON文件中下载。 密码值采用以下形式： {technicalAccountId}：{credential}. 未过期凭据的配置JSON文件是在其初始化期间的一次性下载，该Adobe不保留的副本。 |

有关查找用户名、密码和登录凭据的详细信息，请阅读 [凭据指南](../ui/credentials.md). 要查找您的凭据，请登录 [!DNL Platform]，然后选择 **[!UICONTROL 查询]**，后接 **[!UICONTROL 凭据]**.

确保您已检查 **[!UICONTROL 需要SSL]** 方框，然后再尝试连接。 请参阅 [SSL模式文档](./ssl-modes.md) 了解到Adobe Experience Platform查询服务的第三方连接的SSL支持。

>[!IMPORTANT]
>
>第三方BI工具中的嵌套数据结构可以扁平化，以提高其可用性并减少检索、分析、转换和报告数据所需的工作量。 请参阅有关以下内容的文档[`FLATTEN` 特征](../key-concepts/flatten-nested-data.md) 以获取有关在连接到数据库时如何激活此设置的说明。

填写完您的所有凭据后，确认您的设置以继续。 您现在已与Adobe Experience Platform建立了连接。

## 后续步骤

现在您已连接到 [!DNL Query Service]，您可以使用 [!DNL Tableau] 以编写查询。 有关如何编写和运行查询的更多信息，请阅读以下指南： [正在运行查询](../best-practices/writing-queries.md).
