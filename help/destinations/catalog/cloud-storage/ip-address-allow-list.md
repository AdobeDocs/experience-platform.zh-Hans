---
title: IP地址允许列表SFTP目标
type: Documentation
description: 本页提供了可添加到允许列表的IP范围，以便安全地将数据从Experience Platform导出到SFTP服务器。
exl-id: 0b8086aa-786e-4244-b2a5-a3f57ad59a8b
source-git-commit: 52186e03ba2a9d8b105d01ebfcd9be7666bfb6ff
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 0%

---

# 列入允许列表 SFTP目标的IP地址 {#ip-address-allow-list-sftp}

>[!IMPORTANT]
>
> * Adobe建议您将此页面加入书签，每三个月重新访问一次，以检查最新IP地址。 Adobe不提供新IP范围的通知。
> * 虽然Adobe支持将数据导出到SFTP服务器，但建议用于导出数据的云存储位置为 [!DNL Amazon S3] 和 [!DNL Azure Blob].

## 概述 {#overview}

列入允许列表本页提供了可添加到Experience Platform的IP范围，以便安全地将数据从IP范围导出到您的IP范围。 [SFTP服务器](./sftp.md).

您可以通过网络防火墙定义网络访问控制。 通过指定适当的IP范围，您可以允许数据传输服务的通信。

Adobe列入允许列表建议您在使用Cloud Storage目标连接之前，将以下IP范围添加到。 在使用Cloud Storage目标连接时，如果未能将特定于区域的IP范围添加到允许列表，可能会导致错误或性能下降。

## 所有客户均需要

* `52.247.108.70`

## 美国客户

* `52.252.71.64/29`

## 加拿大客户

* `20.220.135.16/29`

## EMEA客户

* `51.137.8.208/29`

## 英国客户

* `20.26.133.96/29`

## APAC客户

* `20.53.201.168/29`
