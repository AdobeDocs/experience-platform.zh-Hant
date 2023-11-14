---
keywords: Experience Platform；首頁；熱門主題；Pinterest Ads；
title: pinterest Ads來源概觀
description: 瞭解如何使用API或使用者介面將Pinterest Ads連結至Adobe Experience Platform。
badge: Beta
hide: true
hidefromtoc: true
exl-id: 8edbcb26-0a18-47f1-8012-ca209d99d7a6
source-git-commit: e37c00863249e677f1645266859bf40fe6451827
workflow-type: tm+mt
source-wordcount: '984'
ht-degree: 0%

---

# [!DNL Pinterest Ads]

>[!NOTE]
>
>此 [!DNL Pinterest Ads] 來源為測試版。 閱讀 [來源概觀](../../home.md#terms-and-conditions) 以取得有關使用Beta標籤聯結器的詳細資訊。

Adobe Experience Platform可讓您從外部來源擷取資料，同時使用Platform服務來建構、加標籤及增強傳入資料。 您可以從多種來源(例如Adobe應用程式、雲端儲存、資料庫和許多其他來源)內嵌資料。

Experience Platform支援從協力廠商廣告系統擷取資料。 對廣告提供者的支援包括 [!DNL Pinterest Ads].

[[!DNL Pinterest]](https://www.pinterest.com) 是視覺化探索引擎，可在網路上尋找配方、家庭裝飾、風格靈感和其他創意。 這些以小比例呈現，使用插接板格式的影像、動畫GIF和影片。 [[!DNL Pinterest Ads]](https://ads.pinterest.com/) 可讓您發展業務，並透過以下方式吸引4億人 [!DNL Pinterest].

替換為 [!DNL Pinterest Ads]，您可以透過鎖定目標的廣告觸及使用者，以探索及購買您的產品。 釘選來源 [!DNL Pinterest Ads] 獲得贊助，以便在相關搜尋結果中取得額外的曝光率。 訂閱的使用者 [!DNL Pinterest Business] 可選擇促銷現有效能最佳的圖釘、建立新的影像或影片，或甚至促銷從網站釘選的影像。 [!DNL Pinterest Ads] 提供數種廣告格式，協助您達成特定的行銷活動目標。

## [!DNL Pinterest] API {#pinterest-apis}

此 [!DNL Pinterest Ads] 來源會利用 [!DNL Pinterest] 用於擷取您的 [!DNL Pinterest Ads] 資料，以及所有效能和量度。 支援的API端點包括：

* [行銷活動分析](https://developers.pinterest.com/docs/api/v5/#operation/campaigns/analytics)
* [廣告群組分析](https://developers.pinterest.com/docs/api/v5/#operation/ad_groups/analytics)
* [廣告分析](https://developers.pinterest.com/docs/api/v5/#operation/ads/analytics)

使用 [!DNL Pinterest Ads] 將您的資料帶入的來源 [!DNL Pinterest] 以Experience Platform，您可在其中執行資料分析。 日期回溯範圍為90天的資料會從擷取日期開始傳回。 [!DNL Pinterest Ads] 使用持有人權杖作為驗證機制，以與 [!DNL Pinterest] API。

## 先決條件 {#prerequisites}

建立的第一步 [!DNL Pinterest Ads] 來源連線是為了確保您擁有Pinterest開發人員帳戶。 如果您還沒有這類網站，請前往 [註冊](https://www.pinterest.com/business/create/?next=https://developers.pinterest.com/account-setup/) 頁面以註冊及建立您的帳戶。

### 設定 [!DNL Pinterest] 應用程式並產生存取權杖 {#create-app-and-generate-token}

>[!IMPORTANT]
>
>建議使用 [!DNL Pinterest] API會產生您的存取權杖，因為在UI中產生您的存取權杖可提供有限的存取權。 透過UI，您將只能存取以下範圍： `pins:read`， `boards:read` 和 `user_accounts:read`. 此限制不足以搭配的分析端點使用 [!DNL Pinterest] API。

若要產生存取權杖，請閱讀 [!DNL Pinterest] 指南 [設定您的應用程式](https://developers.pinterest.com/docs/getting-started/set-up-app/) 和 [使用OAuth 2.0進行驗證](https://developers.pinterest.com/docs/getting-started/authentication/).

### 收集必要的認證 {#gather-required-credentials}

為了連線 [!DNL Pinterest Ads] 至Platform，您必須提供下列連線屬性的值：

| 認證 | 說明 |
| --- | --- |
| 存取權杖 | 此 [!DNL Pinterest Ads] 您的使用者帳戶的存取權杖。 權杖的使用者帳戶必須是指定的擁有者 [!DNL Pinterest Ad] 帳戶或擁有透過Business Access授予的必要角色之一：管理員、分析人員或行銷活動管理員。 如需存取Token的詳細資訊，請參閱 [[!DNL Pinterest] 產生存取權杖的相關指南](https://developers.pinterest.com/docs/getting-started/set-up-app/). |
| 廣告帳戶ID | 相關的 [!DNL Pinterest Ads] 您業務單位的廣告帳戶ID。 有關擷取廣告帳戶ID的資訊。 造訪 [[!DNL Pinterest] 在Ads Manager中尋找ID指南](https://help.pinterest.com/en/business/article/find-ids-in-ads-manager). |
| 行銷活動、廣告群組或廣告ID | 此 `campaign`， `ad group`，或 `ad` 與您的廣告帳戶ID相對應的ID。 若要取得必要的ID，請導覽至 [!DNL Pinterest] 第頁 —  **pinterest商業中心** > **廣告帳戶摘要** > **行銷活動** / **廣告群組** / **廣告** 並複製其每個名稱正下方提及的必要ID。 |

>[!NOTE]
>
>此 [!DNL Pinterest] API提供個別API，可擷取與每個ID相關聯的資料。 因此，您只需針對感興趣的ID型別傳遞對應的ID。

## 護欄 {#guardrails}

以下小節提供有關以下專案的資料護欄資訊： [!DNL Pinterest].

### [!DNL Pinterest] 日期範圍 {#pinterest-date-range}

此 [!DNL Pinterest] API同時支援 `start_date` 和 `end_date` 引數來擷取指定日期範圍之間的分析資料。

* 此 `start_date` 距目前日期不能超過90天。
* 此 `end_date` 之後不能超過90天 `start_date`.

排程資料流時，您必須設定下列其中一個頻率和間隔設定：

| 頻率 | 間隔 |
| --- | --- |
| `Day` | 1 |
| `Hour` | 24 |

例如，如果內嵌設定在2023年3月15日，而頻率和間隔設定則設定為 `Day=1` 或 `Hour=24`，然後 [!DNL Pinterest] API最多只會從2022年12月15日擷取資料，因為計算日期回溯了90天。

### [!DNL Pinterest] 時間範圍 {#pinterest-time-range}

此 [!DNL Pinterest] API支援不同型別的時間詳細程度，以便擷取資料：

| 時間粒度 | 說明 |
| --- | --- |
| **總計** | 資料量度會在指定的日期範圍內彙總。 |
| **日** | 資料量度每天都會劃分。 |
| **HOUR** | 資料量度會每小時細分。 |
| **每週** | 資料量度每週都會劃分。 |
| **每月** | 資料量度每月都會劃分。 |

對於Platform，則是 [!DNL Pinterest Ads] 來源已在內部設定為 `Day`，即資料將會每日彙總。 例如，使用 `impressions recorded` 做為量度，因為詳細程度會設定為 `DAY`，您會得到 `xx` 閱聽次數 `day 1`， `yy` 閱聽次數 `day 2` 等等。

>[!IMPORTANT]
>
>pinterest會對其API施加每日1000次API呼叫的速率限制，以從廣告、廣告群組或廣告行銷活動中讀取資訊。 如需適用於基礎API呼叫之速率限制的詳細資訊，請參閱 [[!DNL Pinterest] 有關速率限制的檔案](https://developers.pinterest.com/docs/reference/ratelimits/).

## 連線 [!DNL Pinterest Ads] 至平台 {#connect-to-platform}

以下檔案提供有關如何連線的資訊 [!DNL Pinterest Ads] 使用API或使用者介面至Platform：

### 連線 [!DNL Pinterest Ads] 使用API移至Platform {#connect-to-platform-using-api}

* [使用Flow Service API建立Pinterest基本連線](../../tutorials/api/create/advertising/pinterest-ads.md)
* [使用流量服務API探索資料表](../../tutorials/api/explore/tabular.md)
* [使用流量服務API為廣告來源建立資料流](../../tutorials/api/collect/advertising.md)

### 連線 [!DNL Pinterest Ads] 使用UI移至Platform {#connect-to-platform-using-ui}

* [在UI中建立Pinterest來源連線](../../tutorials/ui/create/advertising/pinterest-ads.md)
* [在UI中為Advertising來源連線建立資料流](../../tutorials/ui/dataflow/advertising.md)
