---
keywords: Experience Platform；首頁；熱門主題；Pinterest Ad;
title: Pinterest Ads來源概述
description: 了解如何使用API或使用者介面將Pinterest Ads連線至Adobe Experience Platform。
badge: "Beta"
hide: true
hidefromtoc: true
source-git-commit: a16264da68d9e5e9aeac86b1a3083c701407febb
workflow-type: tm+mt
source-wordcount: '984'
ht-degree: 0%

---

# [!DNL Pinterest Ads]

>[!NOTE]
>
>此 [!DNL Pinterest Ads] 來源為測試版。 閱讀 [來源概觀](../../home.md#terms-and-conditions) 有關使用測試版標籤連接器的詳細資訊。

Adobe Experience Platform可讓您從外部來源擷取資料，同時使用Platform服務來建構、加標籤及增強傳入資料。 您可以從多種來源(如Adobe應用程式、雲儲存、資料庫等)內嵌資料。

Experience Platform支援從協力廠商廣告系統擷取資料。 對廣告提供者的支援包括 [!DNL Pinterest Ads].

[[!DNL Pinterest]](https://www.pinterest.com) 是視覺探索引擎，可在網路上尋找食譜、家居裝飾、風格靈感和其他想法。 這些內容以插針式格式使用影像、動畫GIF和視訊，以小規模呈現。 [[!DNL Pinterest Ads]](https://ads.pinterest.com/) 使您能夠擴展業務，使用 [!DNL Pinterest].

使用 [!DNL Pinterest Ads]，您可以透過目標廣告聯絡使用者，以探索及購買您的產品。 針 [!DNL Pinterest Ads] 會在相關搜尋結果中獲得額外曝光。 訂閱的使用者 [!DNL Pinterest Business] 可以選擇促銷現有的效能最佳的針腳、建立新的影像或視頻，甚至促銷已從網站固定的影像。 [!DNL Pinterest Ads] 提供數種廣告格式，協助您達成特定的行銷活動目標。

## [!DNL Pinterest] API {#pinterest-apis}

此 [!DNL Pinterest Ads] 源利用 [!DNL Pinterest] 擷取您 [!DNL Pinterest Ads] 資料，以及所有效能和量度。 支援的API端點為：

* [Campaign分析](https://developers.pinterest.com/docs/api/v5/#operation/campaigns/analytics)
* [廣告群組分析](https://developers.pinterest.com/docs/api/v5/#operation/ad_groups/analytics)
* [Ads分析](https://developers.pinterest.com/docs/api/v5/#operation/ads/analytics)

使用 [!DNL Pinterest Ads] 來源將資料從 [!DNL Pinterest] 至Experience Platform，接著您就可以執行資料分析。 系統會從擷取日期開始傳回90天回溯範圍的資料。 [!DNL Pinterest Ads] 使用承載令牌作為與通信的驗證機制 [!DNL Pinterest] API。

## 先決條件 {#prerequisites}

建立 [!DNL Pinterest Ads] 來源連線是為了確保您擁有Pinterest開發人員帳戶。 如果尚未建立，請造訪 [註冊](https://www.pinterest.com/business/create/?next=https://developers.pinterest.com/account-setup/) 頁面來註冊和建立您的帳戶。

### 設定 [!DNL Pinterest] 應用程式和產生存取權杖 {#create-app-and-generate-token}

>[!IMPORTANT]
>
>建議使用 [!DNL Pinterest] API來產生您的存取權杖，因為在UI中產生您的存取權杖時提供的存取權限有限。 您只能透過UI存取下列範圍： `pins:read`, `boards:read` 和 `user_accounts:read`. 此限制不適合搭配以 [!DNL Pinterest] API。

若要產生存取權杖，請閱讀 [!DNL Pinterest] 指南 [設定您的應用程式](https://developers.pinterest.com/docs/getting-started/set-up-app/) 和 [使用OAuth 2.0驗證](https://developers.pinterest.com/docs/getting-started/authentication/).

### 收集所需憑據 {#gather-required-credentials}

為了連接 [!DNL Pinterest Ads] 若要使用Platform，您必須提供下列連線屬性的值：

| 憑據 | 說明 |
| --- | --- |
| 存取權杖 | 此 [!DNL Pinterest Ads] 使用者帳戶的存取權杖。 代號的使用者帳戶必須是指定 [!DNL Pinterest Ad] 帳戶，或通過業務訪問授予其一個必要角色：管理員、分析師或行銷活動經理。 如需存取權杖的詳細資訊，請參閱 [[!DNL Pinterest] 產生存取權杖的指南](https://developers.pinterest.com/docs/getting-started/set-up-app/). |
| 廣告帳戶ID | 相關 [!DNL Pinterest Ads] 您業務部門的廣告帳戶ID。 以取得擷取廣告帳戶ID的相關資訊。 造訪 [[!DNL Pinterest] 在Ads Manager中尋找ID的指南](https://help.pinterest.com/en/business/article/find-ids-in-ads-manager). |
| 促銷活動、廣告群組或廣告ID | 此 `campaign`, `ad group`，或 `ad` 與您的廣告帳戶ID對應的ID。 若要取得必要ID，請導覽至 [!DNL Pinterest] 頁面 **Pinterest業務中心** > **廣告帳戶摘要** > **行銷活動** / **廣告群組** / **廣告** 並複製每個人名稱正下方提及的必要ID。 |

>[!NOTE]
>
>此 [!DNL Pinterest] API提供個別API，用以擷取與每個ID相關聯的資料。 因此，您只需要針對您感興趣的ID類型傳遞對應的ID。

## 護欄 {#guardrails}

以下各節提供的資料護欄資訊 [!DNL Pinterest].

### [!DNL Pinterest] 日期範圍 {#pinterest-date-range}

此 [!DNL Pinterest] API支援 `start_date` 和 `end_date` 在指定日期範圍之間擷取analytics資料的參數。

* 此 `start_date` 不得超過目前日期的90天。
* 此 `end_date` 不能超過90天 `start_date`.

調度資料流時，必須配置以下頻率和間隔設定之一：

| 頻率 | 間隔 |
| --- | --- |
| `Day` | 1 |
| `Hour` | 24 |

例如，如果擷取是在2023年3月15日設定，且頻率和間隔設定設定為 `Day=1` 或 `Hour=24`，則 [!DNL Pinterest] API只會從2022年12月15日以前擷取資料，因為計算日期可追溯90天。

### [!DNL Pinterest] 時間範圍 {#pinterest-time-range}

此 [!DNL Pinterest] API支援不同類型的時間粒度，以利擷取資料：

| 時間粒度 | 說明 |
| --- | --- |
| **總計** | 資料量度會匯總至指定的日期範圍。 |
| **日** | 資料量度會每日劃分。 |
| **小時** | 資料量度會每小時劃分。 |
| **每週** | 每週劃分資料量度。 |
| **每月** | 資料量度會每月劃分。 |

若為Platform, [!DNL Pinterest Ads] 源在內部配置為 `Day`，即表示資料會每天匯總。 例如，使用 `impressions recorded` 作為量度，因為精細度會設定為 `DAY`，你會 `xx` 曝光次數 `day 1`, `yy` 曝光次數 `day 2` 等等。

>[!IMPORTANT]
>
>Pinterest對其API實施每日1000個API呼叫的比率限制，以從廣告、廣告群組或廣告促銷活動讀取資訊。 如需基礎API呼叫適用的比率限制資訊，請參閱 [[!DNL Pinterest] 費率限制檔案](https://developers.pinterest.com/docs/reference/ratelimits/).

## Connect [!DNL Pinterest Ads] 到平台 {#connect-to-platform}

以下檔案提供如何連線的資訊 [!DNL Pinterest Ads] 若要使用API或使用者介面來建立平台：

### Connect [!DNL Pinterest Ads] 使用API到平台 {#connect-to-platform-using-api}

* [使用流程服務API建立Pinterest基本連線](../../tutorials/api/create/advertising/pinterest-ads.md)
* [使用流量服務API探索資料表](../../tutorials/api/explore/tabular.md)
* [使用流量服務API為廣告來源建立資料流](../../tutorials/api/collect/advertising.md)

### Connect [!DNL Pinterest Ads] 使用UI設為Platform {#connect-to-platform-using-ui}

* [在UI中建立Pinterest來源連線](../../tutorials/ui/create/advertising/pinterest-ads.md)
* [在UI中為Advertising來源連線建立資料流](../../tutorials/ui/dataflow/advertising.md)
