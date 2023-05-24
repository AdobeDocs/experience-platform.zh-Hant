---
keywords: Experience Platform；首頁；熱門主題；架構；架構；XDM；欄位；架構；架構；應用程式；資料類型；資料類型；
solution: Experience Platform
title: 應用程式資料類型
description: 本文檔概述了應用程式體驗資料模型(XDM)資料類型。
exl-id: ac7d6761-7b58-4e0d-85e7-6f157fb2eea5
source-git-commit: 983682489e2c0e70069dbf495ab90fc9555aae2d
workflow-type: tm+mt
source-wordcount: '439'
ht-degree: 1%

---

# [!UICONTROL 應用程式] 資料類型

[!UICONTROL 應用程式] 是標準的體驗資料模型(XDM)資料類型，它描述與應用程式生成的交互相關的詳細資訊。 應用程式是指軟體體驗，如可由最終用戶安裝、運行、關閉或卸載的移動或案頭應用程式。 此資料類型的屬性不用於描述代理，如聊天機、基於瀏覽器的插件或不適用於應用程式的其他體驗。

<img src="../images/data-types/application.PNG" width="500" /><br />

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `applicationCloses` | [[!UICONTROL 度量]](./measure.md) | 描述有關終止應用程式的詳細資訊。 |
| `crashes` | [[!UICONTROL 度量]](./measure.md) | 當應用程式未按預期退出時，此屬性將觸發。 |
| `featureUsages` | [[!UICONTROL 度量]](./measure.md) | 描述激活正在測量的應用程式功能時的任何資料。 |
| `firstLaunches` | [[!UICONTROL 度量]](./measure.md) | 包含首次啟動時的資料。 此屬性在安裝後首次啟動時觸發。 |
| `installs` | [[!UICONTROL 度量]](./measure.md) | 當特定安裝事件可用時，記錄在設備上安裝應用程式。 |
| `launches` | [[!UICONTROL 度量]](./measure.md) | 描述與應用程式啟動關聯的值。 每次運行時都會觸發此操作，包括超出會話超時時的崩潰、安裝和從後台恢復。 |
| `upgrades` | [[!UICONTROL 度量]](./measure.md) | 包含有關升級以前已安裝的應用程式的資料。 升級後首次啟動時觸發此按鈕。 |
| `id` | 字串 | 應用程式的唯一標識符。 |
| `name` | 字串 | 應用程式的名稱。 |
| `userPerspective` | 字串 | 事件發生時用戶與應用或品牌之間的透視關係或物理關係。 瞭解用戶對應用的視角有助於準確生成會話，因為大多數時間您不希望包括這些會話 `background` 和 `detached` 事件作為「活動」會話的一部分。 此屬性的值必須等於下面列出的枚舉值之一。 <li> `foreground`:用戶和應用程式正在直接交互。 </li> <li> `background`:應用程式和用戶之間正在間接交互。 例如，應用程式可以測量值並在螢幕被鎖定或前景中正在使用另一個應用程式時刷新。  </li> <li> `detached`:Detached表示事件與應用相關，但不直接來自應用，例如從外部系統發送電子郵件或推送通知。 |
| `version` | 字串 | 應用程式的版本。 |

{style="table-layout:auto"}

有關資料類型的詳細資訊，請參閱公共XDM儲存庫：

* [填充示例](https://github.com/adobe/xdm/blob/master/components/datatypes/channels/application.example.1.json)
* [完整架構](https://github.com/adobe/xdm/blob/master/components/datatypes/channels/application.schema.json)
