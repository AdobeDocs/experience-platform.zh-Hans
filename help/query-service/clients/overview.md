---
keywords: Experience Platform；主页；热门主题；查询服务；查询服务；连接；连接到查询服务；aqua data Studio；Aqua Data Studio；查找器；Postico；postico；Power BI；power bi；psql；rstudio；PSQL；RStudio；Tableau；tableau；
solution: Experience Platform
title: 将客户端连接到查询服务
description: 本文档介绍如何从各种桌面客户端应用程序连接到查询服务，以及如何验证这些连接。
exl-id: 2ba20179-5adb-4259-a120-231a40e78054
source-git-commit: 778c65c6310ed4a627be0fd3ae076784cfc8495b
workflow-type: tm+mt
source-wordcount: '229'
ht-degree: 0%

---

# 将客户端连接到 [!DNL Query Service]

本节介绍如何连接到 [!DNL Query Service] 以及如何验证这些连接。 [!DNL Query Service] 使用 [!DNL PostgreSQL] 协议，因此本节中的说明将介绍如何使用 [!DNL PostgreSQL] 用于连接和编写查询的工具和驱动程序。

>[!IMPORTANT]
>
>查询服务Interactive Postgres API的生产环境上的TLS/SSL证书已于2024年1月24日星期三更新。<br>尽管这是年度要求，但这次链中的根证书也发生了变化，因为Adobe的TLS/SSL证书提供商更新了其证书层次结构。 如果某些Postgres客户端的证书颁发机构列表缺少根证书，这可能会影响这些客户端。 例如，PSQL CLI客户端可能需要将根证书添加到显式文件中 `~/postgresql/root.crt`，否则可能会导致错误。 例如：`psql: error: SSL error: certificate verify failed`。请参阅 [PostgreSQL官方文档](https://www.postgresql.org/docs/current/libpq-ssl.html#LIBQ-SSL-CERTIFICATES) 以了解有关此问题的更多信息。<br>可以从中下载要添加的根证书 [https://cacerts.digicert.com/DigiCertGlobalRootG2.crt.pem](https://cacerts.digicert.com/DigiCertGlobalRootG2.crt.pem).

为以下客户端提供了说明：

- [[!DNL Aqua Data Studio]](./aqua-data-studio.md)
- [[!DNL DbVisualizer]](./dbvisulaizer.md)
- [[!DNL Looker]](./looker.md)
- [[!DNL Postico (Mac)]](./postico.md)
- [[!DNL Power BI (PC)]](./power-bi.md)
- [[!DNL PSQL]](./psql.md)
- [[!DNL RStudio]](./rstudio.md)
- [[!DNL Tableau]](./tableau.md)
