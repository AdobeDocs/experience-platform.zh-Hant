---
title: 事件異動檢視
description: 本指南會詳細介紹 Adob​​e Experience Platform Assurance 中事件異動檢視的資訊。
exl-id: ad97f2c1-5bbc-49e2-8378-edcb8af149a3
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '695'
ht-degree: 100%

---

# 事件異動檢視

Adobe Experience Platform Assurance 中的事件異動檢視讓您可驗證 Edge Network 用戶端實作並進行偵錯，而且可近乎即時地查看上游驗證結果。

## 為 Edge Network 工作流程設定 Assurance

[設定 Assurance](../tutorials/implement-assurance.md) 後，請確保您已實作應用程式中最新版本的 Assurance 和 Edge Network 擴充功能。

若要檢視您的事件，請在左側選單中選取「**[!UICONTROL 事件異動]**」(在 **[!UICONTROL Adobe Experience Platform Edge]** 章節中)。

如果您沒有看到此選項，請在視窗左下方選取「**[!UICONTROL 設定]**」，新增「**[!UICONTROL 事件異動]**」檢視，然後選取「**[!UICONTROL 儲存]**」。

## 開始使用「事件異動」檢視

在本節中，您會熟悉事件異動檢視，並了解如何在 Edge Network 工作流程有效地將它用於端到端驗證。

### 事件處理流程

![事件異動檢視](./images/event-transactions/event-transactions-view.png)

事件異動檢視會依事件處理流程的順序顯示三欄：

- **[!UICONTROL 用戶端]**：此欄會顯示用戶端處理或接收的事件，可供 Mobile SDK 存取。這包括使用 API 呼叫建立的事件，例如 `Edge.sendEvent`，以及用戶端從 Edge Network 伺服器接收到的回應事件控點 (如有)。用戶端事件範例：
   - AEP 要求事件是透過 Edge 擴充功能傳送的事件，並包含 XDM 和可選的自由格式資料。
   - AEP 回應事件控點則是從 Edge Network 接收的事件控點，以回應 AEP 要求事件。要求事件可以不接收、接收一個或多個回應事件控點。
   - 發生錯誤時，可能會看到 AEP 錯誤回應，例如，如果無法處理 XDM 承載或者其中一個上游服務傳回錯誤或警告。
- **[!UICONTROL Edge Network]**：本欄會顯示 Edge Network 透過網路要求在伺服器端接收到的事件以及該事件包含哪些資料和中繼資料。
- **[!UICONTROL 上游]**：本欄會顯示已設定的上游服務所接收到的事件，包括有關傳入事件的處理和/或驗證結果的詳細資訊。
請注意，本欄是動態的，並可能會依據兩個主要因素而顯示不同類型的資訊：
   - 資料流設定和在此設定啟用的服務。
   - 傳送至 Edge Network 的事件類型。

### 檢查事件

「事件異動」檢視中顯示的事件會提供在每個狀態處理之資料的格式和內容的資訊，以及對於在上游處理資料時遇到的任何警告或錯誤具洞察力的詳細資料。該檢視有助於縮小事件/要求層級的偵錯資訊範圍以及在開發週期中提早識別錯誤。

#### 展開事件的詳細資料

若要檢查事件，請從檢視中選取所需的事件。此動作會在畫面右側展開「**[!UICONTROL 事件詳細資料]**」檢視。
巢狀資料會以樹形格式顯示。選取索引鍵名稱左邊的 **+** (加號) 按鈕，即可檢查巢狀索引鍵值。

![事件詳細資料](./images/event-transactions/event-details.png)

#### 檢查警告或錯誤

每個事件名稱都會有一個圖示作為前綴，象徵該事件高層級的處理狀態：

- 如果事件已成功處理，會顯示綠色的打勾記號。
- 如果偵測到警告或錯誤，則會顯示警告標誌。若要了解警告或錯誤原因的詳細資訊，請在&#x200B;**[!UICONTROL 事件詳細資料]**&#x200B;檢視中選取相關事件。

### 組態設定 

選取 **[!UICONTROL Edge Network]** 欄標題旁的資訊工具提示，即可檢查目前使用的資料流識別碼。

![顯示資料流 ID](./images/event-transactions/show-datastream-id.png)

>[!INFO]
>
>當多個用戶端連線至相同的 Assurance 工作階段並使用不同的資料流 ID 時，您會看到它們全都顯示在這裡。但是，這並不表示您目前的實作即是使用多個資料流。只有該應用程式所使用的標記 (行動資產) 中目前設定的資料流 ID 會用於處理來自該用戶端的新事件。當使用不同的組態設定和連線的多個用戶端測試較複雜的使用案例時，使用單獨的 Assurance 工作階段可能有助於簡化驗證流程。
