---
title: 委派描述符ID
description: 了解Reactor API中的委派描述元ID，以及它們如何將資源與擴充功能連結。
source-git-commit: 6a1728bd995137a7cd6dc79313762ae6e665d416
workflow-type: tm+mt
source-wordcount: '501'
ht-degree: 1%

---

# 委派描述符ID

在Adobe Experience Platform中使用標籤時，您可在網站上部署的所有功能都由擴充功能提供。 每個擴充功能提供的功能由擴充功能開發人員定義。 部署擴充功能時，會以[擴充功能套件](../endpoints/extension-packages.md)的形式與其各種功能搭配。 開發人員新增至擴充功能套件的功能視為該套件的「委派」。

擴充功能套件內的每個委派都獲得唯一的委派描述元ID。 特定資源的委派描述符ID告知系統它是何種資源及其所屬的擴展包。

## 語法

委派描述符ID由三個由雙冒號字元(`::`)連結的字串組成，分別代表擴充功能套件名稱、委派類型和委派名稱。 這些字串是人類看得懂的，且會在擷取擴充功能套件時由系統自動產生及指派。

例如，如果名為`example-package`的擴展包具有名為`custom-code`的操作，則該操作將具有以下委託描述符ID:`example-package::actions::custom-code`。

## 在適用資源上使用委派描述符ID

委派描述元ID對於在API中定義規則元件（事件、條件和動作）和資料元素時務必要了解。 以下各節將說明這些ID在每個資源中如何發揮作用。

### 規則元件

[規則元件](../endpoints/rule-components.md)必須與屬於擴充功能套件的事件、條件或動作相關聯。 這代表規則元件的「類型」，因為它與整體規則（事件、條件或動作）的邏輯相關。 因此，在建立規則元件時，必須提供委派描述符ID以指出規則元件應與哪個事件、條件或動作相關聯。

例如，若要建立以擴充功能套件`example-package`中的`click`事件為基礎的事件規則元件，規則元件將使用下列`delegate_descriptor_id`值：`example-package::events::click`。

如需詳細資訊，請參閱關於[建立規則元件](../endpoints/rule-components.md#create)的區段。

### 資料元素

[資料元素](../endpoints/data-elements.md)在首次建立時必須與擴充功能套件相關聯，因為每個擴充功能套件都定義其委派資料元素的相容類型及其預期行為。

例如，若要建立使用擴充功能套件`example-package`所定義之`cookie`類型的資料元素，資料元素將使用下列`delegate_descriptor_id`值：`example-package::dataElements::cookie`。

如需詳細資訊，請參閱關於[建立資料元素](../endpoints/data-elements.md#create)的區段。

### 擴充功能

[擴充功能](../endpoints/extensions.md)在首次建立時會自動與擴充功能套件相關聯，並在擴充功能的`relationships`物件中呈現。 如果您的擴充功能需要自訂設定，則也需要委派描述元ID。

>[!NOTE]
>
>不需要自訂設定的擴充功能不需要委派描述元ID。

例如，要將委派描述符ID添加到屬於擴展包`example-package`的擴展中，該擴展將使用以下`delegate_descriptor_id`值：`example-package::extensionConfiguration::config`。

如需詳細資訊，請參閱[建立擴充功能](../endpoints/extensions.md#create)的指南。