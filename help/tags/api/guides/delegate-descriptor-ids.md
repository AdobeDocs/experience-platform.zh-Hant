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

使用Adobe Experience Platform中的標籤時，擴充功能會提供您可部署在網站上的所有功能。 每個擴充功能提供的功能由擴充功能開發人員定義。 部署擴充功能時，會以[擴充功能套件](../endpoints/extension-packages.md)的形式，將擴充功能與其各種功能整合。 開發人員新增至擴充功能套件的功能會視為該套件的「代理人」。

擴充功能套件內的每個委派都會獲得唯一的委派描述項ID。 特定資源的委派描述項ID會告知系統它是什麼資源，以及它屬於哪個擴充功能套件。

## 語法

委派描述項ID包含三個由雙冒號字元(`::`)連結的字串，分別代表擴充套件名稱、委派型別和委派名稱。 這些字串的撰寫方式可供使用者讀取，並在內嵌擴充功能套件時由系統自動產生和指派。

例如，如果名為`example-package`的擴充功能套件有名為`custom-code`的動作，該動作會有下列委派描述項識別碼： `example-package::actions::custom-code`。

## 在適用的資源上使用委派描述項ID

在API中定義規則元件（事件、條件和動作）和資料元素時，委派描述項ID是重要的瞭解事項。 以下各節概述這些ID對每個資源如何發揮作用。

### 規則元件

[規則元件](../endpoints/rule-components.md)必須與屬於擴充功能套件的事件、條件或動作相關聯。 這代表規則元件的「型別」，因為它與整體規則（事件、條件或動作）的邏輯相關。 因此，建立規則元件時，必須提供委派描述項ID以指出應將規則元件與哪個事件、條件或動作相關聯。

例如，若要建立以擴充功能套件`example-package`中的`click`事件為基礎的事件規則元件，規則元件將使用下列`delegate_descriptor_id`值： `example-package::events::click`。

如需詳細資訊，請參閱[建立規則元件](../endpoints/rule-components.md#create)的相關章節。

### 資料元素

[資料元素](../endpoints/data-elements.md)必須在第一次建立時與擴充功能套件關聯，因為每個擴充功能套件都會定義其委派資料元素的相容型別，以及預期行為。

例如，若要建立使用擴充套件`example-package`所定義之`cookie`型別的資料元素，資料元素將使用下列`delegate_descriptor_id`值： `example-package::dataElements::cookie`。

如需詳細資訊，請參閱[建立資料元素](../endpoints/data-elements.md#create)的相關章節。

### 擴充功能

[擴充功能](../endpoints/extensions.md)在第一次建立時自動與擴充功能套件建立關聯，並在擴充功能的`relationships`物件中呈現。 如果您的擴充功能需要自訂設定，則它也需要委派描述項ID。

>[!NOTE]
>
>不需要自訂設定的擴充功能不需要委派描述項ID。

例如，若要將委派描述項ID新增至屬於擴充功能套件`example-package`的擴充功能，擴充功能將使用下列`delegate_descriptor_id`值： `example-package::extensionConfiguration::config`。

如需詳細資訊，請參閱[建立擴充功能](../endpoints/extensions.md#create)的指南。
