---
title: 擴充功能開發概述
description: 了解不同標籤擴充功能類型的主要元件，以及Adobe Experience Platform中的擴充功能開發程式。
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '948'
ht-degree: 18%

---

# 擴充功能開發概述

>[!NOTE]
>
>Adobe Experience Platform Launch在Adobe Experience Platform中已重新命名為一套資料收集技術。 因此，產品檔案中已推出數個術語變更。 有關術語更改的綜合參考，請參閱以下[document](../term-updates.md)。

Adobe Experience Platform中標籤的主要目標之一，是建立開放的生態系統，讓Adobe以外的工程師能夠在其網站和行動應用程式上公開其他功能。 這可透過標籤擴充功能來完成。 將擴充功能安裝在標籤屬性上後，該擴充功能的功能便可供屬性的所有使用者使用。

本檔案概述擴充功能的主要元件，並提供進一步檔案的連結，以協助您了解擴充功能的開發流程。

## 擴充功能結構

擴充功能由檔案目錄組成。具體而言，擴充功能包含資訊清單檔案、程式庫模組和檢視。

### 資訊清單檔案

清單檔案([`extension.json`](./manifest.md))必須位於根目錄。 此檔案說明擴充功能的組成，以及目錄中某些檔案的位置。 資訊清單的功能與[npm](https://www.npmjs.com/)專案中的[`package.json`](https://docs.npmjs.com/files/package.json)檔案類似。

### 程式庫模組

程式庫模組是描述擴充功能提供之不同[元件](#components)的檔案（亦即要在標籤執行階段程式庫內發出的邏輯）。 每個程式庫模組檔案的內容必須遵循[CommonJS模組標準](http://wiki.commonjs.org/wiki/Modules/1.1.1)。

例如，如果您要建置稱為「傳送信標」的動作類型，則必須有包含傳送信標之邏輯的檔案。 如果使用JavaScript，則檔案可稱為`sendBeacon.js`。 此檔案的內容將在標籤執行階段程式庫內發出。

只要您在`extension.json`中說明程式庫模組的位置，您就可以將程式庫模組檔案放在擴充功能目錄中所需的位置。

### 檢視

檢視是HTML檔案，可載入至標籤應用程式內的[`iframe`元素](https://developer.mozilla.org/zh-TW/docs/Web/HTML/Element/iframe)中，尤其是透過資料收集UI。 檢視必須包含擴充功能提供的指令碼，並符合小型API，才能與應用程式通訊。

任何擴充功能最重要的檢視檔案都是其設定。 如需詳細資訊，請參閱[擴充功能組態](#configuration)的相關章節。

您的檢視中並沒有可用程式庫的限制。換言之，您可以使用jQuery、Underscore、React、Angular、Bootstrap或其他。 不過，建議您讓擴充功能的外觀與資料收集UI類似。

建議您將所有檢視相關檔案 (HTML、CSS、JavaScript) 放在與程式庫模組檔案不同的單一子目錄中。在`extension.json`中，您可以說明此檢視子目錄的位置。 然後，Platform會從其Web伺服器提供此子目錄（且僅限此子目錄）。

## 程式庫元件 {#components}

每個擴充功能都定義一組功能。 這些功能是透過包含在部署至您網站或應用程式的[library](../ui/publishing/libraries.md)中而實作。 程式庫是個別元件的集合，包括條件、動作、資料元素等。 每個程式庫元件都是一段可重複使用的程式碼（由擴充功能提供），會在標籤執行階段內發出。

根據您是開發網頁擴充功能還是邊緣擴充功能，可用的元件類型和使用案例會有所不同。 請參閱下方的子區段，概略了解每種擴充功能類型可使用的元件。

### 網頁擴充功能的元件 {#web}

在 Web 擴充功能中，規則會透過事件觸發，接著在符合特定條件時執行特定動作。如需詳細資訊，請參閱 [Web 擴充功能中的模組流程](./web/flow.md)概述文件。

除了Adobe提供的[核心模組](./web/core.md)之外，您還可以在網頁擴充功能中定義下列程式庫元件：

* [事件](./web/event-types.md)
* [條件](./web/condition-types.md)
* [動作](./web/action-types.md)
* [資料元素](./web/data-element-types.md)
* [共用模組](./web/shared.md)

>[!NOTE]
>
>如需在網頁擴充功能中實作程式庫元件所需格式的詳細資訊，請參閱[模組格式概述](./web/format.md)。

### 邊緣擴充功能的元件 {#edge}

邊緣擴充功能中，規則會透過條件檢查作業來觸發，接著在通過檢查後執行特定動作。如需詳細資訊，請參閱[邊緣擴充功能流程](./edge/flow.md)上的概觀。

您可以在邊緣擴充功能中定義下列程式庫元件：

* [條件](./edge/condition-types.md)
* [動作](./edge/action-types.md)
* [資料元素](./edge/data-element-types.md)

>[!NOTE]
>
>若要進一步了解在邊緣擴充功能中實作程式庫模組所需的格式，請參閱[模組格式概述](./edge/format.md)。

## 擴充功能組態 {#configuration}

擴充功能組態是指擴充功能據以向使用者收集全域設定的方式。此設定包含一個檢視元件，該元件會匯出並發出標籤執行階段程式庫內的設定，作為純物件。

例如，假設擴充功能允許使用者使用「傳送信標」動作來傳送信標，且信標一律必須包含帳戶ID。 擴充功能應從擴充功能組態檢視中要求一次帳戶ID，而非在每次設定「傳送信標」動作時都要求使用者提供帳戶ID。 每次傳送信標時，「傳送信標」動作都可從擴充功能設定中提取帳戶ID，並將其新增至信標。

當使用者在UI中將擴充功能安裝至屬性時，會顯示擴充功能組態檢視，使用者必須完成此檢視才能完成安裝。

若要深入了解，請參閱[擴充功能組態](./configuration.md)的指南。

## 提交擴充功能

完成擴充功能的建置後，您就可以提交該擴充功能，以列在Platform的擴充功能目錄中。 如需詳細資訊，請參閱[擴充功能提交程式概述](./submit/overview.md) 。