---
keywords: IP地址， IP范围，允许列表，允许列表
title: 列入允许列表查询服务的IP地址
description: 此页提供了可添加到允许列表的IP范围。
exl-id: f6745e0f-d387-45f2-9f72-054e721016ff
source-git-commit: 308d07cf0c3b4096ca934a9008a13bf425dc30b6
workflow-type: tm+mt
source-wordcount: '175'
ht-degree: 2%

---

# IP地址允许列表 {#ip-address-allow-list}

>[!IMPORTANT]
>
> * Adobe建议您将此页面加入书签，每三个月重新访问一次，以检查最新IP地址。 Adobe不提供新IP范围的通知。
> * 虽然Adobe支持将数据导出到SFTP服务器，但建议用于导出数据的云存储位置为 [!DNL Amazon S3] 和 [!DNL Azure Blob].

## 概述 {#overview}

列入允许列表本页提供了可添加到Experience Platform的IP地址，以便安全地将数据从IP地址导出到IP地址。 [SFTP服务器](../destinations/catalog/cloud-storage/sftp.md).

您可以通过网络防火墙定义网络访问控制。 通过指定适当的IP范围，您可以允许数据传输服务的通信。

Adobe建议您将以下IP范围添加到允许列表，具体取决于您所在的区域。 未能将特定于区域的IP范围添加到允许列表可能会导致错误或性能不佳。

## VA7：美国和美洲客户 {#us-americas}

* 52.138.119.167

## NLD2：EMEA客户 {#emea}

* 51.124.70.4

## AUS5：APAC客户 {#apac}

* 20.193.36.37

## CAN2：加拿大客户 {#can2}

* 20.104.5.248
