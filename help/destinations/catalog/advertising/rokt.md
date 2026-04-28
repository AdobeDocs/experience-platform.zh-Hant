---
title: 洛克
description: 瞭解如何將Adobe Experience Platform受眾連結至Rokt，以透過更聰明的鎖定目標、抑制和個人化來改善行銷活動績效。
source-git-commit: a281a7c961b8576105913feb7a7f8258c975e875
workflow-type: tm+mt
source-wordcount: '1235'
ht-degree: 4%

---


# [!DNL Rokt] 連線 {#rokt-destination}

## 概觀 {#overview}

[[!DNL Rokt]](https://www.rokt.com)會使用AI驅動的即時決策在電子商務中解除鎖定值，讓每個交易時刻更™相關。 它提供個人化體驗，並將廣告商與高意圖客戶連結在一起。 將[!DNL Adobe Experience Platform]個對象連線到[!DNL Rokt]，以透過更聰明的鎖定目標、隱藏和個人化來改善行銷活動績效。 在適當的時間與適當的客戶接觸，同時減少浪費的支出。

>[!IMPORTANT]
>
>目的地聯結器和檔案頁面是由[!DNL Rokt]團隊建立和維護的。 如有任何查詢或更新要求，請連絡您的[!DNL Rokt]客戶經理，或連絡`support@rokt.com`。

## 使用案例 {#use-cases}

下列使用案例顯示[!DNL Experience Platform]客戶如何使用[!DNL Rokt]目的地。

### 使用案例#1：重新目標定位 {#use-case-1}

重新與造訪您的網站或應用程式但未轉換的高意圖客戶互動。 在[!DNL Experience Platform]中建立對象，包括瀏覽特定產品類別或放棄結帳流程的使用者。 接著將該對象推送至[!DNL Rokt]，以便在合作夥伴網站上的購買點提供個人化優惠方案。 [!DNL Rokt]會在交易時間內運作，在客戶於其他地方完成購買後立即執行。 當購買意圖達到尖峰時，就會達到重新定位的對象，進而帶來比傳統顯示重新定位更高的轉換率。

### 使用案例#2：隱藏清單 {#use-case-2}

抑制不應收到特定[!DNL Rokt]選件的對象，以避免浪費支出和無關體驗。 常見的抑制使用案例包括排除最近的轉換者、進行中促銷的忠誠會員，或選擇退出行銷的使用者。 例如，排除過去30天內購買的客戶。 即時將這些隱藏對象從[!DNL Experience Platform]同步到[!DNL Rokt]。 這能讓行銷活動持續聚焦於全新或重新參與的使用者。 這可以提高ROI並保護客戶體驗。

## 先決條件 {#prerequisites}

在[!DNL Adobe Experience Platform]中設定[!DNL Rokt]目的地之前，您必須先從您的&#x200B;**[!DNL Rokt]帳戶管理員**&#x200B;取得下列認證：

* **API金鑰**：在[驗證目的地連線](#authenticate)時，請將此金鑰用作&#x200B;**[!UICONTROL Username]**。
* **API密碼**：在[驗證目的地連線](#authenticate)時，請將此項當作&#x200B;**[!UICONTROL Password]**。

在設定前，您的[!DNL Rokt]帳戶管理員將在[!DNL Rokt]平台中布建這些認證。 如果您尚未收到通知，請聯絡客戶經理。

## 支援的身分 {#supported-identities}

[!DNL Rokt]支援下表所述的身分啟用。 深入瞭解[身分](/help/identity-service/features/namespaces.md)。

| 目標身分 | 說明 | 考量事項 |
|---|---|---|
| 電子郵件 | 純文字電子郵件地址 | 建議使用。 用於[!DNL Rokt]中的設定檔比對。 |
| email_lc_sha256 | 使用SHA256演演算法雜湊的電子郵件地址 | 支援純文字和SHA256雜湊電子郵件地址。 當您的來源欄位包含未雜湊的屬性時，請選取&#x200B;**[!UICONTROL Apply transformation]**&#x200B;選項，讓[!DNL Experience Platform]在啟用時自動雜湊資料。 |
| 電話 | 純文字電話號碼 | 用於[!DNL Rokt]中的設定檔比對。 |
| phone_sha256 | 使用SHA256演演算法雜湊的電話號碼 | 支援純文字和SHA256雜湊電話號碼。 當您的來源欄位包含未雜湊的屬性時，請選取&#x200B;**[!UICONTROL Apply transformation]**&#x200B;選項，讓[!DNL Experience Platform]在啟用時自動雜湊資料。 |
| GAID | [!DNL Google] Advertising ID | 當您的來源身分是GAID名稱空間時，請選取GAID目標身分。 |
| IDFA | 廣告商的[!DNL Apple] ID | 當您的來源身分是IDFA名稱空間時，請選取IDFA目標身分。 |
| aepProfileId | [!DNL Adobe Experience Platform]設定檔識別碼 | 將設定檔識別碼(`xdm:_id`)對應為遞補識別碼。 |

{style="table-layout:auto"}

## 支援的對象 {#supported-audiences}

本節說明您可以將哪些型別的對象匯出至此目的地。

| 對象來源 | 支援 | 說明 |
|---------|----------|----------|
| [!DNL Segmentation Service] | 是 | 透過[!DNL Experience Platform] [[!DNL Segmentation Service]](/help/segmentation/home.md)產生的對象。 |
| 所有其他受眾來源 | 是 | 此類別包含透過[!DNL Segmentation Service]產生的對象以外的所有對象來源。 閱讀[各種對象來源](/help/segmentation/ui/audience-portal.md#customize)。 部分範例包括： <ul><li> 自訂上傳對象[從CSV檔案匯入](/help/segmentation/ui/audience-portal.md#import-audience)至[!DNL Experience Platform]，</li><li> 相似受眾， </li><li> 同盟對象， </li><li> 在其他[!DNL Experience Platform]應用程式（例如[!DNL Adobe Journey Optimizer]）中產生的對象 </li><li> 及更多內容。 </li></ul> |

{style="table-layout:auto"}

依受眾資料型別支援的受眾：

| 對象資料型別 | 支援 | 說明 | 使用案例 |
|--------------------|-----------|-------------|-----------|
| [人員對象](/help/segmentation/types/people-audiences.md) | 是 | 根據客戶設定檔。 使用這些來針對特定人群進行行銷活動。 | 經常購買者、購物車放棄者 |
| [帳戶對象](/help/segmentation/types/account-audiences.md) | 無 | 針對帳戶型行銷策略，鎖定特定組織內的個人。 | B2B行銷 |
| [潛在客戶對象](/help/segmentation/types/prospect-audiences.md) | 無 | 將目標定位為尚未成為客戶但與目標受眾具有相同特性的個人。 | 使用第三方資料進行勘探 |
| [資料集匯出](/help/catalog/datasets/overview.md) | 無 | 儲存在[!DNL Adobe Experience Platform]資料湖中的結構化資料集合。 | 報告、資料科學工作流程 |

{style="table-layout:auto"}

## 匯出型別和頻率 {#export-type-frequency}

請參閱下表以取得目的地匯出型別和頻率的資訊。

| 項目 | 類型 | 附註 |
|---------|----------|---------|
| 匯出類型 | **[!UICONTROL Audience export]** | 您正在匯出具有[!DNL Rokt]目的地中所使用識別碼（電子郵件、電話、行動廣告ID或其他）的對象的所有成員。 |
| 匯出頻率 | **[!UICONTROL Streaming]** | 串流目的地是「一律開啟」的API型連線。 一旦根據對象評估在[!DNL Experience Platform]中更新設定檔，聯結器就會將更新傳送至下游的[!DNL Rokt]。 深入瞭解[串流目的地](/help/destinations/destination-types.md#streaming-destinations)。 |

{style="table-layout:auto"}

## 連線到目標 {#connect}

>[!IMPORTANT]
>
>若要連線到目的地，您需要&#x200B;**[!UICONTROL View Destinations]**&#x200B;和&#x200B;**[!UICONTROL Manage Destinations]** [存取控制許可權](/help/access-control/home.md#permissions)。 閱讀[存取控制總覽](/help/access-control/ui/overview.md)或連絡您的產品管理員以取得必要的許可權。

若要連線到此目的地，請依照[目的地組態教學課程](/help/destinations/ui/connect-destination.md)中所述的步驟進行。 在設定目標工作流程中，填寫以下兩個區段中列出的欄位。

### 驗證目標 {#authenticate}

若要驗證到目的地，請填寫必填欄位並選取&#x200B;**[!UICONTROL Connect to destination]**。

* **[!UICONTROL Username]**：您的API金鑰，由您的[!DNL Rokt]帳戶管理員提供。
* **[!UICONTROL Password]**：您的API機密，由您的[!DNL Rokt]帳戶管理員提供。

  ![ [!DNL Experience Platform]中的[!DNL Rokt]目的地設定畫面，已填入帳戶詳細資料、驗證欄位和目的地詳細資料。](/help/destinations/assets/catalog/advertising/rokt/aep-configure-destination.png)

### 填寫目標詳細資訊 {#destination-details}

若要設定目的地的詳細資訊，請填寫下方的必填和選用欄位。 UI中欄位旁的星號表示該欄位為必填欄位。

* **[!UICONTROL Name]**：您日後可辨識此目的地的名稱（例如「[!DNL Rokt] — 重新鎖定受眾」）。
* **[!UICONTROL Description]**：可協助您日後識別此目的地的說明。

### 啟用警示 {#enable-alerts}

您可以啟用警報以接收有關傳送到您目的地的資料流狀態的通知。 從清單中選取警報以訂閱接收有關資料流狀態的通知。 如需警示的詳細資訊，請參閱[使用UI訂閱目的地警示](/help/destinations/ui/alerts.md)的指南。

當您完成提供目的地連線的詳細資訊時，請選取&#x200B;**[!UICONTROL Next]**。

## 啟動此目標的對象 {#activate}

>[!IMPORTANT]
>
>* 若要啟用資料，您需要&#x200B;**[!UICONTROL View Destinations]**、**[!UICONTROL Activate Destinations]**、**[!UICONTROL View Profiles]**&#x200B;和&#x200B;**[!UICONTROL View Segments]** [存取控制許可權](/help/access-control/home.md#permissions)。 閱讀[存取控制總覽](/help/access-control/ui/overview.md)或連絡您的產品管理員以取得必要的許可權。
>* 若要匯出&#x200B;*身分*，您需要&#x200B;**[!UICONTROL View Identity Graph]** [存取控制許可權](/help/access-control/home.md#permissions)。<br> ![選取工作流程中反白的身分名稱空間，以啟用目的地的對象。](/help/destinations/assets/overview/export-identities-to-destination.png "選取工作流程中反白顯示的身分名稱空間，以啟用目的地的對象。"){width="100" zoomable="yes"}

閱讀[將設定檔和對象啟用至串流對象匯出目的地](/help/destinations/ui/activate-segment-streaming-destinations.md)，以瞭解啟用此目的地對象的指示。

### 對應屬性和身分 {#map}

[!DNL Rokt]目的地支援從[!DNL Experience Platform]到[!DNL Rokt]識別欄位的識別名稱空間對應。 您必須至少對應一個身分，才能成功啟用對象。 建議的對應如下表所示。

| 來源欄位 | 目標欄位 | 考量事項 |
|---|---|---|
| `IdentityMap: Email` | `Identity: email` | 建議 |
| `IdentityMap: Email_LC_SHA256` | `Identity: emailSha256` | 建議 |
| `IdentityMap: Phone` | `Identity: phone` | 選填 |
| `IdentityMap: Phone_SHA256` | `Identity: phoneSha256` | 選填 |
| `IdentityMap: GAID` | `Identity: gaid` | 選填 |
| `IdentityMap: IDFA` | `Identity: idfa` | 選填 |
| `xdm: _id` | `Identity: aepProfileId` | 選填 |

{style="table-layout:auto"}

以下為完整對應的範例：

![ [!DNL Experience Platform]中[!DNL Rokt]目的地啟用工作流程的對應步驟，已設定來源與目標識別欄位。](/help/destinations/assets/catalog/advertising/rokt/aep-identity-mapping.png)

>[!NOTE]
>
>強烈建議至少有一個電子郵件型身分對應（`email`或`emailSha256`），以在[!DNL Rokt]中最大化符合率。

### 設定對象排程 {#audience-schedule}

完成對應步驟後，為每個選取的對象設定對象排程。 提供&#x200B;**[!UICONTROL Start date]**&#x200B;以確認對象應何時開始同步，並提供&#x200B;**[!UICONTROL Mapping ID]** （在[!DNL Rokt]內用來識別此對象的標籤）。 您可以使用[!DNL Experience Platform]對象名稱或有助於您和您的[!DNL Rokt]客戶經理識別對象的任何描述性字串。

## 資料使用與控管 {#data-usage-governance}

處理您的資料時，所有[!DNL Experience Platform]目的地都符合資料使用原則。 如需[!DNL Experience Platform]如何強制資料控管的詳細資訊，請閱讀[資料控管概觀](/help/data-governance/home.md)。

## 其他資源 {#additional-resources}

* [[!DNL Rokt]開發人員檔案](https://docs.rokt.com)
* [Adobe Experience Platform目的地概觀](/help/destinations/home.md)
