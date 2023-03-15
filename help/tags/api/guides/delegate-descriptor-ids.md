---
title: 委派描述符ID
description: 了解Reactor API中的委派描述元ID，以及它們如何將資源與擴充功能連結。
exl-id: 2c2b9b31-0618-4b93-97ec-0798fc06aac0
source-git-commit: a8b0282004dd57096dfc63a9adb82ad70d37495d
workflow-type: tm+mt
source-wordcount: '501'
ht-degree: 1%

---

# 委派描述符ID

在Adobe Experience Platform中使用標籤時，您可在網站上部署的所有功能都由擴充功能提供。 每個擴充功能提供的功能由擴充功能開發人員定義。 部署擴充功能時，會以 [擴充功能套件](../endpoints/extension-packages.md). 開發人員新增至擴充功能套件的功能視為該套件的「委派」。

擴充功能套件內的每個委派都獲得唯一的委派描述元ID。 特定資源的委派描述符ID告知系統它是何種資源及其所屬的擴展包。

## 語法

委派描述符ID由三個字串組成，以雙冒號字元(`::`)，分別代表擴充功能套件名稱、委派類型和委派名稱。 這些字串是人類看得懂的，且會在擷取擴充功能套件時由系統自動產生及指派。

例如，如果擴充功能套件名為 `example-package` 已命名 `custom-code`，則該動作會有下列委派描述元ID: `example-package::actions::custom-code`.

## 在適用資源上使用委派描述符ID

委派描述元ID對於在API中定義規則元件（事件、條件和動作）和資料元素時務必要了解。 以下各節將說明這些ID在每個資源中如何發揮作用。

### 規則元件

A [規則元件](../endpoints/rule-components.md) 必須與屬於擴充功能套件的事件、條件或動作相關聯。 這代表規則元件的「類型」，因為它與整體規則（事件、條件或動作）的邏輯相關。 因此，在建立規則元件時，必須提供委派描述符ID以指出規則元件應與哪個事件、條件或動作相關聯。

例如，若要建立以 `click` 擴充功能套件中的事件 `example-package`，規則元件會使用下列 `delegate_descriptor_id` 值： `example-package::events::click`.

請參閱 [建立規則元件](../endpoints/rule-components.md#create) 以取得更多資訊。

### 資料元素

A [資料元素](../endpoints/data-elements.md) 必須在初次建立擴充功能套件時與其相關聯，因為每個擴充功能套件都會定義其委派資料元素的相容類型，以及其預期行為。

例如，若要建立使用 `cookie` 由擴充功能套件定義的類型 `example-package`，資料元素會使用下列 `delegate_descriptor_id` 值： `example-package::dataElements::cookie`.

請參閱 [建立資料元素](../endpoints/data-elements.md#create) 以取得更多資訊。

### 擴充功能

安 [擴充功能](../endpoints/extensions.md) 會在初次建立時自動與擴充功能套件建立關聯，並在擴充功能的中呈現 `relationships` 物件。 如果您的擴充功能需要自訂設定，則也需要委派描述元ID。

>[!NOTE]
>
>不需要自訂設定的擴充功能不需要委派描述元ID。

例如，要將委派描述符ID添加到屬於該擴展包的擴展 `example-package`，擴充功能會使用下列 `delegate_descriptor_id` 值： `example-package::extensionConfiguration::config`.

請參閱 [建立擴充功能](../endpoints/extensions.md#create) 以取得更多資訊。
