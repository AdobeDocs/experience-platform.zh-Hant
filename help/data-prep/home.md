---
keywords: Experience Platform;home；熱門主題；map csv;map csv;map csv file;map csv file to xdm;map csv to xdm;ui guide;mapper;mapping;data preparation;data preparation；準備資料；
solution: Experience Platform
title: 資料準備概述
topic-legacy: overview
description: 本檔案介紹Adobe Experience Platform的資料準備。
exl-id: f15eeb50-a531-4560-a524-1a670fbda706
translation-type: tm+mt
source-git-commit: daefd977cd09bd9cd7f8d6101b45be98f30d24ae
workflow-type: tm+mt
source-wordcount: '437'
ht-degree: 0%

---


# 資料準備概觀

資料準備可讓資料工程師將資料對應、轉換及驗證至Experience Data Model(XDM)。 「資料準備」會以「地圖」步驟顯示在「資料擷取」程式中，包括「CSV擷取」工作流程。 資料工程師可使用資料準備，在擷取期間執行下列資料操作：

- 定義簡單的直通映射，以將輸入屬性分配給XDM屬性
- 建立計算欄位以執行可分配給XDM屬性的行內計算
- 透過套用字串、數值或日期處理函式來轉換資料
- 使用層次函式構造XDM層次
- 在「資料準備」中處理資料時預覽資料

「資料準備」還應用多個內部資料驗證，以確保資料在接收時保持完整性。 如果可能，「資料準備」會自動將傳入的資料架構映射到XDM。 資料工程師可以變更、修正和刪除建議的映射，並視需要以映射取代它們。

## 映射

映射是輸入屬性或計算欄位與一個XDM屬性的關聯。 單一屬性可建立個別的映射，以映射至多個XDM屬性。

若要進一步瞭解不同的映射函式，請閱讀[映射函式指南](./functions.md)。

## 映射集

將一個模式轉換為另一個模式的映射集統稱為映射集。 每個資料流都會建立單一對應集。 映射集是資料流的一個組成部分，並作為資料流的一部分建立、編輯和監控。

要進一步瞭解映射集，包括如何使用映射集中的欄位，請閱讀[映射集指南](./mapping-set.md)。 要瞭解如何建立映射集並使用與映射集相關的其他API調用，請閱讀[開發人員指南](./api/mapping-set.md)中的映射集部分。

## 資料格式處理

「資料準備」可強穩地處理傳入Platform的不同格式資料。 若要進一步瞭解資料準備如何處理不同的資料類型，請閱讀[資料格式處理概述](./data-handling.md)。

## 後續步驟

本文檔介紹了有關Adobe Experience Platform資料準備的基本知識。 若要進一步瞭解不同的映射函式，請閱讀[映射函式指南](./functions.md)。 若要進一步瞭解資料準備如何處理不同的資料類型，請閱讀[資料格式處理指南](./data-handling.md#dates)。 要瞭解如何使用資料準備API，請閱讀[資料準備開發人員指南](api/overview.md)。
