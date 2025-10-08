---
title: 內容卡片檢視
description: 本指南詳細說明Adobe Experience Platform Assurance中內容卡片檢視的相關資訊。
source-git-commit: fa5dbbfcc0c178c8886000479f44afd5d63c8c34
workflow-type: tm+mt
source-wordcount: '709'
ht-degree: 0%

---

# Assurance中的內容卡片檢視

Adobe Experience Platform Assurance中的應用程式內傳訊檢視可讓您驗證應用程式、監視傳送到裝置的內容卡片，以及預覽卡片。

## 內容卡片

在&#x200B;**[!UICONTROL 內容卡]**&#x200B;標籤頂端是&#x200B;**[!UICONTROL 內容卡]**&#x200B;下拉式清單。 這會列出Assurance工作階段中收到的所有內容卡片。 如果卡片不在此清單中，表示應用程式從未收到該卡片。

![包含卡片清單的內容卡片下拉式清單](./images/content-cards/dropdown.png)

選取內容卡片會顯示該卡片的許多相關資訊，如下節所述。

### 卡片預覽

在右側面板中，**[!UICONTROL 卡片預覽]**&#x200B;窗格會顯示卡片在常見範本（僅限小影像、大影像和僅限影像）中的呈現方式。

![預覽選取的內容卡](./images/content-cards/preview.png)

使用&#x200B;**[!UICONTROL 佈景主題]**&#x200B;切換功能，以明暗模式檢視卡片。

![以深色佈景主題預覽選取的內容卡](./images/content-cards/preview-dark.png)

### 可用標籤

在左側部分，可用的標籤取決於所選的卡片。 如果卡片包含規則，您會看到三個標籤： **[!UICONTROL 資訊]**、**[!UICONTROL 互動]**&#x200B;和&#x200B;**[!UICONTROL 分析規則]**。

出現規則時![可用的標籤：資訊、互動、分析規則](./images/content-cards/tabs-with-rules.png)

如果卡片不包含規則，您會看到兩個標籤： **[!UICONTROL 資訊]**&#x200B;和&#x200B;**[!UICONTROL 互動]**。

![沒有規則時可用的標籤：資訊和互動](./images/content-cards/tabs-no-rules.png)

### 資訊索引標籤

**[!UICONTROL 資訊]**&#x200B;索引標籤在頂端顯示&#x200B;**[!UICONTROL 卡片屬性]**&#x200B;區段，包括&#x200B;**[!UICONTROL 目前狀態]** （觸發、顯示、關閉、取消資格）的徽章，以及&#x200B;**[!UICONTROL 範本]** （僅限小影像、大影像或僅限影像）、**[!UICONTROL 表面]**&#x200B;等中繼詳細資訊，以及任何自訂索引鍵值配對。

![顯示目前狀態徽章、範本、表面和索引鍵值配對的卡片屬性](./images/content-cards/card-properties.png)

在其下方，**[!UICONTROL 行銷活動屬性]**&#x200B;區段會顯示從Adobe Journey Optimizer (AJO)載入的資訊。

您也可以選取「**[!UICONTROL 檢視行銷活動]**」以在AJO中開啟資訊卡以進行檢查或編輯。

![具有檢視行銷活動按鈕的行銷活動屬性區段](./images/content-cards/campaign-properties.png)

### 互動標籤

**[!UICONTROL 互動]**&#x200B;索引標籤會將每個卡片的生命週期總結為一系列徽章：它一律以&#x200B;**[!UICONTROL 觸發器]**&#x200B;開頭，後面接著規則產生的任何結果 — **[!UICONTROL 顯示]**、**[!UICONTROL 解除]**&#x200B;或&#x200B;**[!UICONTROL 取消資格]**。

![顯示從觸發程式到顯示、解除或取消資格之生命週期徽章的互動表](./images/content-cards/interactions-tab.png)

### 分析規則標籤

**[!UICONTROL 分析]**&#x200B;索引標籤會顯示一個事件資料表，根據卡片規則最多有三個規則資料行 — **[!UICONTROL 顯示]**、**[!UICONTROL 取消]**&#x200B;和&#x200B;**[!UICONTROL 取消資格]**。 如果卡片只定義一個規則，則只會顯示該欄。

每一列代表一個工作階段事件，每一欄指出卡片的規則是否與該事件的條件相符。 0%分數表示沒有符合的條件；100%是完全符合（規則會引發）。

如果事件符合條件，則會顯示綠色核取記號。 如果事件不符，則會顯示紅色圖示。

![分析索引標籤事件表格，包含[顯示]、[解除]和[取消資格]規則欄](./images/content-cards/rules-tab.png)

使用&#x200B;**[!UICONTROL 符合臨界值]**&#x200B;滑桿，依最小符合百分比篩選事件。

![符合臨界值滑桿，可依最小符合百分比篩選事件](./images/content-cards/match-threshold.png)

當您選取事件時，右側會開啟詳細資料面板，其中包含三個規則的收合式選單： **[!UICONTROL 顯示]**、**[!UICONTROL 關閉]**&#x200B;以及&#x200B;**[!UICONTROL 取消資格]**。

![事件詳細資訊面板列出顯示、解除和取消規則資格](./images/content-cards/rules-panel.png)

展開任何區段以檢視規則的條件、符合的條件，以及該結果的已計算符合百分比。

![顯示符合條件和符合百分比的展開規則摺疊式功能表](./images/content-cards/expanded-accordion.png)

## 請求索引標籤

**[!UICONTROL 要求]**&#x200B;索引標籤會顯示要求的內容卡片以及哪個表面。

![顯示內容卡請求的[請求]索引標籤](./images/content-cards/requests-tab.png)

使用&#x200B;**[!UICONTROL 檢視卡片]**&#x200B;按鈕返回特定內容卡片的資訊標籤。

## 事件清單索引標籤

**[!UICONTROL 事件清單]**&#x200B;索引標籤會顯示與內容卡相關的工作階段事件，包括AJO主張請求/回應、卡片生命週期事件和互動追蹤。 您可以搜尋、篩選、排序和自訂欄，以及匯出結果。

選取事件會開啟右側詳細資訊面板，其中包含原始裝載和關鍵屬性；您也可以標幟事件以供後續追蹤。 此檢視適用於關聯工作階段中的請求、規則結果和互動。

![事件清單索引標籤，其中包含內容卡的可搜尋、可篩選的工作階段事件](./images/content-cards/event-list.png)

## 驗證標籤

**[!UICONTROL 驗證]**&#x200B;索引標籤會針對您目前的工作階段執行驗證，檢查應用程式是否已正確設定傳訊：

![驗證標籤結果會檢查目前工作階段的傳訊設定](./images/content-cards/validation.png)
