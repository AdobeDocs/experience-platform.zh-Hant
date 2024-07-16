---
keywords: Experience Platform；首頁；熱門主題；結構；結構；XDM；欄位；結構；應用程式；資料型別；資料型別；
solution: Experience Platform
title: 應用程式資料型別
description: 瞭解應用程式體驗資料模型(XDM)資料型別。
exl-id: ac7d6761-7b58-4e0d-85e7-6f157fb2eea5
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '416'
ht-degree: 1%

---

# [!UICONTROL 應用程式]資料型別

[!UICONTROL 應用程式]是標準的體驗資料模型(XDM)資料型別，可描述與應用程式產生的互動相關的詳細資訊。 應用程式是指軟體體驗，例如可由一般使用者安裝、執行、關閉或解除安裝的行動或案頭應用程式。 此資料型別的屬性並非旨在說明聊天機器人、瀏覽器外掛程式等代理程式，或其他不適用於應用程式的體驗。

<img src="../images/data-types/application.PNG" width="500" /><br />

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `applicationCloses` | [[!UICONTROL 量值]](./measure.md) | 說明應用程式終止的詳細資訊。 |
| `crashes` | [[!UICONTROL 量值]](./measure.md) | 當應用程式未如預期結束時，就會觸發此屬性。 |
| `featureUsages` | [[!UICONTROL 量值]](./measure.md) | 說明啟動所測量之應用程式功能所產生的任何資料。 |
| `firstLaunches` | [[!UICONTROL 量值]](./measure.md) | 包含第一次啟動的資料。 此屬性會在安裝後的首次啟動時觸發。 |
| `installs` | [[!UICONTROL 量值]](./measure.md) | 在有特定安裝事件可用時，記錄應用程式在裝置上的安裝。 |
| `launches` | [[!UICONTROL 量值]](./measure.md) | 說明與應用程式啟動相關的值。 每次執行時都會觸發此動作，包括當機、安裝，以及超過工作階段逾時時從背景繼續。 |
| `upgrades` | [[!UICONTROL 量值]](./measure.md) | 包含有關升級先前已安裝的應用程式的資料。 這會在升級後的首次啟動時觸發。 |
| `id` | 字串 | 適用於應用程式的唯一識別碼。 |
| `name` | 字串 | 應用程式的名稱。 |
| `userPerspective` | 字串 | 事件發生時使用者與應用程式或品牌之間的觀點或實體關係。 瞭解使用者相對於應用程式的觀點，有助於準確產生工作階段，因為您大部分時間不想將`background`和`detached`事件包含在「作用中」工作階段中。 此屬性的值必須等於下列其中一個列舉值。 <li> `foreground`：使用者和應用程式直接互動。 </li> <li> `background`：應用程式和使用者正在間接互相互動。 例如，應用程式可測量值，然後在熒幕鎖定或前景中使用另一個應用程式時重新整理。  </li> <li> `detached`： Detached表示事件與應用程式相關，但並非直接來自應用程式，例如從外部系統傳送電子郵件或推播通知。 |
| `version` | 字串 | 應用程式的版本。 |

{style="table-layout:auto"}

如需資料型別的詳細資訊，請參閱公用XDM存放庫：

* [已填入範例](https://github.com/adobe/xdm/blob/master/components/datatypes/channels/application.example.1.json)
* [完整結構描述](https://github.com/adobe/xdm/blob/master/components/datatypes/channels/application.schema.json)
