---
title: 擴充功能開發概述
description: 了解關於不同標記擴充功能類型的主要元件，以及 Adobe Experience Platform 中的擴充功能開發程序。
exl-id: b72df3df-f206-488d-a690-0f086973c5b6
source-git-commit: 8ded2aed32dffa4f0923fedac7baf798e68a9ec9
workflow-type: tm+mt
source-wordcount: '950'
ht-degree: 22%

---

# 擴充功能開發概述

>[!NOTE]
>
>Adobe Experience Platform Launch已經過品牌重塑，現在是Adobe Experience Platform中的一套資料收集技術。 因此，所有產品文件中出現了幾項術語變更。 如需術語變更的彙整參考資料，請參閱以下[文件](../term-updates.md)。

Adobe Experience Platform中標籤的主要目標之一，是建立開放的生態系統，讓Adobe以外的工程師可以在他們的網站和行動應用程式上公開其他功能。 這是透過標籤擴充功能來完成。 在標籤屬性上安裝擴充功能後，該擴充功能的功能就會供屬性的所有使用者使用。

本檔案概述擴充功能的主要元件，並提供進一步檔案的連結，以協助您進行擴充功能開發程式。

## 擴充功能結構

擴充功能由檔案目錄組成。具體而言，擴充功能包含資訊清單檔案、程式庫模組和檢視。

### 資訊清單檔案

資訊清單檔案([`extension.json`](./manifest.md))必須存在於根目錄中。 此檔案說明副檔名的組成以及某些檔案在目錄中的位置。 資訊清單的功能類似於 [`package.json`](https://docs.npmjs.com/files/package.json) 中的檔案 [npm](https://www.npmjs.com/) 專案。

### 程式庫模組

程式庫模組是描述不同物件的檔案 [元件](#components) 擴充功能提供的邏輯（換句話說，就是要在標籤執行階段程式庫內發出的邏輯）。 每個程式庫模組檔案的內容都必須遵循 [CommonJS模組標準](https://nodejs.org/api/modules.html#modules-commonjs-modules).

例如，如果您要建立名為「傳送信標」的動作型別，則必須要有一個檔案內含傳送信標的邏輯。 如果使用JavaScript，則可呼叫檔案 `sendBeacon.js`. 此檔案的內容將在標籤執行階段程式庫內發出。

您可以將程式庫模組檔案放在擴充功能目錄中的任何位置，但前提是您要說明它們在中的位置 `extension.json`.

### 檢視

檢視是可載入至的HTML檔案 [`iframe` 元素](https://developer.mozilla.org/zh-TW/docs/Web/HTML/Element/iframe) 標籤應用程式內，尤其是透過Platform UI和Data Collection UI。 檢視必須包含擴充功能提供的指令碼，並符合小型API，才能與應用程式通訊。

任何副檔名最重要的檢視檔案是其設定。 請參閱以下小節： [擴充功能組態](#configuration) 以取得詳細資訊。

您的檢視中並沒有可用程式庫的限制。換言之，您可以使用jQuery、Underscore、React、Angular、Bootstrap或其他。 不過，我們仍建議您讓擴充功能具有類似於UI的外觀。

建議您將所有檢視相關檔案 (HTML、CSS、JavaScript) 放在與程式庫模組檔案不同的單一子目錄中。在 `extension.json`，您可以說明此檢視子目錄的位置。 Platform會從其Web伺服器為此子目錄（且僅此子目錄）提供服務。

## 程式庫元件 {#components}

每個擴充功能會定義一組功能。 這些功能的實作方式為包含在 [資料庫](../ui/publishing/libraries.md) 部署至您的網站或應用程式的屬性。 程式庫是個別元件的集合，包括條件、動作、資料元素等。 每個程式庫元件都是一段可重複使用的程式碼（由擴充功能提供），會在標籤執行階段內發出。

根據您正在開發Web擴充功能或邊緣擴充功能，可用的元件型別及其使用案例會有所不同。 請參閱以下小節，概略瞭解每種擴充功能型別可用的元件。

### Web擴充功能的元件 {#web}

在 Web 擴充功能中，規則會透過事件觸發，接著在符合特定條件時執行特定動作。如需詳細資訊，請參閱 [Web 擴充功能中的模組流程](./web/flow.md)概述文件。

除了 [核心模組](./web/core.md) 由Adobe提供，您可以在Web擴充功能中定義下列程式庫元件：

* [事件](./web/event-types.md)
* [條件](./web/condition-types.md)
* [動作](./web/action-types.md)
* [資料元素](./web/data-element-types.md)
* [共用模組](./web/shared.md)

>[!NOTE]
>
>若要進一步瞭解在Web擴充功能中實作程式庫元件所需的格式，請參閱 [模組格式概觀](./web/format.md).

### 邊緣擴充功能的元件 {#edge}

邊緣擴充功能中，規則會透過條件檢查作業來觸發，接著在通過檢查後執行特定動作。請參閱以下文章的概觀： [edge擴充功能流程](./edge/flow.md) 以取得詳細資訊。

您可以在邊緣擴充功能中定義下列程式庫元件：

* [條件](./edge/condition-types.md)
* [動作](./edge/action-types.md)
* [資料元素](./edge/data-element-types.md)

>[!NOTE]
>
>若要進一步了解在邊緣擴充功能中實作程式庫模組所需的格式，請參閱[模組格式概述](./edge/format.md)。

## 擴充功能組態 {#configuration}

擴充功能組態是指擴充功能據以向使用者收集全域設定的方式。此設定包含一個檢視元件，該元件會以純物件的形式匯出和發出標籤執行階段程式庫中的設定。

例如，假設擴充功能允許使用者使用「傳送信標」動作傳送信標，且信標一律須包含帳戶ID。 擴充功能不應該在使用者每次設定「傳送信標」動作時詢問其帳戶ID，而是應該從擴充功能設定檢視中詢問一次帳戶ID。 每次要傳送信標時，「傳送信標」動作就會從擴充功能設定中提取帳戶ID，並將其新增至信標。

當使用者將擴充功能安裝至UI中的屬性時，他們會看到擴充功能組態檢視，使用者必須完成該檢視才能完成安裝。

若要深入瞭解，請參閱以下專案的指南： [擴充功能組態](./configuration.md).

## 提交擴充功能

擴充功能建置完成後，您可以提交擴充功能，以列在Platform的擴充功能目錄中。 請參閱 [擴充功能提交程式概觀](./submit/overview.md) 以取得詳細資訊。
