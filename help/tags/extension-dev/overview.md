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
>Adobe Experience Platform Launch已被改名為Adobe Experience Platform的一套資料收集技術。 因此，所有產品文件中出現了幾項術語變更。 如需術語變更的彙整參考資料，請參閱以下[文件](../term-updates.md)。

在Adobe Experience Platform，標籤的主要目標之一是建立一個開放生態系統，讓Adobe之外的工程師可以在網站和移動應用程式上展示更多功能。 這是通過標籤擴展完成的。 在標籤屬性上安裝擴展後，該擴展的功能便可供該屬性的所有用戶使用。

本文檔概述了擴展的主要元件，並提供指向進一步文檔的連結，以幫助您指導擴展開發過程。

## 擴充功能結構

擴充功能由檔案目錄組成。具體來說，副檔名由清單檔案、庫模組和視圖組成。

### 資訊清單檔案

清單檔案([`extension.json`](./manifest.md))必須存在於目錄的根目錄中。 此檔案描述副檔名的構成以及某些檔案位於目錄中的位置。 清單的功能與 [`package.json`](https://docs.npmjs.com/files/package.json) 檔案 [npm](https://www.npmjs.com/) 項目。

### 程式庫模組

庫模組是描述不同 [元件](#components) 擴展提供（換句話說，要在標籤運行時庫中發出的邏輯）。 每個庫模組檔案的內容必須跟在 [CommonJS模組標準](https://nodejs.org/api/modules.html#modules-commonjs-modules)。

例如，如果要構建名為「發送信標」的操作類型，則必須有一個包含發送信標的邏輯的檔案。 如果使用JavaScript，則可以調用該檔案 `sendBeacon.js`。 此檔案的內容將在標籤運行時庫中發出。

只要描述庫模組在以下位置，您就可以將庫模組檔案放在擴展目錄中的任意位置 `extension.json`。

### 檢視

視圖是能夠載入到 [`iframe` 元素](https://developer.mozilla.org/zh-TW/docs/Web/HTML/Element/iframe) 在標籤應用程式中，特別是通過平台UI和資料收集UI。 該視圖必須包括擴展提供的指令碼並符合小API以便與應用程式通信。

任何副檔名的最重要視圖檔案是其配置。 請參閱 [擴展配置](#configuration) 的子菜單。

您的檢視中並沒有可用程式庫的限制。換句話說，您可以使用jQuery、下划線、React、Angular、Bootstrap或其他。 但是，仍建議您的分機與UI具有相似的外觀。

建議您將所有檢視相關檔案 (HTML、CSS、JavaScript) 放在與程式庫模組檔案不同的單一子目錄中。在 `extension.json`，可描述此視圖子目錄的位置。 然後，平台將從其Web伺服器中提供此子目錄（且僅此子目錄）。

## 庫元件 {#components}

每個擴展定義一組功能。 這些功能通過包含在 [庫](../ui/publishing/libraries.md) 已部署到您的網站或應用。 庫是單個元件的集合，包括條件、操作、資料元素等。 每個庫元件是在標籤運行時內發出的可重用代碼（由擴展提供）。

根據您是開發Web擴展還是邊擴展，可用的元件類型及其使用案例會有所不同。 有關每種擴展類型可用的元件的概述，請參閱以下子部分。

### Web擴展元件 {#web}

在 Web 擴充功能中，規則會透過事件觸發，接著在符合特定條件時執行特定動作。如需詳細資訊，請參閱 [Web 擴充功能中的模組流程](./web/flow.md)概述文件。

除 [核心模組](./web/core.md) 由Adobe提供，您可以在web擴展中定義以下庫元件：

* [事件](./web/event-types.md)
* [條件](./web/condition-types.md)
* [動作](./web/action-types.md)
* [資料元素](./web/data-element-types.md)
* [共用模組](./web/shared.md)

>[!NOTE]
>
>有關在Web擴展中實現庫元件所需格式的詳細資訊，請參見 [模組格式概述](./web/format.md)。

### 邊擴展的元件 {#edge}

邊緣擴充功能中，規則會透過條件檢查作業來觸發，接著在通過檢查後執行特定動作。請參閱 [邊緣延伸流](./edge/flow.md) 的子菜單。

可在邊擴展中定義以下庫元件：

* [條件](./edge/condition-types.md)
* [動作](./edge/action-types.md)
* [資料元素](./edge/data-element-types.md)

>[!NOTE]
>
>若要進一步了解在邊緣擴充功能中實作程式庫模組所需的格式，請參閱[模組格式概述](./edge/format.md)。

## 擴充功能組態 {#configuration}

擴充功能組態是指擴充功能據以向使用者收集全域設定的方式。該配置由視圖元件組成，該元件將標籤運行時庫中的設定導出並作為普通對象發出。

例如，請考慮一個擴展，該擴展允許用戶使用「發送信標」操作發送信標，並且信標必須始終包含帳戶ID。 分機應從分機配置視圖一次詢問帳戶ID，而不是每次用戶配置「發送信標」操作時都詢問其帳戶ID。 每次發送信標時，「發送信標」操作都可以從擴展配置中提取帳戶ID並將其添加到信標中。

當用戶在UI中為屬性安裝擴展時，將顯示擴展配置視圖，為完成安裝，必須完成該視圖。

要瞭解更多資訊，請參閱上的指南 [擴展配置](./configuration.md)。

## 提交擴展

完成擴展構建後，您可以提交它以列在「平台」的擴展目錄中。 查看 [擴展提交過程概述](./submit/overview.md) 的子菜單。
