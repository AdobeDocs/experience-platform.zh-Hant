---
keywords: Experience Platform;home；熱門主題；map csv;map csv;map csv file;map csv file to xdm;map csv to xdm;ui guide;mapper;mapping;data preparation;data preparation；準備資料；
solution: Experience Platform
title: 資料準備概述
topic: 概述
description: 本檔案介紹Adobe Experience Platform的資料準備。
translation-type: tm+mt
source-git-commit: 73bf6abb143c0866a400aafe984f9a553ffc1abf
workflow-type: tm+mt
source-wordcount: '352'
ht-degree: 1%

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

## 後續步驟

本文檔介紹了有關Adobe Experience Platform資料準備的基本知識。 若要進一步瞭解不同的映射函式，請閱讀[映射函式指南](./functions.md)。 要瞭解有關不同日期時間字串的更多資訊，請閱讀[日期字串指南](./dates.md)。 要瞭解如何使用資料準備API，請閱讀[資料準備開發人員指南](api/overview.md)。