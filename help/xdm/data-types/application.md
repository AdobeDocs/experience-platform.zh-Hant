---
keywords: Experience Platform；首頁；熱門主題；結構；結構； XDM；欄位；結構；結構；應用程式；資料類型；資料類型；
solution: Experience Platform
title: 應用程式資料類型
description: 本檔案概述Application Experience Data Model(XDM)資料類型。
exl-id: ac7d6761-7b58-4e0d-85e7-6f157fb2eea5
source-git-commit: 983682489e2c0e70069dbf495ab90fc9555aae2d
workflow-type: tm+mt
source-wordcount: '439'
ht-degree: 1%

---

# [!UICONTROL 應用程式] 資料類型

[!UICONTROL 應用程式] 是標準的Experience Data Model(XDM)資料類型，可說明與應用程式產生的互動相關的詳細資訊。 應用程式是指軟體體驗，例如可由最終用戶安裝、運行、關閉或卸載的移動或案頭應用程式。 此資料類型的屬性不是用於描述聊天機器人、基於瀏覽器的插件或不適用於應用程式的其他體驗等代理。

<img src="../images/data-types/application.PNG" width="500" /><br />

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `applicationCloses` | [[!UICONTROL 測量]](./measure.md) | 說明終止應用程式的詳細資訊。 |
| `crashes` | [[!UICONTROL 測量]](./measure.md) | 當應用程式未如預期退出時，此屬性便會觸發。 |
| `featureUsages` | [[!UICONTROL 測量]](./measure.md) | 說明啟動要測量的應用程式功能時的任何資料。 |
| `firstLaunches` | [[!UICONTROL 測量]](./measure.md) | 包含首次啟動的資料。 此屬性會在安裝後首次啟動時觸發。 |
| `installs` | [[!UICONTROL 測量]](./measure.md) | 當特定安裝事件可用時，記錄在設備上安裝應用程式的情況。 |
| `launches` | [[!UICONTROL 測量]](./measure.md) | 說明與啟動應用程式相關聯的值。 每次執行時都會觸發此動作，包括當機、安裝和在超過工作階段逾時時從背景恢復。 |
| `upgrades` | [[!UICONTROL 測量]](./measure.md) | 包含先前已安裝之應用程式升級的資料。 這會在升級後的首次啟動時觸發。 |
| `id` | 字串 | 應用程式的唯一識別碼。 |
| `name` | 字串 | 應用程式的名稱。 |
| `userPerspective` | 字串 | 事件發生時，使用者與應用程式或品牌之間的透視或實體關係。 了解使用者對應用程式的看法，有助於在您不想納入的大多數時間內，準確產生工作階段 `background` 和 `detached` 事件作為「作用中」工作階段的一部分。 此屬性的值必須等於下列列舉值之一。 <li> `foreground`:使用者和應用程式會直接彼此互動。 </li> <li> `background`:應用程式和使用者間接互動。 例如，應用程式可測量值並在畫面鎖定或前景中使用另一個應用程式時重新整理。  </li> <li> `detached`:分離表示事件與應用程式相關，但並非直接來自應用程式，例如從外部系統傳送電子郵件或推播通知。 |
| `version` | 字串 | 應用程式的版本。 |

{style="table-layout:auto"}

如需資料類型的詳細資訊，請參閱公用XDM存放庫：

* [填入範例](https://github.com/adobe/xdm/blob/master/components/datatypes/channels/application.example.1.json)
* [完整結構](https://github.com/adobe/xdm/blob/master/components/datatypes/channels/application.schema.json)
