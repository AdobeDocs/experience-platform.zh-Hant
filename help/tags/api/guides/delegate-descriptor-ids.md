---
title: 委託描述符ID
description: 瞭解有關Reactor API中委託描述符ID的資訊，以及它們如何將資源與擴展連結。
exl-id: 2c2b9b31-0618-4b93-97ec-0798fc06aac0
source-git-commit: a8b0282004dd57096dfc63a9adb82ad70d37495d
workflow-type: tm+mt
source-wordcount: '501'
ht-degree: 1%

---

# 委託描述符ID

在Adobe Experience Platform使用標籤時，您可以在站點上部署的所有功能都由擴展提供。 每個擴展提供的功能由擴展開發者定義。 部署擴展時，它會與其各種功能捆綁在一起， [擴展包](../endpoints/extension-packages.md)。 開發人員添加到擴展包的功能被視為該包的「委派」。

擴展包內的每個委託都被賦予唯一的委託描述符ID。 特定資源的委託描述符ID將告訴系統它屬於哪種資源及其屬於哪個擴展包。

## 語法

委託描述符ID由三個由雙冒號字元聯接的字串組成(`::`)，分別表示擴展包名稱、委託類型和委託名稱。 這些字串被構成為人可讀的，並且當接收擴展包時由系統自動生成和分配。

例如，如果名為 `example-package` 具有名為 `custom-code`，該操作將具有以下委託描述符ID: `example-package::actions::custom-code`。

## 在適用資源上使用委託描述符ID

在定義API中的規則元件（事件、條件和操作）和資料元素時，委派描述符ID非常重要。 以下各節概述了這些ID如何為每個資源發揮作用。

### 規則元件

A [規則元件](../endpoints/rule-components.md) 必須與屬於擴展包的事件、條件或操作關聯。 這表示規則元件的「類型」，因為它與整個規則（事件、條件或操作）的邏輯相關。 因此，在建立規則元件時，必須提供委託描述符ID以指示規則元件應與哪個事件、條件或操作關聯。

例如，建立基於 `click` 擴展包中的事件 `example-package`，規則元件將使用以下 `delegate_descriptor_id` 值： `example-package::events::click`。

請參閱 [建立規則元件](../endpoints/rule-components.md#create) 的子菜單。

### 資料元素

A [資料元](../endpoints/data-elements.md) 首次建立擴展包時，必須與擴展包關聯，因為每個擴展包都為其委託資料元素定義了相容類型以及它們的預期行為。

例如，建立使用 `cookie` 由擴展包定義的類型 `example-package`，資料元素將使用以下 `delegate_descriptor_id` 值： `example-package::dataElements::cookie`。

請參閱 [建立資料元素](../endpoints/data-elements.md#create) 的子菜單。

### 擴充功能

安 [擴展](../endpoints/extensions.md) 在首次建立擴展包時自動與擴展包關聯，並在擴展包中表示 `relationships` 的雙曲餘切值。 如果您的擴展需要自定義設定，則還需要委託描述符ID。

>[!NOTE]
>
>不需要自定義設定的擴展不需要委託描述符ID。

例如，要向屬於擴展包的擴展添加委託描述符ID `example-package`，擴展將使用以下 `delegate_descriptor_id` 值： `example-package::extensionConfiguration::config`。

請參閱上的指南 [建立擴展](../endpoints/extensions.md#create) 的子菜單。
