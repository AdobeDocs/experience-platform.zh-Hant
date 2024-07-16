---
title: Edge Delivery檢視
description: 本指南詳細說明Adobe Experience Platform Assurance中Edge Delivery檢視的相關資訊。
exl-id: 570c1bcb-ec6d-465e-84ff-ed910d4f7e8a
source-git-commit: a11f469cb54421e0ca30c7c5878128e216470f7f
workflow-type: tm+mt
source-wordcount: '962'
ht-degree: 2%

---

# 在Assurance中檢視Edge Delivery

**[!UICONTROL Edge Delivery保證]**&#x200B;內的&#x200B;**[!UICONTROL Adobe Experience Platform]**&#x200B;檢視可讓您檢查並驗證[!UICONTROL AJO輸入]邊緣傳遞的訊息到您的網頁與行動應用程式。 此檢視對於疑難排解[!UICONTROL AJO傳入]網頁和行動行銷活動與歷程的傳送特別有用。

## 快速入門

在繼續之前，請確定您有權存取以下服務：

- [Adobe Experience Platform 資料集合 UI](https://experience.adobe.com/#/data-collection/)。
- [Adobe Experience Platform Assurance](https://experience.adobe.com/assurance)

若要瞭解如何在您的應用程式中安裝&#x200B;**[!UICONTROL 保證]**，請閱讀[實作保證指南](../tutorials/implement-assurance.md)。

## 搭配Edge Delivery使用保證

開啟&#x200B;**[!UICONTROL 保證]**&#x200B;工作階段後，您就可以將&#x200B;**[!UICONTROL Edge Delivery]**&#x200B;檢視新增至&#x200B;**[!UICONTROL 保證]**。 在左側面板底部，選取&#x200B;**[!UICONTROL 設定]**&#x200B;以新增&#x200B;**[!UICONTROL Edge Delivery]**&#x200B;檢視並&#x200B;**儲存**。

![選取左下方的[設定]以新增外掛程式](./images/edge-delivery/add-plugin.png)

新增後，請在&#x200B;**[!UICONTROL Edge Delivery]**&#x200B;區段中選取&#x200B;**[!UICONTROL Adobe Journey Optimizer]**&#x200B;檢視，以驗證傳入邊緣傳遞。

![可在Adobe Journey Optimizer檢視群組中存取Edge Delivery](./images/edge-delivery/ajo-plugins.png)

## 請求清單

在檢視的主窗格上，會顯示邊緣傳送要求清單。 此清單顯示向Experience Edge提出並由&#x200B;**[!UICONTROL 傳入傳遞服務]**&#x200B;處理的所有[!UICONTROL 傳入AJO]要求，包括擷取個人化決定的要求，以及追蹤個人化主張互動（例如顯示、點按、觸發或解除）。

請求會依時間戳記排序，最新的請求會位於頂端。 除了時間戳記之外，此清單也包含「請求ID」欄，以及「請求型別」，可為下列其中一項：

- **[!UICONTROL 體驗傳送]**：擷取個人化決定的要求
- **[!UICONTROL 體驗互動]**：追蹤個人化主張互動的要求
- **[!UICONTROL 體驗傳遞和互動]**：擷取個人化決定的要求，其中也包含個人化主張互動
- **[!UICONTROL 預覽傳遞]**：擷取預覽個人化決定的要求

您也可以在清單頂端的搜尋列中輸入搜尋字詞，以篩選請求。 依特定值（例如ID）篩選時，這項功能相當實用。

![傳入要求清單會顯示在主要檢視中](./images/edge-delivery/request-list.png)

## 詳細請求檢視

在主檢視中選取請求後，所選請求的詳細資訊將顯示在右側。 此檢視包含下列段落：

### 請求總覽

本節提供所選請求的高層級概觀，包括[!UICONTROL 組織ID]、[!UICONTROL Edge叢集]、[!UICONTROL 請求ID]和[!UICONTROL 請求型別]、[!UICONTROL 沙箱ID]、[!UICONTROL 沙箱名稱]、[!UICONTROL 資料流ID]，以及有[!UICONTROL 體驗傳送]請求時的請求表面清單。

![要求概觀段落提供高階要求詳細資料](./images/edge-delivery/request-overview.png)

### 設定檔

本節提供處理請求時使用的設定檔資料相關資訊，包括身分對應、區段會籍和同意設定。\
在疑難排解傳送問題（例如由於遺失或延遲區段成員資格或選擇退出同意設定而無法正常運作）時，[!UICONTROL 設定檔]區段非常有用。

![設定檔區段包含身分對應、區段成員資格及同意設定](./images/edge-delivery/profile.png)

### 符合資格的活動

本節提供符合所選請求資格的活動清單，包括活動型別、ID、身分名稱空間、介面、排程和對象。 在[原始執行追蹤區段](#execution)中找到有關活動的詳細資訊。

![合格活動區段包含合格活動的詳細資料](./images/edge-delivery/qualified-activities.png)

### 不合格活動

本節提供不合格之活動的清單。 除了活動型別、ID、身分名稱空間、介面、排程和對象之外，本節也包含活動不符合資格的原因清單。

![不合格活動區段包含不合格活動詳細資料和排除原因](./images/edge-delivery/unqualified-activities.png)

### 訊息詳細資料

本節提供所選請求所傳遞之訊息的詳細資訊。 其中包含訊息ID、片段、決定原則、[!UICONTROL Offer decisioning]引數以及訊息選擇內容。

![包含已傳遞訊息詳細資料的區段，例如訊息ID和選擇內容、片段、決定原則及決定引數](./images/edge-delivery/message-details.png)

### 互動

本節提供在所選請求中追蹤之互動的詳細資訊。 它包含互動型別（在`propositionEventType`下）以及相關的主張中繼資料，例如活動中繼資料（在`scopeDetails.activity`下）和主張事件權杖（在`scopeDetails.characteristics.eventToken`中）。

![透過主張權杖和相關活動中繼資料追蹤互動](./images/edge-delivery/interactions.png)

### 原始追蹤

本節提供所選請求的原始追蹤。 它包含要求的完整追蹤，包括在&#x200B;**[!UICONTROL 傳入傳遞服務]**&#x200B;中收到的實際要求、執行追蹤和回應追蹤。 這對於進階疑難排解（例如由於傳送服務無法使用、資料遺失或不正確而導致傳送無法如預期運作）或瞭解完整的請求處理流程而言，非常有用。

#### 請求

要求追蹤包含完整要求，因為&#x200B;**[!UICONTROL 傳入傳遞服務]** **[!UICONTROL Konductor]**&#x200B;上游已接收該要求。 其中包含請求標頭、本文和其他中繼資料。 例如，可在`event.body.xdm`欄位中檢查要求的XDM裝載。

![在要求追蹤](./images/edge-delivery/request.png)中找到包括標頭和本文在內的詳細要求資訊

#### 執行

執行追蹤包含由&#x200B;**[!UICONTROL 傳入傳遞服務]**&#x200B;處理之要求的完整追蹤。 它會顯示執行內容、活動資格、訊息選擇和其他處理步驟。 在`context.messages`和`context.exceptions`欄位中可找到處理要求期間發生的任何錯誤或警告。 您可以在`context.qualifiedActivitiesDetailed`和`context.unqualifiedActivitiesDetailed`欄位中找到詳細的活動資格資訊。

![執行追蹤包含執行內容、活動資格、訊息選擇及其他處理詳細資料](./images/edge-delivery/execution.png)

#### 回應

回應追蹤包含完整回應，因為它由&#x200B;**[!UICONTROL 傳入傳遞服務]**&#x200B;下游傳回至&#x200B;**[!UICONTROL Konductor]**。 其中包含回應標頭、本文和其他中繼資料。 您可以使用&#x200B;**[!UICONTROL 複製值]**&#x200B;按鈕，將識別碼為`1`的郵件複製到剪貼簿，然後將它貼到JSON檢視器中，即可檢查完整的回應內文。

![回應追蹤包含傳回至下游的完整回應本文](./images/edge-delivery/response.png)
