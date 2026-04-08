---
title: Reddit自訂對象
description: Reddit Ads將品牌與積極探索其激情和問題的使用者即時聯絡起來。 Reddit Ads將高意圖、社群導向的對話與彈性的廣告格式及強大的目標鎖定相結合，有助於廣告商觸及參與的對象、推動績效結果，並直接從塑造線上文化的社群中學習。 本指南適用於使用Adobe Experience Platform將受眾傳送至Reddit廣告的廣告商和媒體團隊。 它涵蓋連線帳戶、對應身分和啟用對象所需的專案。
last-substantial-update: 2026-03-31T00:00:00Z
exl-id: bcce02bd-d508-47a0-8f5c-bf162db1859d
badgeBeta: label="Beta" type="Informative"
source-git-commit: 28bbad7ccbec0b669082658b912d0b52e0374667
workflow-type: tm+mt
source-wordcount: '1231'
ht-degree: 4%

---

# [!DNL Reddit Custom Audience] 連線 {#reddit-custom-audience-connection}

## 概觀 {#overview}

[!DNL Reddit Ads]將品牌與主動探索其激情和問題的人員即時連結。 透過搭配高意圖、社群導向的對話與彈性的廣告格式和強大的目標定位，[!DNL Reddit Ads]可幫助廣告商觸及參與的對象、推動績效結果，並直接從塑造線上文化的社群中學習。

本指南適用於使用[!DNL Adobe Experience Platform]將對象傳送至[!DNL Reddit Ads]的廣告商和媒體團隊。 它涵蓋連線帳戶、對應身分和啟用對象所需的專案。

>[!IMPORTANT]
>
>此目的地聯結器和檔案頁面是由[!DNL Reddit]團隊建立和維護。 若有任何查詢或更新要求，請直接透過<adsapi-partner-support@reddit.com>連絡他們。

## 使用案例 {#use-cases}

為協助您更清楚瞭解您應如何及何時使用[!DNL Reddit Custom Audience]目的地，以下是[!DNL Adobe Experience Platform]客戶可以使用此目的地解決的範例使用案例。

### 透過個人化優惠重新鎖定現有客戶 {#use-case-1}

線上retailer想要透過社交平台觸及現有客戶，並根據他們先前的訂單向他們顯示個人化優惠。 線上retailer可以從自己的CRM將電子郵件地址和裝置ID （IDFA和GAID）擷取到[!DNL Adobe Experience Platform]、從自己的離線資料建立對象，並將這些對象傳送到[!DNL Reddit Ads]，以最佳化其廣告支出。

## 先決條件 {#prerequisites}

在設定此目的地之前，請確定您符合下列先決條件：

* 允許使用自訂對象和客戶清單的[!DNL Reddit Ads]帳戶。
* 授權連線的許可權。 這必須是可以登入[!DNL Reddit]並核准[!DNL Experience Platform]存取許可權的使用者，才能代表廣告帳戶管理對象。
* 您的[!DNL Reddit]廣告帳戶ID：建立受眾之廣告帳戶的識別碼。 您可以在[帳戶](https://ads.reddit.com/accounts)中找到您的廣告帳戶識別碼。 例如: `a2_1b2c34d`。

## 支援的身分 {#supported-identities}

[!DNL Reddit Custom Audience]支援下表所述的身分啟用。 深入瞭解[身分](/help/identity-service/features/namespaces.md)。

| 目標身分 | 說明 | 考量事項 |
| --- | --- | --- |
| email_lc_sha256 | 使用SHA256演演算法雜湊的電子郵件地址 | [!DNL Adobe Experience Platform]同時支援純文字和SHA256雜湊電子郵件地址。 當您的來源欄位包含未雜湊的屬性時，請核取&#x200B;**[!UICONTROL Apply transformation]**&#x200B;選項，讓[!DNL Platform]在啟用時自動雜湊資料。 |
| 女傭 | 廣告商的Google Advertising ID或Apple ID，兩者都使用SHA256演演算法執行雜湊處理 | 將GAID或IDFA對應至&#x200B;**maid**。 當您的來源欄位包含未雜湊的屬性時，請核取&#x200B;**[!UICONTROL Apply transformation]**&#x200B;選項，讓[!DNL Platform]在啟用時自動雜湊資料。 |

{style="table-layout:auto"}

## 支援的對象 {#supported-audiences}

本節說明您可以將哪些型別的對象匯出至此目的地。

| 對象來源 | 支援 | 說明 |
| --- | --- | --- |
| [!DNL Segmentation Service] | 是 | 透過[!DNL Experience Platform] [細分服務](../../../segmentation/home.md)產生的對象。 |
| 所有其他受眾來源 | 是 | 此類別包含透過細分服務產生的對象以外的所有對象來源。 閱讀[各種對象來源](/help/segmentation/ui/audience-portal.md#customize)。 |

{style="table-layout:auto"}

依資料型別區分的支援對象：

| 對象資料型別 | 支援 | 說明 | 使用案例 |
| --- | --- | --- | --- |
| [人員對象](/help/segmentation/types/people-audiences.md) | 是 | 根據客戶設定檔，可讓您針對行銷活動的特定人群進行定位。 | 經常購買者、購物車放棄者 |
| [帳戶對象](/help/segmentation/types/account-audiences.md) | 無 | 針對帳戶型行銷策略，鎖定特定組織內的個人。 | B2B行銷 |
| [潛在客戶對象](/help/segmentation/types/prospect-audiences.md) | 無 | 將目標定位為尚未成為客戶但與目標受眾具有相同特性的個人。 | 使用第三方資料進行勘探 |
| [資料集匯出](/help/catalog/datasets/overview.md) | 無 | 儲存在[!DNL Adobe Experience Platform]資料湖中的結構化資料集合。 | 報告、資料科學工作流程 |

{style="table-layout:auto"}

## 匯出型別和頻率 {#export-type-frequency}

請參閱下表以取得目的地匯出型別和頻率的資訊。

| 項目 | 類型 | 附註 |
| --- | --- | --- |
| 匯出類型 | **[!UICONTROL Audience export]** | 您正在匯出具有[!DNL Reddit Custom Audience]目的地中所使用識別碼（名稱、電話號碼或其他）的對象的所有成員。 |
| 匯出頻率 | **[!UICONTROL Streaming]** | 串流目的地是「一律開啟」的API型連線。 根據對象評估在Experience Platform中更新設定檔後，聯結器會立即將更新傳送至下游的目標平台。 深入瞭解[串流目的地](/help/destinations/destination-types.md#streaming-destinations)。 |

{style="table-layout:auto"}

## 連線到目標 {#connect}

>[!IMPORTANT]
>
>若要連線到目的地，您需要&#x200B;**[!UICONTROL View Destinations]**&#x200B;和&#x200B;**[!UICONTROL Manage Destinations]** [存取控制許可權](/help/access-control/home.md#permissions)。 閱讀[存取控制總覽](/help/access-control/ui/overview.md)或連絡您的產品管理員以取得必要的許可權。

若要連線到此目的地，請依照[目的地組態教學課程](../../ui/connect-destination.md)中所述的步驟進行。 在設定目標工作流程中，填寫以下兩個區段中列出的欄位。

### 驗證目標 {#authenticate}

若要驗證到目的地，請填寫必填欄位並選取&#x200B;**[!UICONTROL Connect to destination]**。

![顯示連線所需欄位的Reddit自訂對象目的地驗證畫面。](../../assets/catalog/advertising/redditcustomaudience/configure_new_destination_fields.png)

系統會將您重新導向以使用[!DNL Reddit]登入。 檢閱要求的許可權後，選取&#x200B;**[!UICONTROL Allow]**，讓[!DNL Experience Platform]可以代表您的廣告帳戶建立對象和更新成員資格。

![Reddit OAuth許可權畫面。](../../assets/catalog/advertising/redditcustomaudience/reddit_oauth.png)

### 填寫目標詳細資訊 {#destination-details}

若要設定目的地的詳細資訊，請填寫下方的必填和選用欄位。 UI中欄位旁的星號表示該欄位為必填欄位。

![Reddit自訂對象目的地詳細資訊畫面。](../../assets/catalog/advertising/redditcustomaudience/reddit_account_details.png)

* **[!UICONTROL Name]**：識別此目的地的名稱。
* **[!UICONTROL Description]**：可協助您識別此目的地的說明。
* **[!UICONTROL Ad Account ID]**：您的[!DNL Reddit]廣告帳戶識別碼。

### 啟用警示 {#enable-alerts}

您可以啟用警報以接收有關傳送到您目的地的資料流狀態的通知。 從清單中選取警報以訂閱接收有關資料流狀態的通知。 如需警示的詳細資訊，請參閱[使用UI訂閱目的地警示](../../ui/alerts.md)的指南。

當您完成提供目的地連線的詳細資訊時，請選取&#x200B;**[!UICONTROL Next]**。

## 啟動此目標的對象 {#activate}

>[!IMPORTANT]
>
>* 若要啟用資料，您需要&#x200B;**[!UICONTROL View Destinations]**、**[!UICONTROL Activate Destinations]**、**[!UICONTROL View Profiles]**&#x200B;和&#x200B;**[!UICONTROL View Segments]** [存取控制許可權](/help/access-control/home.md#permissions)。 閱讀[存取控制總覽](/help/access-control/ui/overview.md)或連絡您的產品管理員以取得必要的許可權。
>* 若要匯出&#x200B;*身分*，您需要&#x200B;**[!UICONTROL View Identity Graph]** [存取控制許可權](/help/access-control/home.md#permissions)。<br> ![選取工作流程中反白的身分名稱空間，以啟用目的地的對象。](/help/destinations/assets/overview/export-identities-to-destination.png "選取工作流程中反白顯示的身分名稱空間，以啟用目的地的對象。"){width="100" zoomable="yes"}

閱讀[將設定檔和對象啟用至串流對象匯出目的地](/help/destinations/ui/activate-segment-streaming-destinations.md)，以瞭解啟用此目的地對象的指示。

### 對應屬性和身分 {#map}

下列目標身分名稱空間必須根據使用案例進行對應：

| 來源欄位 | 目標欄位 | 附註 |
| --- | --- | --- |
| 電子郵件（純文字或雜湊） | email_lc_sha256 | 您的來源欄位可進行雜湊或取消雜湊。 [!DNL Reddit]只接受雜湊值。 啟用&#x200B;**[!UICONTROL Apply transformation]**，讓[!DNL Experience Platform]在傳送前先雜湊電子郵件。 |
| MAID （純文字或雜湊） | 女傭 | 您的來源欄位可進行雜湊或取消雜湊。 [!DNL Reddit]只接受雜湊值。 啟用&#x200B;**[!UICONTROL Apply transformation]**，讓[!DNL Experience Platform]在傳送前先雜湊值。 |

您必須至少對應其中一個身分。

![身分對應畫面顯示為Reddit自訂對象設定的來源和目標欄位。](../../assets/catalog/advertising/redditcustomaudience/mapping.png)

## 匯出的資料/驗證資料匯出 {#exported-data}

啟用對象後，您就能在[!DNL Reddit]廣告管理員帳戶中看到這些對象。

在[!DNL Reddit]中新建立的對象會以擱置狀態出現。 在您的資料流執行並匯出設定檔後，[!DNL Reddit]會比對設定檔與[!DNL Reddit]位使用者。 處理資料後，對象狀態會變更為&#x200B;**[!UICONTROL Valid]**。 對象人數必須達到[1,000位或更多](https://ads-api.reddit.com/docs/v3/manage-customer-lists)個使用者，才能視為有效。 不符合所需大小的對象會顯示為&#x200B;**[!UICONTROL Invalid]**。

![Reddit廣告管理員顯示匯出的對象及其狀態。](../../assets/catalog/advertising/redditcustomaudience/see_audience_in_reddit.png)

以下為傳送至[!DNL Reddit]之裝載的範例：

```json
{
  "data": {
    "action_type": "ADD",
    "column_order": [
      "EMAIL_SHA256",
      "MAID_SHA256"
    ],
    "user_data": [
      [
        "d7ef2e7b2a3663c25284a3d6d13b1ca727fc8c659474b81afe0cec997a4737d2",
        "510870d7b3e47a28a2b2f3aef27a4c81aab0b2eefda27dea50bc4c991d9e5435"
      ]
    ]
  }
}
```

如需其他詳細資訊，請參閱[Reddit API檔案](https://ads-api.reddit.com/docs/v3/operations/Update%20Custom%20Audience%20Users)。

## 資料使用與控管 {#data-usage-governance}

處理您的資料時，所有[!DNL Adobe Experience Platform]目的地都符合資料使用原則。 如需[!DNL Adobe Experience Platform]如何強制資料控管的詳細資訊，請閱讀[資料控管概觀](/help/data-governance/home.md)。

## 其他資源 {#additional-resources}

如需自訂對象端點如何運作的詳細資訊，請參閱[Reddit API檔案](https://ads-api.reddit.com/docs/v3/operations/Update%20Custom%20Audience%20Users)。
