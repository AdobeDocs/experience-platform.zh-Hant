---
keywords: Experience Platform；配置檔案；即時客戶配置檔案；故障排除；API；統一配置檔案；統一配置檔案；配置檔案；rtcp;XDM圖形
title: 平台中的一般輔助功能
type: Documentation
description: 瞭解有關Adobe Experience Platform支援的一般輔助功能的更多資訊，包括鍵盤導航、調色板和對比度以及輔助技術支援。
exl-id: 4b7e2f2b-af51-4376-8a63-16c921cc7135
source-git-commit: 7b197f253aa5ce04a682040814cf749407154ebc
workflow-type: tm+mt
source-wordcount: '484'
ht-degree: 3%

---

# Experience Platform中的輔助功能

Adobe Experience Platform致力於向所有個人提供無障礙和包容的功能，包括使用語音識別軟體和螢幕閱讀器等輔助設備的用戶。 本文檔概述了平台支援的一般輔助功能，包括鍵盤導航、語義結構、前景元素和背景元素之間的充分對比以及對輔助技術的支援。

## 輔助技術

殘疾用戶經常依靠硬體和軟體（即輔助技術）來訪問數字內容和使用軟體產品。 Adobe Experience Platform支援多種輔助技術(AT)，如螢幕閱讀器、縮放和語音識別軟體，方法是根據輔助工具的最佳做法，如在需要時使用語義代碼、文本等價物、標籤和ARIA。 Experience Platform用戶介面(UI)中的交互元素使用相應的標籤、可訪問的名稱和角色來標識其用途和當前狀態。 這確保輔助技術，例如螢幕閱讀器，能夠向用戶讀出標籤和其他資訊，以便他們能夠容易地與應用程式控制項交互。

## 鍵盤協助工具

Experience Platform努力支援全鍵盤輔助功能。

以下是可輔助協助工具的導覽元素：
* Tab鍵在UI元素、節和菜單組之間移動。
* 箭頭鍵在菜單組內移動，以將焦點設定為單個活動元素。
* Shift + Tab在制表符順序中向後移動。
* 返回(Enter)和空格鍵激活選定項。
* 轉義鍵(ESC)用作取消按鈕，以在出現時關閉對話框。
* Experience Platform在選定元素周圍顯示藍色邊框，以顯示當前UI元素的焦點的明確指示。

![顯示在選定元素周圍的藍色邊框，以指示已應用焦點。](images/profile-overview-tab.png)

## 調色盤和對比

Experience Platform [WCAG 2.1安](https://www.w3.org/TR/WCAG/) 符合性，包括顏色對比度要求。 Experience PlatformUI在應用程式中提供了足夠的對比度，以確保低視力或缺色用戶能夠獲得可訪問的觀看體驗。

![Experience PlatformUI首頁上顯示的調色板和對比度。](images/homepage.png)

## 必填欄位驗證

在添加資料、建立方案或定義段時，必填欄位都以可視方式顯示，使用欄位文本標籤旁邊的星號，並以寫程式方式顯示。 在欄位中和保存時輸入無效資料時，這些欄位將觸發驗證。 如果必填欄位未通過驗證，則它將以紅色列出，並帶有錯誤表徵圖，同時還會顯示需要修復的問題的書面說明。

![未通過驗證的必需欄位的特寫。 該欄位以紅色顯示，並顯示錯誤表徵圖。](images/field-validation.png)
