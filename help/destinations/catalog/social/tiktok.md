---
title: TikTok連線
description: 使用您的資料在TikTok上建立自訂對象，以便透過您的廣告促銷活動鎖定目標。 這些對象可能是造訪您的網站或與您的內容互動的人員。 使用Adobe與TikTok Ads Manager的即時整合，快速安全地將所需的區段從Adobe Experience Platform推送至TikTok。
last-substantial-update: 2023-03-20T00:00:00Z
source-git-commit: 7bfcd0132380f0c847742ff05c1f334542adfba2
workflow-type: tm+mt
source-wordcount: '980'
ht-degree: 2%

---


# TikTok連線

## 總覽 {#overview}

使用您的資料在TikTok上建立自訂對象，以便透過您的廣告促銷活動鎖定目標。 這些對象可能是造訪您的網站或與您的內容互動的人員。 使用Adobe與TikTok Ads Manager的即時整合，快速安全地將所需的區段從Adobe Experience Platform推送至TikTok。 瀏覽 [TikTok商務支援中心](https://ads.tiktok.com/help/article/audiences?lang=en) 以取得更多資訊。

>[!IMPORTANT]
>
>本檔案頁面由TikTok團隊建立。 如有任何查詢或更新請求，請直接與他們聯繫，地址為 [https://ads.tiktok.com/help/](https://ads.tiktok.com/help/).

## 使用案例 {#use-cases}

為協助您更清楚了解應如何及何時使用TikTok目的地，以下是Adobe Experience Platform客戶的範例使用案例。

### 使用案例 {#use-case-1}

運動服裝品牌想透過其社交媒體帳戶觸及現有客戶。 服飾品牌可將其CRM的電子郵件地址擷取至Adobe Experience Platform、從其離線資料建立區段，並將這些區段傳送至TikTok，以在其客戶的社交媒體摘要中顯示廣告。

## 先決條件 {#prerequisites}

將資料傳送至 [!DNL TikTok Ads Manager] 帳戶時，您需要授予Adobe Experience Platform存取您的廣告帳戶的權限 `Audience Management`. 您可以在Experience Platform中輸入廣告商ID，並在重新導向後授予權限，才能提供此權限。 如需更多指示，請參閱 [TikTok API檔案](https://ads.tiktok.com/marketing_api/docs?id=1738373141733378).

## 支援的身分 {#supported-identities}

TikTok支援啟用下表所述的身分。 深入了解 [身分](/help/identity-service/namespaces.md).

| Target身分 | 說明 | 考量事項 |
|---|---|---|
| GAID | Google Advertising ID | 當源標識為GAID命名空間時，選擇GAID目標標識。 |
| IDFA | Apple ID for Advertisers | 如果來源識別為IDFA命名空間，請選取IDFA目標識別。 |
| 電話號碼 | 使用SHA256演算法雜湊的電話號碼 | Adobe Experience Platform支援純文字和SHA256雜湊電話號碼，且必須採用E.164格式。 當來源欄位包含未雜湊屬性時，請檢查 **[!UICONTROL 套用轉換]** 選項，必須 [!DNL Platform] 啟動時自動雜湊資料。 |
| 電子郵件 | 使用SHA256演算法雜湊的電子郵件地址 | Adobe Experience Platform支援純文字和SHA256雜湊電子郵件地址。 當來源欄位包含未雜湊屬性時，請檢查 **[!UICONTROL 套用轉換]** 選項，必須 [!DNL Platform] 啟動時自動雜湊資料。 |

{style="table-layout:auto"}

## 匯出類型和頻率 {#export-type-frequency}

有關目標導出類型和頻率的資訊，請參閱下表。

| 項目 | 類型 | 附註 |
---------|----------|---------|
| 匯出類型 | **[!UICONTROL 區段匯出]** | 您正在匯出區段（對象）的所有成員，以及TikTok目的地所使用的識別碼（名稱、電話號碼或其他）。 |
| 匯出頻率 | **[!UICONTROL 串流]** | 串流目的地是「一律開啟」API型連線。 一旦根據區段評估在Experience Platform中更新設定檔，連接器就會將更新傳送至下游的目的地平台。 深入了解 [串流目的地](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## 連接到目標 {#connect}

>[!IMPORTANT]
> 
>若要連線至目的地，您需要 **[!UICONTROL 管理目的地]** [存取控制權限](/help/access-control/home.md#permissions). 閱讀 [存取控制概觀](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得所需的權限。

若要連線至此目的地，請依照 [目的地設定教學課程](../../ui/connect-destination.md). 在設定目標工作流程中，填寫下列兩節所列的欄位。

### 驗證到目標 {#authenticate}

若要驗證目的地，系統會將您重新導向，以登入您的 [!DNL TikTok Ads Manager] 帳戶和授權Adobe代表您管理對象。

![TikTok權限選取](/help/destinations/assets/catalog/social/tiktok/tiktok-authenticate-destination.png "TikTok UI的影像以選取權限")

### 填寫目的地詳細資訊 {#destination-details}

若要設定目的地的詳細資訊，請填寫下方的必填和選填欄位。 UI中欄位旁的星號表示該欄位為必要欄位。

![目標連接詳細資訊](/help/destinations/assets/catalog/social/tiktok/tiktok-configure-destination-details.png "Platform UI的影像，顯示要填入的目的地連線詳細資訊")

* **[!UICONTROL 名稱]**:日後您將透過此名稱識別此目的地。
* **[!UICONTROL 說明]**:未來可協助您識別此目的地的說明。
* **[!UICONTROL TikTok Ads Manager ID]**:您的 [!DNL TikTok Ads Manager ID]. 您可以在 [!DNL TikTok Ads manager] 帳戶。

![TikTok Ads Manager ID](/help/destinations/assets/catalog/social/tiktok/tiktok-ads-manager-ID.png "TikTok Ads Manager UI的影像，顯示如何取得TikTok Ads Manager ID")

### 啟用警報 {#enable-alerts}

您可以啟用警報，接收有關資料流到目標狀態的通知。 從清單中選擇要訂閱的警報，以接收有關資料流狀態的通知。 如需警報的詳細資訊，請參閱 [使用UI訂閱目的地警報](../../ui/alerts.md).

完成提供目標連接的詳細資訊後，請選擇 **[!UICONTROL 下一個]**.

## 啟用此目的地的區段 {#activate}

>[!IMPORTANT]
> 
>若要啟用資料，您需要 **[!UICONTROL 管理目的地]**, **[!UICONTROL 啟動目的地]**, **[!UICONTROL 檢視設定檔]**，和 **[!UICONTROL 檢視區段]** [存取控制權限](/help/access-control/home.md#permissions). 閱讀 [存取控制概觀](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得所需的權限。

閱讀 [啟動設定檔和區段至串流區段匯出目的地](/help/destinations/ui/activate-segment-streaming-destinations.md) 以取得啟用受眾區段至此目的地的指示。

### 對應身分 {#map}

以下是將區段匯出至TikTok Ads Manager時的正確身分對應範例。

選擇源欄位：

* 選取識別碼(例如：` Email_LC_SHA256`)做為來源識別，可在Adobe Experience Platform和 [!DNL TikTok Ads Manager].

選擇目標欄位：

* 選取電子郵件命名空間作為目標身分。

![身分對應](/help/destinations/assets/catalog/social/tiktok/tiktok-map-identity.png "Platform UI的影像、身分對應")

## 匯出的資料 {#exported-data}

檢查 [!DNL TikTok Ads Manager] 帳戶(在 **資產>受眾**)，驗證您的Experience Platform區段是否成功匯出。 對象將會填入為對象類型： `Partner Audience`.

## 資料使用與控管 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 處理資料時，目的地符合資料使用原則。 有關如何 [!DNL Adobe Experience Platform] 強制實施資料治理，讀取 [資料控管概觀](/help/data-governance/home.md).

## 其他資源 {#additional-resources}

請參閱 [TikTok說明中心頁面](https://ads.tiktok.com/help/article/audiences?lang=en) 以取得其他資訊。
