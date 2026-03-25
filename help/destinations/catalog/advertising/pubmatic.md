---
title: PubMatic Connect
description: PubMatic提供未來程式化的數位行銷supply chain，實現客戶價值的最大化。 PubMatic Connect結合平台技術與專屬服務，以強化詳細目錄與資料的封裝與異動方式。
last-substantial-update: 2025-02-12T00:00:00Z
exl-id: 21e07d2c-9a6a-4cfa-a4b8-7ca48613956c
source-git-commit: 20427c4c8826905a77fac04d055d523b12a6f739
workflow-type: tm+mt
source-wordcount: '1130'
ht-degree: 3%

---


# PubMatic Connect目的地 {#pubmatic-connect}

## 概觀 {#overview}

使用[!DNL PubMatic Connect]提供未來程式化的數位行銷supply chain，以最大化客戶價值。 [!DNL PubMatic Connect]結合平台技術與專屬服務，以強化詳細目錄與資料的封裝與交易方式。

有兩個可用的目的地可讓您將受眾資料傳送至PubMatic Connect平台。 它們的功能稍有不同：

1. PubMatic Connect

   在初始啟用期間，此目的地會自動在PubMatic平台中註冊對象，並使用內部[!DNL Adobe Experience Platform] ID進行對應。

2. PubMatic Connect （自訂對象ID對應）

   此目的地可讓您選擇在啟動工作流程期間手動新增對應ID。 當資料應傳送至PubMatic平台中的現有對象，或需要自訂「Source對象ID」時，請使用此目的地。

![目的地目錄中兩個PubMatic聯結器的並排檢視。](/help/destinations/assets/catalog/advertising/pubmatic/two-pubmatic-connectors-side-by-side.png)

>[!IMPORTANT]
>
> 目的地聯結器和檔案頁面是由[!DNL PubMatic]團隊建立和維護的。 若有任何查詢或更新要求，請直接透過`support@pubmatic.com`連絡他們。

## 使用案例 {#use-cases}

為協助您更清楚瞭解您應如何及何時使用[!DNL PubMatic Connect]目的地，以下是[!DNL Adobe Experience Platform]客戶可以使用此目的地解決的範例使用案例。

### 在行動、網頁和CTV平台上鎖定使用者 {#targeting}

發行者或資料提供者想要使用大量識別碼，將對象從[!DNL Adobe Experience Platform]傳送至[!DNL PubMatic Connect]，以鎖定行動、網頁及CTV平台上的使用者。

## 先決條件 {#prerequisites}

請洽詢您的[!DNL PubMatic]帳戶管理員，確定您的帳戶已正確設定，並支援對象區段的上線。 他們也會確保您擁有使用此目的地的所有相關詳細資料，並在設定期間為您提供支援。

## 支援的身分 {#supported-identities}

[!DNL PubMatic Connect]支援下表所述的身分啟用。 深入瞭解[身分](/help/identity-service/features/namespaces.md)。

| 目標身分 | 說明 | 考量事項 |
| --------------- | ------------------------ | ------------------------------------------------------------------------------- |
| GAID | GOOGLE ADVERTISING ID | 當您的來源身分是GAID名稱空間時，請選取GAID目標身分。 |
| IDFA | 廣告商適用的Apple ID | 當您的來源身分是IDFA名稱空間時，請選取IDFA目標身分。 |
| extern_id | 自訂使用者ID | 當您的來源身分是自訂名稱空間時，請選取此目標身分。 |

{style="table-layout:auto"}

## 支援的對象 {#supported-audiences}

本節說明您可以將哪些型別的對象匯出至此目的地。

| 對象來源 | 支援 | 說明 |
|---------|----------|----------|
| [!DNL Segmentation Service] | 是 | 透過Experience Platform [細分服務](../../../segmentation/home.md)產生的對象。 |
| 所有其他受眾來源 | 無 | 此類別包含透過[!DNL Segmentation Service]產生的對象以外的所有對象來源。 閱讀[各種對象來源](/help/segmentation/ui/audience-portal.md#customize)。 部分範例包括： <ul><li> 自訂上傳對象[從CSV檔案匯入](../../../segmentation/ui/audience-portal.md#import-audience)至Experience Platform，</li><li> 相似受眾， </li><li> 同盟對象， </li><li> 其他Experience Platform應用程式中產生的對象，例如[!DNL Adobe Journey Optimizer]、 </li><li> 及更多內容。 </li></ul> |

{style="table-layout:auto"}



依受眾資料型別支援的受眾：

| 對象資料型別 | 支援 | 說明 | 使用案例 |
|--------------------|-----------|-------------|-----------|
| [人員對象](/help/segmentation/types/people-audiences.md) | 是 | 根據客戶設定檔，可讓您針對行銷活動的特定人群進行定位。 | 經常購買者、購物車放棄者 |
| [帳戶對象](/help/segmentation/types/account-audiences.md) | 無 | 針對帳戶型行銷策略，鎖定特定組織內的個人。 | B2B行銷 |
| [潛在客戶對象](/help/segmentation/types/prospect-audiences.md) | 無 | 將目標定位為尚未成為客戶但與目標受眾具有相同特性的個人。 | 使用第三方資料進行勘探 |
| [資料集匯出](/help/catalog/datasets/overview.md) | 無 | 儲存在[!DNL Adobe Experience Platform]資料湖中的結構化資料集合。 | 報告、資料科學工作流程 |

{style="table-layout:auto"}


## 匯出型別和頻率 {#export-type-frequency}

請參閱下表以取得目的地匯出型別和頻率的資訊。

| 項目 | 類型 | 附註 |
| ---------------- | ------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 匯出類型 | **[!UICONTROL Segment export]** | 您正在匯出區段（對象）的所有成員，而這些區段具有PubMatic Connect目的地所使用的識別碼（名稱、電話號碼或其他）。 |
| 匯出頻率 | **[!UICONTROL Streaming]** | 串流目的地是「一律開啟」的API型連線。 當根據區段評估在Experience Platform中更新設定檔時，聯結器會將更新傳送至下游的目標平台。 深入瞭解[串流目的地](/help/destinations/destination-types.md#streaming-destinations)。 |

{style="table-layout:auto"}

## 連線到目標 {#connect}

>[!IMPORTANT]
>
> 若要連線到目的地，您需要&#x200B;**[!UICONTROL Manage Destinations]** [存取控制許可權](/help/access-control/home.md#permissions)。 閱讀[存取控制總覽](/help/access-control/ui/overview.md)或連絡您的產品管理員以取得必要的許可權。

若要連線到此目的地，請依照[目的地組態教學課程](../../ui/connect-destination.md)中所述的步驟進行。 在目標設定工作流程中，填寫以下兩個區段中列出的欄位。

### 驗證目標 {#authenticate}

若要驗證到目的地，請填寫必填欄位並選取&#x200B;**[!UICONTROL Connect to destination]**。

![如何驗證](../../assets/catalog/advertising/pubmatic/authenticate-destination.png)

- **[!UICONTROL Bearer token]**：填寫持有人權杖以驗證目的地。

### 填寫目標詳細資訊 {#destination-details}

若要設定目的地的詳細資訊，請填寫下方的必填和選用欄位。 UI中欄位旁的星號表示該欄位為必填欄位。

![目的地詳細資料](../../assets/catalog/advertising/pubmatic/destination-details.png)

- **[!UICONTROL Name]**：您日後可辨識此目的地的名稱。
- **[!UICONTROL Description]**：可協助您日後識別此目的地的說明。
- **[!UICONTROL Data partner ID]**：在您[!DNL PubMatic]帳戶中為此整合設定的資料合作夥伴ID。
- **[!UICONTROL Default country code]**：如果設定檔中未提供任何資料，應套用至所有身分的預設國家/地區代碼。
- **[!UICONTROL Account ID]**：您的[!DNL PubMatic Connect]帳戶識別碼。
- **[!UICONTROL Account type]**： [!DNL PubMatic]平台帳戶的帳戶型別。 如果您有任何選擇的問題，請洽詢您的[!DNL PubMatic]客戶經理。 可用的選項包括：
   - [!UICONTROL PUBLISHER]
   - [!UICONTROL DEMAND_PARTNER]
   - [!UICONTROL BUYER]

### 啟用警示 {#enable-alerts}

您可以啟用警報以接收有關傳送到您目的地的資料流狀態的通知。 從清單中選取警報以訂閱接收有關資料流狀態的通知。 如需警示的詳細資訊，請參閱[使用UI訂閱目的地警示](../../ui/alerts.md)的指南。

當您完成提供目的地連線的詳細資訊時，請選取&#x200B;**[!UICONTROL Next]**。

## 啟動此目標的對象 {#activate}

>[!IMPORTANT]
>
> - 若要啟用資料，您需要&#x200B;**[!UICONTROL View Destinations]**、**[!UICONTROL Activate Destinations]**、**[!UICONTROL View Profiles]**&#x200B;和&#x200B;**[!UICONTROL View Segments]** [存取控制許可權](/help/access-control/home.md#permissions)。 閱讀[存取控制總覽](/help/access-control/ui/overview.md)或連絡您的產品管理員以取得必要的許可權。
>
> - 若要匯出&#x200B;_身分_，您需要&#x200B;**[!UICONTROL View Identity Graph]** [存取控制許可權](/help/access-control/home.md#permissions)。<br> ![選取工作流程中反白的身分名稱空間，以啟用目的地的對象。](../../assets/overview/export-identities-to-destination.png "選取工作流程中反白顯示的身分名稱空間，以啟用目的地的對象。"){width="100" zoomable="yes"}

閱讀[啟用串流目的地的對象](/help/destinations/ui/activate-segment-streaming-destinations.md)，以取得啟用此目的地對象的指示。

### 對應屬性和身分 {#map}

選取來源欄位：

- 選取識別碼（通常是IDFA或自訂ID名稱空間等名稱空間）。

選取目標欄位：

- 請洽詢您的[!DNL PubMatic]帳戶管理員，以取得在此步驟中哪種UID型別將正確的資訊。
- 選取符合您在第一個步驟中選取的識別碼的[!DNL PubMatic UID]型別編號。

![對應屬性和身分](../..//assets/catalog/advertising/pubmatic/export-identities-to-destination.png)

### 對象排程 {#audience-scheduling}

如果您使用PubMatic Connect （自訂對象ID對應）目的地，則必須為對應至PubMatic平台中「Source對象ID」的每個對象提供對應ID。

![對象排程](../..//assets/catalog/advertising/pubmatic/audience-scheduling-mapping-id.png)

## 匯出的資料/驗證資料匯出 {#exported-data}

使用[!DNL PubMatic] UI檢查資料是否已正確推送，以及區段是否可用。 推播資料後，可能需要24小時才能更新[!DNL PubMatic] UI。

## 資料使用與控管 {#data-usage-governance}

處理您的資料時，所有[!DNL Adobe Experience Platform]目的地都符合資料使用原則。 如需[!DNL Adobe Experience Platform]如何強制資料控管的詳細資訊，請閱讀[資料控管概觀](/help/data-governance/home.md)。
