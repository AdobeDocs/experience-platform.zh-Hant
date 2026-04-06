---
title: Amazon Ads v2
description: Amazon Ads v2提供一系列選項，協助您為註冊賣家、廠商、圖書供應商、Kindle Direct Publishing (KDP)作者、應用程式開發人員或代理商達成廣告目標。 Amazon Ads v2與Adobe Experience Platform的整合提供與Amazon Ads產品的關鍵整合。
last-substantial-update: 2026-03-31T00:00:00Z
source-git-commit: 1e93c78b13159a2aed24d283e3768c670ad14097
workflow-type: tm+mt
source-wordcount: '1667'
ht-degree: 3%

---

# Amazon Ads v2連線 {#amazon-ads-v2}

## 概觀 {#overview}

[!DNL Amazon Ads v2]可讓廣告商有效率地擷取、管理、啟用及重複使用[!DNL Amazon Ads]產品的對象資料。

>[!IMPORTANT]
>
>[!DNL Amazon Ads v2]是所有新[!DNL Amazon Ads]連線的目前目的地。 如果您有現有的[（舊版） [!DNL Amazon Ads]](./amazon-ads.md)連線，它將繼續運作，而不會進行任何必要的變更。 [!DNL Amazon Ads v2]連線到[!DNL Ads Data Manager]，後者支援擴充的身分型別、位址相關欄位，以及跨[!DNL Amazon Ads]個產品的資料共用，相較於[ （舊版） [!DNL Amazon Ads]](./amazon-ads.md)改善鎖定目標和對象符合率。
>
>2026年4月底後，[!DNL Amazon Ads v2]將重新命名為[!DNL Amazon Ads]，舊版卡片將隱藏，在目錄中保留單一目的地卡片。 現有的舊版資料流將繼續運作，而您可以在該日期之後的&#x200B;**[!UICONTROL Browse]**&#x200B;索引標籤中管理這些資料流。

與[!DNL Amazon Ads v2]的[!DNL Adobe Experience Platform]整合提供直接連線，可將對象成員擷取到[!DNL Amazon Ads]。 上傳的對象可在[!DNL Ads Data Manager (ADM)]內的[!DNL Amazon Ads]主控台中使用。 您可以使用[!DNL Ads Data Manager]主控台，在不同的[!DNL Amazon Ads]產品之間共用資料。

若要進一步瞭解[!DNL Ads Data Manager]，請參閱：

* [廣告資料管理員 — 主控台總覽](https://advertising.amazon.com/API/docs/en-us/adm/1_ads-data-manager-console-overview)
* [使用Ads Data Manager主控台](https://advertising.amazon.com/API/docs/en-us/adm/2_ads-data-manager-console)
* Ads資料管理員中的[帳戶設定](https://advertising.amazon.com/API/docs/en-us/adm/2a_ads-data-manager_account_setup)

>[!IMPORTANT]
>
>此目的地聯結器和檔案頁面是由&#x200B;*[!DNL Amazon Ads]*&#x200B;團隊建立和維護。 若有任何查詢或更新要求，請直接在&#x200B;*`amc-support@amazon.com`.*&#x200B;聯絡他們

## 使用案例 {#use-cases}

為協助您更清楚瞭解您應如何及何時使用[!DNL Amazon Ads v2]目的地，以下是[!DNL Adobe Experience Platform]客戶可以使用此目的地解決的範例使用案例。

### 對象擷取與啟用 {#activation-and-targeting}

運動服裝品牌想要透過[!DNL Amazon Ads]的相關廣告觸及其現有客戶。 品牌可從其CRM擷取客戶電子郵件地址至[!DNL Adobe Experience Platform]、使用其第一方離線資料建立對象，以及透過[!DNL Amazon Ads]目的地啟用這些對象至[!DNL Amazon Ads v2]。 啟用後，您可以使用這些對象來定位跨[!DNL Amazon Ads]詳細目錄之客戶的廣告，協助品牌重新與已知客戶互動並促進重複購買。 若要深入瞭解，請參閱[管理資料](https://advertising.amazon.com/API/docs/en-us/adm/6_adm-manage-data)。

## 先決條件 {#prerequisites}

若要使用[!DNL Amazon Ads v2]與[!DNL Adobe Experience Platform]的連線，您必須使用&#x200B;**[!DNL Amazon Ads Data Manager]**&#x200B;管理員帳戶[存取](https://advertising.amazon.com/help/G69CDSR9MNSWJH95)。 如需詳細資訊，請參閱[開始使用Amazon Ads Data Manager](https://advertising.amazon.com/API/docs/en-us/adm/1_ads-data-manager-console-overview)。

### 接受Amazon Ads Data Manager條款與條件 {#accept-terms}

在設定[!DNL Amazon Ads v2]目的地之前，請登入您的[!DNL Amazon Ads]帳戶並接受[!DNL Ads Data Manager]條款與條件。 導覽至[!DNL Ads Data Manager]內的[!DNL Amazon Ads]主控台，並在出現提示時接受條款。 如果您不接受條款與條件，則不會在[!DNL Amazon Ads]中建立對象。

## 支援的身分 {#supported-identities}

[!DNL Amazon Ads v2]目的地支援啟用下列身分。 深入瞭解[身分](/help/identity-service/features/namespaces.md)。

| 目標身分 | 說明 | 考量事項 |
|---|---|---|
| `phone` | 使用SHA256演演算法雜湊的電話號碼 | [!DNL Adobe Experience Platform]同時支援純文字和SHA256雜湊電話號碼。 當您的來源欄位包含未雜湊的屬性時，請核取&#x200B;**[!UICONTROL Apply transformation]**&#x200B;選項，讓[!DNL Experience Platform]在啟用時自動雜湊資料。 |
| `email` | 使用SHA256演演算法雜湊的電子郵件地址（小寫） | [!DNL Adobe Experience Platform]同時支援純文字和SHA256雜湊電子郵件地址。 當您的來源欄位包含未雜湊的屬性時，請核取&#x200B;**[!UICONTROL Apply transformation]**&#x200B;選項，讓[!DNL Experience Platform]在啟用時自動雜湊資料。 |
| `firstname` | 使用者的名字 | [!DNL Adobe Experience Platform]同時支援純文字和SHA256雜湊名字。 當您的來源欄位包含未雜湊的屬性時，請核取&#x200B;**[!UICONTROL Apply transformation]**&#x200B;選項，讓[!DNL Experience Platform]在啟用時自動雜湊資料。 |
| `lastname` | 使用者的姓氏 | [!DNL Adobe Experience Platform]同時支援純文字和SHA256雜湊姓氏。 當您的來源欄位包含未雜湊的屬性時，請核取&#x200B;**[!UICONTROL Apply transformation]**&#x200B;選項，讓[!DNL Experience Platform]在啟用時自動雜湊資料。 |
| `address` | 使用者的街道地址 | [!DNL Adobe Experience Platform]支援純文字和SHA256雜湊街道。 當您的來源欄位包含未雜湊的屬性時，請核取&#x200B;**[!UICONTROL Apply transformation]**&#x200B;選項，讓[!DNL Experience Platform]在啟用時自動雜湊資料。 |
| `city` | 使用者的城市 | [!DNL Adobe Experience Platform]同時支援純文字和SHA256雜湊城市。 當您的來源欄位包含未雜湊的屬性時，請核取&#x200B;**[!UICONTROL Apply transformation]**&#x200B;選項，讓[!DNL Experience Platform]在啟用時自動雜湊資料。 |
| `state` | 使用者的州或省 | [!DNL Adobe Experience Platform]同時支援純文字和SHA256雜湊狀態。 當您的來源欄位包含未雜湊的屬性時，請核取&#x200B;**[!UICONTROL Apply transformation]**&#x200B;選項，讓[!DNL Experience Platform]在啟用時自動雜湊資料。 |
| `zip` | 使用者的郵遞區號 | [!DNL Adobe Experience Platform]同時支援純文字和SHA256雜湊ZIP。 當您的來源欄位包含未雜湊的屬性時，請核取&#x200B;**[!UICONTROL Apply transformation]**&#x200B;選項，讓[!DNL Experience Platform]在啟用時自動雜湊資料。 |
| `countryCode` | 使用者的國家/地區（2個字元的ISO代碼） | 支援純文字輸入。 |
| `experianId` | 由[!DNL Experian]指派的識別碼 | 支援純文字輸入。 |
| `kantarId` | 由[!DNL Kantar]指派的識別碼 | 支援純文字輸入。 |
| `liveRampId` | 由[!DNL LiveRamp]指派的識別碼 | 支援純文字輸入。 |
| `maId` | 行動應用程式指派的識別碼 | 支援純文字輸入。 |
| `merkleId` | 由[!DNL Merkle]指派的識別碼 | 支援純文字輸入。 |
| `neustarId` | 由[!DNL Neustar]指派的識別碼 | 支援純文字輸入。 |
| `realId` | 由真實ID身分圖表指派的識別碼 | 支援純文字輸入。 |
| `sambaTvId` | 由[!DNL Samba TV]指派的識別碼 | 支援純文字輸入。 |

{style="table-layout:auto"}

## 支援的對象 {#supported-audiences}

本節說明您可以將哪些型別的對象匯出至此目的地。

| 對象來源 | 支援 | 說明 |
|---------|----------|----------|
| [!DNL Segmentation Service] | 是 | 透過[!DNL Experience Platform] [細分服務](/help/segmentation/home.md)產生的對象。 |
| 所有其他受眾來源 | 是 | 此類別包含透過[!DNL Segmentation Service]產生的對象以外的所有對象來源。 閱讀[各種對象來源](/help/segmentation/ui/audience-portal.md#customize)。 部分範例包括： <ul><li> 自訂上傳對象[從CSV檔案匯入](/help/segmentation/ui/audience-portal.md#import-audience)至[!DNL Experience Platform]，</li><li> 相似受眾， </li><li> 同盟對象， </li><li> 在其他[!DNL Experience Platform]應用程式（例如[!DNL Adobe Journey Optimizer]）中產生的對象 </li><li> 及更多內容。 </li></ul> |

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

下表說明目的地匯出型別和頻率。

| 項目 | 類型 | 附註 |
| ---------|----------|---------|
| 匯出類型 | **[!UICONTROL Audience export]** | 您正在匯出具有[!DNL Amazon Ads]支援之識別碼的受眾的所有成員。 |
| 匯出頻率 | **[!UICONTROL Streaming]** | 串流目的地是「一律開啟」的API型連線。 [!DNL Experience Platform]中的對象更新會立即傳送到[!DNL Ads Data Manager]。 |

{style="table-layout:auto"}

## 連線到目標 {#connect}

>[!IMPORTANT]
>
>若要連線到目的地，您需要&#x200B;**[!UICONTROL View Destinations]**&#x200B;和&#x200B;**[!UICONTROL Manage Destinations]** [存取控制許可權](/help/access-control/home.md#permissions)。 閱讀[存取控制總覽](/help/access-control/ui/overview.md)或連絡您的產品管理員以取得必要的許可權。

若要連線到此目的地，請依照[目的地組態教學課程](/help/destinations/ui/connect-destination.md)中所述的步驟進行。 在目標設定工作流程中，填寫以下兩個區段中列出的欄位。

### 驗證目標 {#authenticate}

若要驗證到目的地，請填寫必填欄位並選取&#x200B;**[!UICONTROL Connect to destination]**。

* **[!UICONTROL Account name]**：輸入可協助您識別此目的地帳戶的名稱。 如果您有多個連線連至同一目標，這個做法尤其實用。
* **[!UICONTROL Description]** （選用）：新增詳細資料以協助您或您的團隊區分帳戶，例如連線的目的或相關的業務內容。

![在Experience Platform中為Amazon Ads連線到目的地對話方塊](../../assets/catalog/advertising/amazon-ads/amazon-ads-v2-connect-to-destination.png)

系統已將您重新導向至[!DNL Amazon Ads v2]介面。 選取&#x200B;**[!UICONTROL Allow]**&#x200B;以登入您的Amazon帳戶。

![要求使用者允許的Amazon Ads OAuth授權提示](../../assets/catalog/advertising/amazon-ads/amazon-ads-v2-allow.png)

驗證之後，您會重新導向回[!DNL Adobe Experience Platform]，並使用新連線。

### 填寫目標詳細資訊 {#destination-details}

若要設定目的地的詳細資訊，請填寫下方的必填和選用欄位。 UI中欄位旁的星號表示該欄位為必填欄位。

Experience Platform中的![Amazon Ads v2目的地設定欄位](../../assets/catalog/advertising/amazon-ads/amazon-ads-v2-configure-destination.png)

* **[!UICONTROL Name]**：識別此目的地的名稱。
* **[!UICONTROL Description]**：可協助您識別此目的地的說明。
* **[!UICONTROL Manager Account]**：下拉式清單中的目標管理員帳戶ID。
* **[!UICONTROL All audience members sent to Amazon are consented for use for Advertising]**：指定資料使用的同意（`GRANTED`或`DENIED`）。
* **[!UICONTROL Ads data manager Terms & Conditions]**：接受[!DNL Amazon Ads]資料管理員條款與條件。 閱讀[接受條款](#accept-terms)章節以取得詳細資料。

### 啟用警示 {#enable-alerts}

您可以啟用警報以接收有關傳送到您目的地的資料流狀態的通知。 從清單中選取警報以訂閱接收有關資料流狀態的通知。 如需警示的詳細資訊，請參閱[使用UI訂閱目的地警示](/help/destinations/ui/alerts.md)的指南。

當您完成提供目的地連線的詳細資訊時，請選取&#x200B;**[!UICONTROL Next]**。

## 啟動此目標的對象 {#activate}

>[!IMPORTANT]
>
>* 若要啟用資料，您需要&#x200B;**[!UICONTROL View Destinations]**、**[!UICONTROL Activate Destinations]**、**[!UICONTROL View Profiles]**&#x200B;和&#x200B;**[!UICONTROL View Segments]** [存取控制許可權](/help/access-control/home.md#permissions)。 閱讀[存取控制總覽](/help/access-control/ui/overview.md)或連絡您的產品管理員以取得必要的許可權。
>* 若要匯出身分，您需要&#x200B;**[!UICONTROL View Identity Graph]** [存取控制許可權](/help/access-control/home.md#permissions)。<br> ![選取工作流程中反白的身分名稱空間，以啟用目的地的對象。](/help/destinations/assets/overview/export-identities-to-destination.png "選取工作流程中反白顯示的身分名稱空間，以啟用目的地的對象。"){width="100" zoomable="yes"}

閱讀[將設定檔和對象啟用至串流對象匯出目的地](/help/destinations/ui/activate-segment-streaming-destinations.md)，以瞭解啟用此目的地對象的指示。

### 強制對應 {#map}

[!DNL Amazon Ads v2]目的地需要您設定下列對應才能成功啟用資料。

| 來源欄位 | 目標欄位 | 說明 |
|---------|----------|---------|
| `IdentityMap: Email_LC_SHA256`或 `IdentityMap: Email` | `Identity: email` | 當您的來源欄位包含未雜湊的屬性時，請核取&#x200B;**[!UICONTROL Apply transformation]**&#x200B;選項，讓[!DNL Experience Platform]在啟用時自動雜湊資料。 |
| `xdm: homeAddress.countryCode` | `Identity: countryCode` | 使用者的國家/地區（2個字元的ISO代碼） |

Amazon Ads v2目的地的![身分欄位對應設定](../../assets/catalog/advertising/amazon-ads/amazon-ads-v2-mapping.png)

### 對應最佳實務 {#mapping-best-practices}

結合第一方識別碼（例如電話號碼和地址）與合作夥伴提供的識別碼。 這可讓[!DNL Amazon Ads]在對象比對期間使用多個身分識別訊號，進而提高比對率。

只有在來源資料中填入合作夥伴提供的識別碼時，才使用這些識別碼。 如果特定設定檔的對應合作夥伴識別碼欄位空白或不存在，則會在對象比對期間忽略該欄位，且不會影響比對率。

### 範例 {#examples}

* 啟用使用`kantarId`身分資料建立或擴充的對象時，請使用[!DNL Kantar]。
* 當您的對象資料來自`merkleId`受管理的身分解決方案時，請使用[!DNL Merkle]。
* 當您的資料是透過`neustarId`身分解析連結時，請使用[!DNL Neustar]。
* 針對使用`experianId`身分資料擴充的受眾，使用[!DNL Experian]。
* 啟用依賴`liveRampId`身分解析的受眾時使用[!DNL LiveRamp]。
* 使用`sambaTvId`提供的對象資料時使用[!DNL Samba TV]。

這些識別碼通常由各自的合作夥伴以純文字識別碼的形式提供，不需要雜湊處理。

## 驗證資料匯出 {#exported-data}

啟用後，請在&#x200B;**[!DNL Ads Data Manager]主控台**&#x200B;中驗證您的對象擷取。

導覽至&#x200B;**[!UICONTROL Audiences]** → **[!UICONTROL Uploaded Sources]**。 檢查您的對象擷取狀態、大小和任何錯誤記錄。 [檔案中的](https://advertising.amazon.com/API/docs/en-us/adm/6_adm-manage-data)管理資料[和](https://advertising.amazon.com/API/docs/en-us/adm/7_adm-destinations)目的地[!DNL Amazon Ads]頁面提供進一步的驗證指引。

## 資料使用與控管 {#data-usage-governance}

處理您的資料時，所有[!DNL Adobe Experience Platform]目的地都符合資料使用原則。 如需[!DNL Adobe Experience Platform]如何強制資料控管的詳細資訊，請閱讀[資料控管概觀](/help/data-governance/home.md)。

## 其他資源 {#additional-resources}

如需[!DNL Amazon Ads Data Manager]的詳細資訊，請參閱下列資源：

* [Amazon Ads資料管理員概觀](https://advertising.amazon.com/API/docs/en-us/adm/1_ads-data-manager-console-overview)
