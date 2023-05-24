---
keywords: Experience Platform；首頁；熱門主題；結構描述；結構描述；XDM；欄位；結構描述；信標；互動細節；資料型別；資料型別；
solution: Experience Platform
title: 信標資料型別
description: 本檔案提供XDM個別設定檔類別的概觀。
exl-id: a3767c8d-a009-49b4-81a4-b084b6e5101a
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '250'
ht-degree: 3%

---

# [!UICONTROL Beacon] 資料型別

[!UICONTROL Beacon] 是標準的XDM資料型別，說明在行動裝置進入範圍內時，將身分資訊傳遞給行動應用程式的無線裝置。

<img src="../images/data-types/beacon.png" width="450" /><br />

| 属性 | 資料型別 | 描述 |
| --- | --- | --- |
| `beaconMajor` | 双精度 | 主要值會識別和區分1和65,535之間的群組值與不帶正負號的整數值。 |
| `beaconMinor` | 双精度 | 次要值會識別和區分1和65,535之間的個別值與不帶正負號的整數值。 |
| `proximity` | 字符串 | 與信標的預估距離。 請參閱 [附錄](#proximity) 以取得接受的值和定義。 |
| `proximityUUID` | 字符串 | 近似程度UUID （通用唯一識別碼）是一種特殊型別的識別碼，可用來將您網路中的信標與非您控制之網路中的所有其他信標區分開來。 近似程度UUID會設定為信標，以傳輸到範圍內的行動裝置，藉以識別組織的信標。 |

{style="table-layout:auto"}

如需資料型別的詳細資訊，請參閱公用XDM存放庫：

* [填入範例](https://github.com/adobe/xdm/blob/master/components/datatypes/deprecated/beacon-interaction-details.example.1.json)
* [完整結構描述](https://github.com/adobe/xdm/blob/master/components/datatypes/deprecated/beacon-interaction-details.schema.json)

## 附录

以下小節包含更多關於 [!UICONTROL Beacon] 資料型別。

## 近似程度的接受值 {#proximity}

下表概述下列專案的可接受值 `proximity` 及其相關涵義：

| 值 | 描述 |
| --- | --- |
| `immediate` | 幾公分以內。 |
| `near` | 距離不到10米。 |
| `far` | 10米以外。 |
| `unknown` | 無法判斷距離，可能是因為訊號太弱。 |
