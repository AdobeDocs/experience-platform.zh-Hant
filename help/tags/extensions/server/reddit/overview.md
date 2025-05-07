---
title: Reddit轉換API擴充功能
description: 瞭解如何使用Reddit Ads Conversions API擴充功能，將使用者互動事件傳送至Reddit Ads，以用於目標定位廣告。
last-substantial-update: 2025-05-1
source-git-commit: 603cc86892f518852552eaa2fe1bdeaa296137cf
workflow-type: tm+mt
source-wordcount: '1022'
ht-degree: 1%

---

# [!DNL Reddit] Conversions API擴充功能概觀

Reddit是一個擁有多元化使用者基礎的社群媒體平台，非常適合定位特定受眾的廣告商。

使用[[!DNL Reddit] Conversions API擴充功能](https://ads-api.reddit.com/docs/v2/#tag/Conversions-API)，將Adobe Experience Platform Edge Network中擷取的使用者互動事件傳送至[!DNL Reddit Ads]。 使用此擴充功能協助您的品牌觸及超過3.79億每週活躍使用者的受眾，並更能瞭解使用者行為和執行鎖定目標的廣告。

閱讀本指南，瞭解如何在事件轉送[規則](https://experienceleague.adobe.com/en/docs/experience-platform/tags/ui/rules)中安裝、設定和使用[!DNL Reddit] Conversions API擴充功能。

## 主要優點 {#benefits}

使用Reddit Conversions API擴充功能可以：

- **觸及您的對象**：在[!DNL Reddit]每週與超過3.79億活躍使用者互動。
- **分析使用者行為**：運用使用者互動資料來瞭解行為並最佳化行銷活動。
- **傳遞目標廣告**：根據Adobe Experience Platform中擷取的使用者互動來執行個人化廣告。

## 先決條件 {#prerequisites}

您必須擁有有效的Reddit Ads帳戶才能使用此擴充功能。 移至[[!DNL Reddit Ads] 註冊頁面](https://business.reddithelp.com/s/article/Create-and-manage-your-Reddit-Ads-account)進行註冊並建立帳戶（如果尚未建立帳戶）。 您的帳戶設定完成後，[要求存取Ads API](https://www.redditforbusiness.com/api-partnership)。

### 收集必要的設定詳細資料 {#configuration-details}

若要將Experience Platform連線至[!DNL Reddit]，需要下列輸入：

| 認證 | 說明 | 範例 |
| --- | --- | --- |
| 畫素ID | 畫素ID是與您的[!DNL Reddit Ads]帳戶相關聯的唯一識別碼。 它可用來追蹤使用者在您網站或應用程式上的互動和轉換事件。 您可以在[!DNL Reddit Ads] [帳戶](https://ads.reddit.com/accounts)中找到您的畫素ID。 | 123456789012 |
| 轉換存取權杖 | 您的[!DNL Reddit]轉換存取權杖。 請參閱[[!DNL Reddit] 轉換API](https://business.reddithelp.com/s/article/conversion-access-token)檔案以取得指引。<br> **您只需要完成此程式一次，因為此Token並未過期。** | {YOUR_REDDIT_BEARER_TOKEN} |

## 安裝並設定[!DNL Reddit]擴充功能 {#install-configure}

請依照下列步驟安裝和設定[!DNL Reddit] Conversions API擴充功能：

1. 在Experience Platform資料收集UI中，從左側導覽選取[!UICONTROL 擴充功能]以存取[!UICONTROL 擴充功能]目錄。 然後[建立新的事件轉送屬性](https://experienceleague.adobe.com/en/docs/experience-platform/tags/event-forwarding/overview#properties)或選取現有的屬性。
2. 在左側導覽面板中導覽至&#x200B;**[!UICONTROL 擴充功能]**。 選取&#x200B;**[!UICONTROL 目錄]**，然後選取&#x200B;**[!DNL Reddit]**副檔名。
   ![反白顯示Reddit擴充功能的Adobe Experience Platform擴充功能目錄。](../../../images/extensions/server/reddit/reddit-extension.png)
3. 提供下列設定詳細資料：
   - **畫素識別碼**：輸入您的[!DNL Reddit Ads]畫素識別碼。
   - **轉換存取權杖**：輸入在您的[!DNL Reddit Ads]帳戶中產生的權杖，並在完成時選取&#x200B;**[!UICONTROL 儲存]**。
     ![ Reddit Conversions API擴充功能的設定詳細資料，包括畫素ID和轉換存取權杖的欄位。](../../../images/extensions/server/reddit/reddit-capi-details.png)

## 設定事件轉送規則 {#config-rule}

在您設定資料元素後，請建立事件轉送規則，以判斷將事件傳送至[!DNL Reddit Ads]的時間和方式。

1. 導覽至事件轉送屬性中的&#x200B;**規則**，並建立新的[規則](https://experienceleague.adobe.com/en/docs/experience-platform/tags/ui/rules)。
2. 在&#x200B;**動作**&#x200B;底下，新增動作並將擴充功能設為&#x200B;**[!DNL Reddit CAPI]**。
3. 將&#x200B;**動作型別**&#x200B;設定為&#x200B;**傳送事件**。
   ![Reddit Conversions API擴充功能的事件轉送規則設定介面，並反白顯示擴充功能和動作型別欄位。](../../../images/extensions/server/reddit/reddit-rule.png)
4. 設定事件的其他控制項，如下表所示：

   | 欄位名稱 | 說明 | 範例 |
   | --- | --- | --- |
   | `Event Name` | 指定轉換事件的名稱。 | `Purchase` |
   | `Event Type` | 定義可以是[支援的Reddit轉換事件](https://business.reddithelp.com/s/article/supported-conversion-events#supported-conversion-events)或自訂事件的事件型別。 | `SignUp`、`MyCustomEvent` |
   | `Timestamp` | 以ISO格式或紀元時間提供事件時間。 | `2025-04-15T16:01:00.000Z`、`1744742460000` |
   | `Client Dedupe ID` | 新增重複資料刪除的唯一ID。 | `abc123` |
   | `Match Keys` | 包含歸因的使用者和裝置識別碼。 | `{"email":"hashed_email@example.com", "phone":"hashed_phone"}` |
   | `Value` | 指定事件的貨幣值。 | `99.99` |
   | `Currency Code` | 使用ISO-4217格式作為貨幣。 | `USD` |
   | `Units Sold` | 輸入採購的料號數量。 | `3` |
   | `Country Code` | 指定事件發生的國家/地區。 | `US` |
   | `Data Processing Options` | 新增隱私權標幟，例如LDU （有限資料使用）。 | `{"modes":["LDU"],"country":"US","region":"US-NY"}` |
   | `Consent` | 表示廣告資料使用的使用者同意。 | `true` |

5. 選取&#x200B;**保留變更**&#x200B;以儲存規則。

## 事件中繼資料 {#event-metadata}

請參閱本節，以取得事件中繼資料和使用者資料欄位的詳細劃分，確保您瞭解設定事件的必要和選用引數。 顯示的欄位可能會依所選的事件型別而有所不同。

>[!NOTE]
>
>若要從轉換事件取得最佳結果，請務必在設定[動態產品廣告](https://business.reddithelp.com/s/article/dynamic-product-ads)時填寫所有欄位。

### 事件中繼資料欄位

![ Reddit Conversions API擴充功能的設定詳細資料，包括畫素ID和轉換存取權杖的欄位。](../../../images/extensions/server/reddit/reddit-event-metadata.png)

| 欄位名稱 | 說明 | 範例 |
| --- | --- | --- |
| `Conversion ID` （必要） | 用於重複資料刪除的轉換事件唯一ID。 | `abc123` |
| `Item Count` | 轉換事件的專案總數。 | `6` |
| `Currency` | 提供值的貨幣，格式為[ISO-4217](https://www.iso.org/iso-4217-currency-codes.html)。 | `USD` |
| `Value` | 轉換事件的總貨幣值，包括小數。 | `1.23` |
| `Products` | JSON物件陣列，其中包含與事件相關聯之產品的詳細資訊。 每個物件至少必須包含`id`。 | `[{"id":"SKU123","name":"ProductName","category":"CategoryName"},{"id":"SKU456","name":"ProductName","category":"CategoryName"}]` |

### 使用者資料欄位

下列引數為選用引數，但建議使用：

| 欄位名稱 | 說明 | 範例 |
| --- | --- | --- |
| `Email` （強烈建議） | 雜湊或未雜湊的使用者電子郵件。 | `example@email.com` |
| `External ID` | 雜湊或未雜湊的廣告商指派使用者ID。 | `customer12345` |
| `UUID` （強烈建議） | Reddit Pixel在您網站上產生的ID。 | `1677712978045.b8f7eb7d-b357-437b-8bd3-e1c8166c7132` |
| `IP Address` （強烈建議） | 使用者的裝置IP位址。 | `192.168.0.1` |
| `User Agent` （強烈建議） | 使用者使用的瀏覽器或應用程式。 | `Chrome/98.0.4758.102` |
| `IDFA` | 適用於廣告商的雜湊或未雜湊的Apple識別碼。 | `8A2E4F6D-0852-4B2A-B9D5-79334DE14B16` |
| `AAID` | 雜湊或未雜湊的Android Advertising ID。 | `38400000-8cf0-11bd-b23e-10b96e40000d` |
| `Screen Width` | 使用者顯示的寬度。 | `1920` |
| `Screen Height` | 使用者的顯示高度。 | `1080` |
| `Data Processing Options` （JSON格式） | 使用者隱私設定。 僅支援LDU （有限的資料使用量）。 | `{"modes":["LDU"],"country":"US","region":"US-NY"}` |

### 重要考量

在傳送資料至[!DNL Reddit Ads]之前，擴充功能會雜湊並標準化下列欄位的值： `Email`、`External ID`、`IDFA`和`AAID`。 擴充功能不會重新雜湊這些值（如果這些值已在[!DNL SHA-256]中雜湊）。

## 驗證和部署 {#validate-deploy}

設定擴充功能和規則後，請檢查[[!DNL Reddit Ads] 事件管理員](https://business.reddithelp.com/s/article/Events-Manager)中的事件資料以驗證整合。 使用[相符品質分數(MQS)](https://business.reddithelp.com/s/article/match-quality-score)來評估訊號整合的正確性和可靠性。

如需[!DNL Reddit Ads]的其他詳細資料，請瀏覽[Reddit Ads檔案](https://ads.reddit.com/)。

## 後續步驟 {#next-steps}

閱讀本檔案後，您現在應瞭解如何設定及使用[!DNL Reddit] Conversions API擴充功能。 如需Adobe Experience Platform中事件轉送功能的詳細資訊，請參閱[事件轉送概觀](../../../ui/event-forwarding/overview.md)或下列資源：

- [共用比對索引鍵](https://business.reddithelp.com/s/article/about-attribution-matching-signals)和[事件中繼資料](https://business.reddithelp.com/s/article/about-event-metadata)：瞭解如何有效共用比對索引鍵和事件中繼資料。
- [刪除重複事件](https://business.reddithelp.com/s/article/event-deduplication)：刪除重複事件，以確保事件追蹤準確。
- [建立轉換存取權杖](https://business.reddithelp.com/helpcenter/s/article/conversion-access-token)：請依照步驟建立安全API驗證的轉換存取權杖。
