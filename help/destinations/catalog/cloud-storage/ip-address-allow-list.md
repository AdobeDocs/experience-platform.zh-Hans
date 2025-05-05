---
title: 基于文件的云存储目标的IP地址允许列表
type: Documentation
description: 本页提供了可添加到允许列表的IP范围，以便安全地将数据从Experience Platform导出到云存储目标。
exl-id: 0b8086aa-786e-4244-b2a5-a3f57ad59a8b
source-git-commit: 7cf15550d7619e247052efc4d9b4c72c5d32641a
workflow-type: tm+mt
source-wordcount: '299'
ht-degree: 1%

---

# 列入允许列表基于文件的云存储目标的IP地址 {#ip-address-allow-list-cloud-storage}

>[!IMPORTANT]
>
> * Adobe建议您将此页面加入书签，每三个月重新访问一次，以检查最新IP地址。 Adobe不提供新IP范围的通知。
> * 虽然Adobe支持将数据导出到SFTP服务器，但建议用于导出数据的云存储位置为[!DNL Amazon S3]和[!DNL Azure Blob]。

## 适用性 {#applicability}

此页面上的IP范围信息适用于目标目录中的以下基于文件的云存储连接器：

* [[!UICONTROL Amazon S3]](./amazon-s3.md)
* [[!UICONTROL Google云存储]](google-cloud-storage.md)
* [SFTP](./sftp.md)

>[!IMPORTANT]
>
>以下基于文件的云存储目标不支持此页面上记录的IP范围： *Azure Blob、[!UICONTROL Azure Data Lake Storage Gen2]和[!UICONTROL Data Landing Zone]： 不支持*。

## 概述 {#overview}

列入允许列表本页提供了可添加到Experience Platform的IP范围，以便安全地将数据从Cloud导出到多个Cloud Storage目标。

您可以通过网络防火墙定义网络访问控制。 通过指定适当的IP范围，您可以允许数据传输服务的通信。

Adobe列入允许列表建议您在使用Cloud Storage目标连接之前，将以下IP范围添加到Storage 。 在使用Cloud Storage目标连接时，如果未能将特定于区域的IP范围添加到允许列表，可能会导致错误或性能下降。

## 所有客户均需要 {#all-customers}

* `52.247.108.70`

## 在AWS上运行的美国客户 {#aws}

以下IP范围适用于在Amazon Web Services (AWS)上运行的Experience Platform客户。 有关详细信息，请参阅[Experience Platform Multi-Cloud概述](../../../landing/multi-cloud.md)。

>[!NOTE]
>
>在AWS上运行、使用基于文件的目标将数据导出到Amazon S3的客户不支持此IP范围。

* `66.117.18.0/24`

## 美国客户 {#us-customers}

* `52.252.71.64/29`

## 加拿大客户 {#canada-customers}

* `20.220.135.16/29`

## EMEA客户 {#emea-customers}

* `51.137.8.208/29`

## 英国客户 {#uk-customers}

* `20.26.133.96/29`

## APAC客户 {#apac-customers}

* `20.53.201.168/29`
