---
title: 擴充功能開發快速入門
description: 開始在Adobe Experience Platform中開發您自己的標籤擴充功能。
exl-id: 3925b928-0180-4a4f-aaa6-42f342089560
source-git-commit: 0a4883cff4f8e04dd0dd62a9e01435fa302a9e54
workflow-type: tm+mt
source-wordcount: '448'
ht-degree: 71%

---

# 擴充功能開發快速入門

>[!NOTE]
>
>Adobe Experience Platform Launch已經過品牌重塑，現在是Adobe Experience Platform中的一套資料收集技術。 因此，所有產品檔案中出現了幾項術語變更。 請參閱下列[檔案](../term-updates.md)，以取得術語變更的彙總參考資料。

為了協助您著手展開擴充功能的建置，我們將使用Adobe工程師提供的開放原始碼架構工具，為您的擴充功能套件建立必要的檔案和檔案結構，而您只需負責最重要的工作：撰寫程式碼。

## 先決條件

* 安裝 [Node.js](https://nodejs.org/zh-tw/download/)。

## 擴充功能設定

建立將用來保存擴充功能檔案的目錄。

```shell
mkdir example && cd example
```

本指南採用擴充功能結構工具建置初始擴充結構，讓開發人員能夠快速展開編碼工作。此程序可視需要手動完成，而無需使用架構工具。

執行架構工具。

```shell
npx @adobe/reactor-scaffold
```

架構工具會顯示一些初始設定選項的提示，如下所示：

* 顯示名稱 - 擴充功能的可見名稱
* 版本 - 擴充功能的版本
* 說明 - 擴充功能用途的簡短說明
* 作者 - 擴充功能作者的名稱

架構工具隨後將提供用來建置擴充功能結構的選項：

* [擴充功能組態檢視](./configuration.md)：供擴充功能用來向使用者收集全域設定的檢視 (HTML 檔案)。
* [事件類型](./web/event-types.md)：定義要觀察的活動。例如，了解使用者於何時快速捲動，或使用者何時與頁面元素互動。然後，即可在規則中使用事件來執行動作。
* [條件類型](./web/condition-types.md)：條件類型會評估某條件是否成立。
例如，此選項可傳回使用者的瀏覽器是否為 Chrome、他們是否使用 iPad，或使用者是否位於特定網域。
* [動作類型](./web/action-types.md)：發生事件時所要執行的動作。例如，傳送分析信標、顯示優惠活動、儲存 Cookie，或開啟支援聊天。
* [資料元素類型](./web/data-element-types.md)：一個資料元素類型會擷取一個資料片段。此資料可能位於本機儲存體、Cookie、DOM 元素或自訂位置中。
* [共用模組](./web/shared.md)：共用模組是一種可讓擴充功能與其他擴充功能進行通訊的機制。
* [檢視](./web/views.md)：每個事件、條件、動作或資料元素類型都可提供一個檢視，讓使用者提供設定。

>[!NOTE]
>
>* 架構工具的後續執行將略過初始設定。
>* 可以新增多個事件、條件、動作。
>* 只能有一個組態檢視。

## 後續步驟

* 遵循[提交程式概述](./submit/overview.md)，並準備[驗證](./submit/upload-and-test.md#validate)和[上傳](./submit/upload-and-test.md#integration)您的擴充功能，以便在標籤生態系統中進行測試。
