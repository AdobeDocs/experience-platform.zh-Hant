---
title: PubMatic Connect
description: PubMatic提供未來程式化的數位行銷供應鏈，以最大化客戶價值。 PubMatic Connect結合平台技術與專屬服務，以強化詳細目錄與資料的封裝與異動方式。
last-substantial-update: 2023-12-14T00:00:00Z
exl-id: 21e07d2c-9a6a-4cfa-a4b8-7ca48613956c
source-git-commit: c35b43654d31f0f112258e577a1bb95e72f0a971
workflow-type: tm+mt
source-wordcount: '923'
ht-degree: 2%

---

# PubMatic Connect目的地 {#pubmatic-connect}

## 概觀 {#overview}

使用[!DNL PubMatic Connect]提供未來程式化的數位行銷供應鏈，以最大化客戶價值。 [!DNL PubMatic Connect]結合平台技術與專屬服務，以強化詳細目錄與資料的封裝與交易方式。

使用此目的地將對象資料傳送至[!DNL PubMatic Connect]平台。

>[!IMPORTANT]
>
>目的地聯結器和檔案頁面是由[!DNL PubMatic]團隊建立和維護的。 若有任何查詢或更新要求，請直接透過`support@pubmatic.com`連絡他們。

## 使用案例 {#use-cases}

為協助您更清楚瞭解您應如何及何時使用[!DNL PubMatic Connect]目的地，以下是Adobe Experience Platform客戶可藉由使用此目的地解決的範例使用案例。

### 在行動、網頁和CTV平台上鎖定使用者 {#targeting}

發佈者或資料提供者想要使用大量識別碼，從Adobe Experience Platform傳送對象至[!DNL PubMatic Connect]，以鎖定行動、網頁及CTV平台上的使用者。

## 先決條件 {#prerequisites}

請洽詢您的[!DNL PubMatic]帳戶管理員，確定您的帳戶已正確設定，並支援對象區段的上線。 他們也會確保您擁有使用此目的地的所有相關詳細資料，並在設定期間為您提供支援。

## 支援的身分 {#supported-identities}

[!DNL PubMatic Connect]支援下表所述的身分啟用。 深入瞭解[身分](/help/identity-service/features/namespaces.md)。

| 目標身分 | 說明 | 考量事項 |
| --------------- | ------ | --- |
| GAID | GOOGLE ADVERTISING ID | 當您的來源身分是GAID名稱空間時，請選取GAID目標身分。 |
| IDFA | 廣告商適用的Apple ID | 當您的來源身分是IDFA名稱空間時，請選取IDFA目標身分。 |
| extern_id | 自訂使用者ID | 當您的來源身分是自訂名稱空間時，請選取此目標身分。 |

{style="table-layout:auto"}

## 支援的對象 {#supported-audiences}

本節說明您可以將哪些型別的對象匯出至此目的地。

| 對象來源 | 支援 | 說明 |
| --- | --------- | ------ |
| [!DNL Segmentation Service] | ✓ (A) | 透過Experience Platform[細分服務](../../../segmentation/home.md)產生的對象。 |
| 自訂上傳 | ✓ (A) | 對象[從CSV檔案匯入](../../../segmentation/ui/audience-portal.md#import-audience)至Experience Platform。 |

{style="table-layout:auto"}

## 匯出型別和頻率 {#export-type-frequency}

請參閱下表以取得目的地匯出型別和頻率的資訊。

| 項目 | 類型 | 附註 |
| --- | --- | --- |
| 匯出類型 | **[!UICONTROL 區段匯出]** | 您正在匯出區段（對象）的所有成員，而這些區段具有PubMatic Connect目的地所使用的識別碼（名稱、電話號碼或其他）。 |
| 匯出頻率 | **[!UICONTROL 串流]** | 串流目的地是「一律開啟」的API型連線。 當根據區段評估在Experience Platform中更新設定檔時，聯結器會將更新傳送至下游的目標平台。 深入瞭解[串流目的地](/help/destinations/destination-types.md#streaming-destinations)。 |

{style="table-layout:auto"}

## 連線到目標 {#connect}

>[!IMPORTANT]
>
> 若要連線到目的地，您需要&#x200B;**[!UICONTROL 管理目的地]** [存取控制許可權](/help/access-control/home.md#permissions)。 閱讀[存取控制總覽](/help/access-control/ui/overview.md)或連絡您的產品管理員以取得必要的許可權。

若要連線到此目的地，請依照[目的地組態教學課程](../../ui/connect-destination.md)中所述的步驟進行。 在目標設定工作流程中，填寫以下兩個區段中列出的欄位。

### 驗證目標 {#authenticate}

若要驗證到目的地，請填入必填欄位，然後選取&#x200B;**[!UICONTROL 連線到目的地]**。

![如何驗證](../../assets/catalog/advertising/pubmatic/authenticate-destination.png)

- **[!UICONTROL 持有人權杖]**：填入持有人權杖以驗證目的地。

### 填寫目標詳細資訊 {#destination-details}

若要設定目的地的詳細資訊，請填寫下方的必填和選用欄位。 UI中欄位旁的星號表示該欄位為必填欄位。

![目的地詳細資料](../../assets/catalog/advertising/pubmatic/destination-details.png)

- **[!UICONTROL 名稱]**：您日後可辨識此目的地的名稱。
- **[!UICONTROL 描述]**：可協助您日後識別此目的地的描述。
- **[!UICONTROL 資料合作夥伴識別碼]**：在您[!DNL PubMatic]帳戶中為此整合設定的資料合作夥伴識別碼。
- **[!UICONTROL 預設國家/地區代碼]**：如果設定檔中未提供任何內容，則應套用至所有身分的預設國家/地區代碼。
- **[!UICONTROL 帳戶識別碼]**：您的[!DNL PubMatic Connect]帳戶識別碼。
- **[!UICONTROL 帳戶型別]**： [!DNL PubMatic]平台帳戶的帳戶型別。 如果您有任何選擇的問題，請洽詢您的[!DNL PubMatic]客戶經理。 可用的選項包括：
   - [!UICONTROL 發行者]
   - [!UICONTROL DEMAND_PARTNER]
   - [!UICONTROL 購買者]

### 啟用警示 {#enable-alerts}

您可以啟用警報以接收有關傳送到您目的地的資料流狀態的通知。 從清單中選取警報以訂閱接收有關資料流狀態的通知。 如需警示的詳細資訊，請參閱[使用UI訂閱目的地警示](../../ui/alerts.md)的指南。

當您完成提供目的地連線的詳細資訊後，請選取&#x200B;**[!UICONTROL 下一步]**。

## 啟用此目的地的區段 {#activate}

>[!IMPORTANT]
>
> - 若要啟用資料，您需要&#x200B;**[!UICONTROL 檢視目的地]**、**[!UICONTROL 啟用目的地]**、**[!UICONTROL 檢視設定檔]**&#x200B;和&#x200B;**[!UICONTROL 檢視區段]** [存取控制許可權](/help/access-control/home.md#permissions)。 閱讀[存取控制總覽](/help/access-control/ui/overview.md)或連絡您的產品管理員以取得必要的許可權。
>
> - 若要匯出&#x200B;_身分_，您需要&#x200B;**[!UICONTROL 檢視身分圖表]** [存取控制許可權](/help/access-control/home.md#permissions)。<br> ![選取工作流程中反白的身分名稱空間，以啟用目的地的對象。](../../assets/overview/export-identities-to-destination.png "選取工作流程中反白顯示的身分名稱空間，以啟用目的地的對象。"){width="100" zoomable="yes"}

閱讀[啟用串流區段匯出目的地的設定檔和區段](/help/destinations/ui/activate-segment-streaming-destinations.md)，以取得啟用此目的地的對象區段的指示。

### 對應屬性和身分 {#map}

選取來源欄位：

- 選取識別碼（通常是IDFA或自訂ID名稱空間等名稱空間）。

選取目標欄位：

- 請洽詢您的[!DNL PubMatic]帳戶管理員，以取得在此步驟中哪種UID型別將正確的資訊。
- 選取符合您在第一個步驟中選取的識別碼的[!DNL PubMatic UID]型別編號。

![對應屬性和身分](../..//assets/catalog/advertising/pubmatic/export-identities-to-destination.png)

## 匯出的資料/驗證資料匯出 {#exported-data}

[!DNL PubMatic] UI可讓您檢查資料是否已正確推送，以及區段是否可供使用。 推播資料後，可能需要24小時才能更新[!DNL PubMatic] UI。

## 資料使用與控管 {#data-usage-governance}

處理您的資料時，所有[!DNL Adobe Experience Platform]目的地都符合資料使用原則。 如需[!DNL Adobe Experience Platform]如何強制資料控管的詳細資訊，請閱讀[資料控管概觀](/help/data-governance/home.md)。
