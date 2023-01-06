---
keywords: Experience Platform；設定檔；即時客戶設定檔；疑難排解；API；統一設定檔；統一設定檔；統一；設定檔；rtcp;XDM圖表
title: Platform中的一般協助工具功能
type: Documentation
description: 進一步了解Adobe Experience Platform支援的一般協助工具功能，包括鍵盤導覽、調色盤和對比，以及輔助技術支援。
exl-id: 4b7e2f2b-af51-4376-8a63-16c921cc7135
source-git-commit: 7b197f253aa5ce04a682040814cf749407154ebc
workflow-type: tm+mt
source-wordcount: '484'
ht-degree: 3%

---

# 協助工具功能Experience Platform

Adobe Experience Platform致力於為所有個人提供無障礙且包容的功能，包括使用語音識別軟體和螢幕閱讀器等輔助裝置的使用者。 本檔案概述Platform支援的一般協助工具功能，包括鍵盤導覽、語意結構、前景元素與背景元素之間的充分對比，以及支援輔助技術。

## 輔助技術

殘疾使用者經常依賴硬體和軟體（稱為輔助技術）來存取數位內容和使用軟體產品。 Adobe Experience Platform支援數種輔助技術(AT)，例如螢幕閱讀器、縮放和語音辨識軟體，方法是遵循協助工具最佳實務，例如視需要使用語義碼、文字等效項、標籤和ARIA。 Experience Platform使用者介面(UI)中的互動式元素會使用對應的標籤、可存取的名稱和角色，來識別其用途和目前狀態。 這可確保輔助技術（例如螢幕閱讀器）可向使用者閱讀標籤和其他資訊，以便他們輕鬆與應用程式控制項互動。

## 鍵盤協助工具

Experience Platform致力支援完整的鍵盤協助功能。

以下是可輔助協助工具的導覽元素：
* Tab鍵在UI元素、區段和功能表群組之間移動。
* 方向鍵在功能表群組內移動，將焦點設為個別作用中元素。
* Shift + Tab鍵可在Tab鍵順序中向後移動。
* 返回鍵(Enter)和空格鍵激活選定項。
* 逸出鍵(ESC)可作為取消按鈕，以在對話方塊出現時關閉對話方塊。
* Experience Platform會在選取的元素周圍顯示藍色邊框，以清楚指出目前有哪個UI元素。

![出現在所選元素周圍的藍色邊框，表示已套用焦點。](images/profile-overview-tab.png)

## 調色盤和對比

Experience Platform努力 [WCAG 2.1 AA](https://www.w3.org/TR/WCAG/) 符合性，包括色彩對比度要求。 Experience PlatformUI在應用程式中提供足夠的對比，以確保為視力不足或色彩缺乏的使用者提供可存取的檢視體驗。

![Experience PlatformUI首頁上顯示的調色盤和對比。](images/homepage.png)

## 必填欄位驗證

新增資料、建立結構或定義區段時，必填欄位會以視覺化方式指出，在欄位的文字標籤旁使用星號，並以程式設計方式指出。 在欄位中和儲存時輸入無效資料時，這些欄位會觸發驗證。 如果必填欄位未通過驗證，則會以紅色列出，並顯示錯誤圖示，且還會顯示需要修正之問題的書面說明。

![尚未通過驗證的必填欄位的特寫。 欄位會以紅色顯示，並顯示錯誤圖示。](images/field-validation.png)
