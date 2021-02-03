---
keywords: Experience Platform;home；熱門主題；模式；模式；XDM;fields；模式；應用程式；datatype；資料類型；
solution: Experience Platform
title: 應用程式資料類型
topic: overview
description: 本檔案概述「應用程式體驗資料模型」(XDM)資料類型。
translation-type: tm+mt
source-git-commit: d282ea5526a05b28c6a82470eabf23e44d1fb420
workflow-type: tm+mt
source-wordcount: '438'
ht-degree: 1%

---


# [!UICONTROL 應用] 程式資料類型

[!UICONTROL 應用] 程式是標準的「體驗資料模型」(XDM)資料類型，可說明與應用程式產生的互動相關的詳細資訊。應用程式是指軟體體驗，例如可由使用者安裝、執行、關閉或解除安裝的行動或案頭應用程式。 此資料類型的屬性並非用來說明聊天機器人、瀏覽器外掛程式或其他不適用於應用程式的體驗等代理。

<img src="../images/data-types/application.PNG" width="500" /><br />

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `applicationCloses` | [[!UICONTROL 測量]](./measure.md) | 說明終止應用程式的詳細資訊。 |
| `crashes` | [[!UICONTROL 測量]](./measure.md) | 當應用程式未如預期退出時，就會觸發此屬性。 |
| `featureUsages` | [[!UICONTROL 測量]](./measure.md) | 說明啟動所測量之應用程式功能時的任何資料。 |
| `firstLaunches` | [[!UICONTROL 測量]](./measure.md) | 包含首次啟動的資料。 此屬性會在安裝後首次啟動時觸發。 |
| `installs` | [[!UICONTROL 測量]](./measure.md) | 當有特定安裝事件時，記錄在裝置上安裝應用程式的情形。 |
| `launches` | [[!UICONTROL 測量]](./measure.md) | 說明與啟動應用程式相關的值。 每次執行時都會觸發此動作，包括當作業逾時時，當發生當機、安裝和從背景繼續。 |
| `upgrades` | [[!UICONTROL 測量]](./measure.md) | 包含先前已安裝之應用程式升級的資料。 這會在升級後的首次啟動時觸發。 |
| `id` | 字串 | 應用程式的唯一識別碼。 |
| `name` | 字串 | 應用程式的名稱。 |
| `userPerspective` | 字串 | 當事件發生時，使用者與應用程式或品牌之間的透視或實際關係。 瞭解使用者對應用程式的看法有助於在您不想將`background`和`detached`事件納入「作用中」作業時，以大部分時間精確產生作業。 此屬性的值必須等於下列其中一個列舉值。 <li> `foreground`:使用者和應用程式會直接彼此互動。 </li> <li> `background`:應用程式和使用者間接互動。例如，應用程式可測量值並在畫面鎖定或前景中使用其他應用程式時重新整理。  </li> <li> `detached`:「分離」表示事件與應用程式相關，但不直接來自應用程式，例如從外部系統傳送電子郵件或推播通知。 |
| `version` | 字串 | 應用程式的版本。 |

有關資料類型的詳細資訊，請參閱公共XDM儲存庫：

* [填入的範例](https://github.com/adobe/xdm/blob/master/components/datatypes/channels/application.example.1.json)
* [完整架構](https://github.com/adobe/xdm/blob/master/components/datatypes/channels/application.schema.json)