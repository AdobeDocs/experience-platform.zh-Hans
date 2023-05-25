---
keywords: IP地址、IP范围、允许列表允许列表目标、
title: 云存储目标的IP地址允许列表
type: Documentation
description: 此页提供了可添加到允许列表的IP范围，以便安全地将数据从Experience Platform导出到SFTP服务器、Amazon S3或Azure Blob存储。
exl-id: 0b8086aa-786e-4244-b2a5-a3f57ad59a8b
source-git-commit: c4d8ae6de2e1bbf23a25a66bde5dc88c13a13402
workflow-type: tm+mt
source-wordcount: '202'
ht-degree: 0%

---

# 允许列表云存储目标的IP地址 {#ip-address-allow-list}

>[!IMPORTANT]
>
> * Adobe建议您将此页加入书签，每三个月重新访问一次，以检查最新的IP地址。 Adobe不提供新IP范围的通知。
> * 虽然Adobe支持将数据导出到SFTP服务器，但建议用于导出数据的云存储位置为 [!DNL Amazon S3] 和 [!DNL Azure Blob].


## 概述 {#overview}

允许列表本页提供了可添加到IP范围的IP范围，以安全地将数据从Experience Platform导出到 [SFTP服务器](./sftp.md).

您可以通过网络防火墙定义网络访问控制。 通过指定适当的IP范围，您可以允许数据传输服务的通信。

Adobe允许列表建议您在使用Cloud Storage目标连接之前，将以下IP范围添加到。 允许列表在使用Cloud Storage目标连接时，如果未能将特定于地区的IP范围添加到，可能会导致错误或性能不佳。

## 所有客户均需要

* `52.247.108.70`

## 美国客户

* `52.252.71.64/29`

## EMEA客户

* `51.137.8.208/29`

## APAC客户

* `20.53.201.168/29`
