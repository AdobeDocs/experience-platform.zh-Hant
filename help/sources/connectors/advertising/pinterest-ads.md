---
keywords: Experience Platform；首頁；熱門主題；Pinterest Ads；
title: Pinterest Ads Source概觀
description: 瞭解如何使用API或使用者介面將Pinterest Ads連結至Adobe Experience Platform。
badge: Beta
hide: true
hidefromtoc: true
exl-id: 8edbcb26-0a18-47f1-8012-ca209d99d7a6
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '946'
ht-degree: 1%

---

# [!DNL Pinterest Ads]

>[!NOTE]
>
>[!DNL Pinterest Ads]來源是測試版。 閱讀[來源概觀](../../home.md#terms-and-conditions)，瞭解使用Beta標籤聯結器的詳細資訊。

Adobe Experience Platform可讓您從外部來源擷取資料，同時使用Experience Platform服務來建構、加標籤及增強傳入資料。 您可以從多種來源(例如Adobe應用程式、雲端儲存、資料庫和許多其他來源)內嵌資料。

Experience Platform支援從協力廠商廣告系統擷取資料。 對廣告提供者的支援包括[!DNL Pinterest Ads]。

[[!DNL Pinterest]](https://www.pinterest.com)是視覺化探索引擎，可在網路上尋找配方、家庭裝飾、風格靈感和其他創意。 這些以小比例呈現，使用插接板格式的影像、動畫GIF和視訊。 [[!DNL Pinterest Ads]](https://ads.pinterest.com/)可讓您使用[!DNL Pinterest]發展業務並觸及4億人。

透過[!DNL Pinterest Ads]，您可以透過目標廣告觸及使用者，以探索及購買您的產品。 來自[!DNL Pinterest Ads]的圖釘已贊助以在相關搜尋結果中取得額外的曝光。 訂閱[!DNL Pinterest Business]的使用者可選擇提升現有表現最佳的釘選、建立新的影像或影片，或甚至提升已從網站釘選的影像。 [!DNL Pinterest Ads]提供多種廣告格式，協助您達成特定的行銷活動目標。

## [!DNL Pinterest] API {#pinterest-apis}

[!DNL Pinterest Ads]來源利用[!DNL Pinterest] API來擷取您的[!DNL Pinterest Ads]資料，以及所有效能和量度。 支援的API端點包括：

* [行銷活動分析](https://developers.pinterest.com/docs/api/v5/#operation/campaigns/analytics)
* [廣告群組分析](https://developers.pinterest.com/docs/api/v5/#operation/ad_groups/analytics)
* [廣告分析](https://developers.pinterest.com/docs/api/v5/#operation/ads/analytics)

使用[!DNL Pinterest Ads]來源將您的資料從[!DNL Pinterest]帶到Experience Platform，您接著可以在其中執行資料分析。 日期回溯範圍為90天的資料會從擷取日期開始傳回。 [!DNL Pinterest Ads]使用持有人權杖作為驗證機制來與[!DNL Pinterest] API通訊。

## 先決條件 {#prerequisites}

建立[!DNL Pinterest Ads]來源連線的第一個步驟是確定您擁有Pinterest開發人員帳戶。 如果您還沒有帳戶，請造訪[註冊](https://www.pinterest.com/business/create/?next=https://developers.pinterest.com/account-setup/)頁面來註冊並建立您的帳戶。

### 設定[!DNL Pinterest]應用程式並產生存取權杖 {#create-app-and-generate-token}

>[!IMPORTANT]
>
>建議您使用[!DNL Pinterest] API來產生您的存取權杖，因為在UI中產生您的存取權杖可提供有限的存取權。 透過UI，您只能存取下列範圍： `pins:read`、`boards:read`和`user_accounts:read`。 此限制不足以用於[!DNL Pinterest] API的分析端點。

若要產生存取權杖，請閱讀[設定您的應用程式](https://developers.pinterest.com/docs/getting-started/set-up-app/)和[使用OAuth 2.0](https://developers.pinterest.com/docs/getting-started/authentication/)驗證的[!DNL Pinterest]指南。

### 收集必要的認證 {#gather-required-credentials}

若要將[!DNL Pinterest Ads]連線至Experience Platform，您必須提供下列連線屬性的值：

| 認證 | 說明 |
| --- | --- |
| 存取權杖 | 您使用者帳戶的[!DNL Pinterest Ads]存取權杖。 權杖的使用者帳戶必須是指定[!DNL Pinterest Ad]帳戶的擁有者，或擁有透過「業務存取」授予他們的一個必要角色：管理員、分析人員或促銷活動管理員。 如需存取權杖的詳細資訊，請參閱產生存取權杖](https://developers.pinterest.com/docs/getting-started/set-up-app/)的[[!DNL Pinterest] 指南。 |
| 廣告帳戶ID | 您事業單位的相關[!DNL Pinterest Ads]廣告帳戶ID。 有關擷取廣告帳戶ID的資訊。 造訪[[!DNL Pinterest] 在廣告管理員](https://help.pinterest.com/en/business/article/find-ids-in-ads-manager)中尋找ID指南。 |
| 行銷活動、廣告群組或廣告ID | 與您的廣告帳戶ID相對應的`campaign`、`ad group`或`ad` ID。 若要取得必要的ID，請瀏覽至&#x200B;**Pinterest Business Hub** > **廣告帳戶摘要** > **促銷活動** / **廣告群組** / **廣告**&#x200B;的[!DNL Pinterest]頁面，並複製每個名稱下方提及的必要ID。 |

>[!NOTE]
>
>[!DNL Pinterest] API提供個別API來擷取與每個ID相關聯的資料。 因此，您只需針對感興趣的ID型別傳遞對應的ID。

## 護欄 {#guardrails}

下列章節提供[!DNL Pinterest]資料護欄的相關資訊。

### [!DNL Pinterest]日期範圍 {#pinterest-date-range}

[!DNL Pinterest] API同時支援`start_date`和`end_date`引數，以便在指定的日期範圍內擷取分析資料。

* `start_date`在目前日期之前不能超過90天。
* `end_date`在`start_date`之後不能超過90天。

排程資料流時，您必須設定下列其中一個頻率和間隔設定：

| 頻率 | 間隔 |
| --- | --- |
| `Day` | 1 |
| `Hour` | 24 |

例如，如果內嵌設定於2023年3月15日，而頻率和間隔設定則設定為`Day=1`或`Hour=24`，則[!DNL Pinterest] API只會從2022年12月15日的最早日期擷取資料，因為計算已回溯90天。

### [!DNL Pinterest]時間範圍 {#pinterest-time-range}

[!DNL Pinterest] API支援各種時間粒度，以便擷取資料：

| 時間詳細程度 | 說明 |
| --- | --- |
| **總計** | 資料量度會在指定的日期範圍內彙總。 |
| **天** | 資料量度每天都會劃分。 |
| **小時** | 資料量度會每小時細分。 |
| **每週** | 資料量度每週都會劃分。 |
| **每月** | 資料量度每月都會劃分。 |

針對Experience Platform，[!DNL Pinterest Ads]來源在內部設定為`Day`，這表示資料將會每日彙總。 例如，使用`impressions recorded`做為量度，因為詳細程度設定為`DAY`，您將會在`day 1`上取得`xx`次曝光數，在`day 2`上取得`yy`次曝光數，以此類推。

>[!IMPORTANT]
>
>Pinterest會對其API施加每日1000次API呼叫的速率限制，以從廣告、廣告群組或廣告行銷活動中讀取資訊。 如需適用於基礎API呼叫的速率限制資訊，請參閱[[!DNL Pinterest] 有關速率限制](https://developers.pinterest.com/docs/reference/ratelimits/)的檔案。

## 將[!DNL Pinterest Ads]連線至Experience Platform {#connect-to-platform}

以下檔案提供如何使用API或使用者介面將[!DNL Pinterest Ads]連線至Experience Platform的資訊：

### 使用API連線[!DNL Pinterest Ads]至Experience Platform {#connect-to-platform-using-api}

* [使用Flow Service API建立Pinterest基本連線](../../tutorials/api/create/advertising/pinterest-ads.md)
* [使用流量服務API探索資料表](../../tutorials/api/explore/tabular.md)
* [使用流量服務API為廣告來源建立資料流](../../tutorials/api/collect/advertising.md)

### 使用UI連線[!DNL Pinterest Ads]至Experience Platform {#connect-to-platform-using-ui}

* [在UI中建立Pinterest來源連線](../../tutorials/ui/create/advertising/pinterest-ads.md)
* [在UI中為Advertising來源連線建立資料流](../../tutorials/ui/dataflow/advertising.md)
