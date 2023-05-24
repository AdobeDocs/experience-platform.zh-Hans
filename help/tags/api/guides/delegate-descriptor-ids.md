---
title: 委派描述項ID
description: 瞭解Reactor API中的委派描述項ID，以及它們如何將資源與擴充功能連結。
exl-id: 2c2b9b31-0618-4b93-97ec-0798fc06aac0
source-git-commit: a8b0282004dd57096dfc63a9adb82ad70d37495d
workflow-type: tm+mt
source-wordcount: '501'
ht-degree: 1%

---

# 委派描述項ID

使用Adobe Experience Platform中的標籤時，擴充功能會提供您可以在網站上部署的所有功能。 擴充功能開發人員會定義每個擴充功能所提供的功能。 部署擴充功能時，會以「 」的形式，與其各種功能搭配 [擴充功能套件](../endpoints/extension-packages.md). 開發人員新增至擴充功能套件的功能會視為該套件的「委派」。

擴充功能套件內的每個委派都會獲得唯一的委派描述項ID。 特定資源的委派描述項ID會告訴系統它是什麼資源，以及它屬於哪個擴充功能套件。

## 语法

委派描述項ID包含三個以雙冒號字元(`::`)，分別代表擴充功能套件名稱、委派型別和委派名稱。 這些字串的構成方式可供讀取，並會在擷取擴充功能套件時，由系統自動產生和指派。

例如，如果擴充功能套件名為 `example-package` 具有名為的動作 `custom-code`，則該動作會有以下委派描述項ID： `example-package::actions::custom-code`.

## 在適用的資源上使用委派描述項ID

談到在API中定義規則元件（事件、條件和動作）和資料元素時，委派描述項ID務必要瞭解。 以下各節會概述這些ID如何對每個資源發揮作用。

### 规则组件

A [規則元件](../endpoints/rule-components.md) 必須與屬於擴充功能套件的事件、條件或動作相關聯。 這代表規則元件的「型別」，因為它與整體規則（事件、條件或動作）的邏輯相關。 因此，建立規則元件時，必須提供委派描述項ID以指出應將規則元件與哪個事件、條件或動作相關聯。

例如，若要建立事件規則元件，其基礎為 `click` 擴充功能套件中的事件 `example-package`，規則元件會使用下列 `delegate_descriptor_id` 值： `example-package::events::click`.

請參閱以下小節： [建立規則元件](../endpoints/rule-components.md#create) 以取得詳細資訊。

### 数据元素

A [資料元素](../endpoints/data-elements.md) 擴充功能套件首次建立時必須與擴充功能套件相關聯，因為每個擴充功能套件都會定義其委派資料元素的相容型別，以及其預期行為。

例如，若要建立使用 `cookie` 擴充功能套件所定義的型別 `example-package`，資料元素會使用下列專案 `delegate_descriptor_id` 值： `example-package::dataElements::cookie`.

請參閱以下小節： [建立資料元素](../endpoints/data-elements.md#create) 以取得詳細資訊。

### 扩展

一個 [擴充功能](../endpoints/extensions.md) 會在第一次建立擴充功能套件時自動與其建立關聯，並在擴充功能的 `relationships` 物件。 如果您的擴充功能需要自訂設定，則還需要委派描述項ID。

>[!NOTE]
>
>不需要自訂設定的擴充功能不需要委派描述項ID。

例如，若要將委派描述項ID新增至擴充功能套件的擴充功能 `example-package`，擴充功能會使用下列 `delegate_descriptor_id` 值： `example-package::extensionConfiguration::config`.

請參閱指南： [建立擴充功能](../endpoints/extensions.md#create) 以取得詳細資訊。
