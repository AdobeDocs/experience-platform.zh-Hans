---
keywords: IP地址、IP范围、允许列表目标、允许列表
title: '云存储目标的IP地址允许列表 '
type: Documentation
description: 本页提供可添加到允许列表的IP范围，以将Experience Platform数据安全地从SFTP服务器、Amazon S3或Azure Blob存储导出。
exl-id: 0b8086aa-786e-4244-b2a5-a3f57ad59a8b
translation-type: tm+mt
source-git-commit: ac62ebcc7b00a96f718a3c39725bcf21ce3d56cf
workflow-type: tm+mt
source-wordcount: '212'
ht-degree: 0%

---

# 云存储目标{#ip-address-allow-list}的IP地址允许列表

>[!IMPORTANT]
>
> * Adobe建议您将此页面加入书签，并每三个月重新访问一次，以检查最新的IP地址。 Adobe不提供新IP范围的通知。
> * 虽然Adobe支持向SFTP服务器导出存储，但建议的用于导出数据的云位置是[!DNL Amazon S3]和[!DNL Azure Blob]。


## 概述 {#overview}

本页提供可添加到允许列表的IP范围，以安全地将Experience Platform数据从导出到您的[SFTP服务器](./sftp.md)、[Amazon S3](./amazon-s3.md)或[Azure Blob](./azure-blob.md)存储。

您可以通过网络防火墙定义网络访问控制。 通过指定适当的IP范围，您可以允许数据传输服务的通信。

Adobe建议您在使用云存储目标连接之前，向允许列表添加以下IP范围。 如果无法向允许列表添加区域特定的IP范围，在使用云存储目标连接时可能会导致错误或性能不佳。

## 所有客户都需要

* `52.247.108.70`

## 美国客户

* `52.252.71.64/29`

## EMEA客户

* `51.137.8.208/29`

## APAC客户

* `20.53.201.168/29`
