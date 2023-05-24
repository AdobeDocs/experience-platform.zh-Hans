---
title: 財務帳戶資料型別
description: 本檔案提供財務帳戶XDM資料型別的概觀。
exl-id: badf9b20-d397-4b46-b045-19c69806fe8e
source-git-commit: f5df893260f0772ad54ccdb00d99ed8f328d35a9
workflow-type: tm+mt
source-wordcount: '103'
ht-degree: 5%

---

# [!UICONTROL 財務帳戶] 資料型別

[!UICONTROL 財務帳戶] 是標準的XDM資料型別，說明財務帳戶的詳細資訊，包括其型別、擁有者和目前餘額。

![](../images/data-types/financial-account.png)

| 属性 | 資料型別 | 描述 |
| --- | --- | --- |
| `currentAccountBalance` | [[!UICONTROL 货币]](./currency.md) | 帳戶的目前餘額。 |
| `financialAccountId` | [!UICONTROL 字符串] | 帳戶的唯一識別碼。 |
| `financialAccountName` | [!UICONTROL 字符串] | 指派給帳戶的名稱。 |
| `financialAccountType` | [!UICONTROL 字符串] | 財務帳戶的型別，例如支票、儲蓄或退休。 |

{style="table-layout:auto"}

如需資料型別的詳細資訊，請參閱 [公用XDM存放庫](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/financial-account.schema.json).
