---
title: Nextdoor Conversion API擴充功能
description: 瞭解如何使用Nextdoor Conversion API擴充功能來傳送轉換事件，以追蹤廣告行銷活動的效能。
last-substantial-update: 2025-12-18T00:00:00Z
source-git-commit: 56c69696300dd9de8c0e98ecc71cafc7328f1620
workflow-type: tm+mt
source-wordcount: '1772'
ht-degree: 8%

---


# [!DNL Nextdoor]轉換API擴充功能 — 使用手冊

## 概觀

[!DNL Nextdoor]是適用於志趣相投的社群網路服務，可將人們連線至其本機社群。 這是一個平台，鄰居可以在這裡溝通、分享資訊、瞭解當地活動和新聞的最新消息，並與當地的其他人一起買賣商品。

使用[[!DNL Nextdoor] 轉換API擴充功能](https://help.nextdoor.com/s/article/About-the-Nextdoor-Conversion-API)將轉換事件直接傳送至[!DNL Nextdoor's]轉換API。 此擴充功能可傳送伺服器端轉換資料，協助您追蹤及測量[!DNL Nextdoor]廣告行銷活動的成效。

本指南說明如何在事件轉送[!DNL Nextdoor]規則[中安裝、設定及使用](https://experienceleague.adobe.com/en/docs/experience-platform/tags/ui/rules) Conversion API擴充功能。

## 先決條件 {#prerequisites}

您需要有效的[!DNL Nextdoor]廣告管理員帳戶才能使用此擴充功能。 如果您還沒有帳戶，請移至[[!DNL Nextdoor Ads] 註冊頁面](https://ads.nextdoor.com/v2/signup)來註冊並建立您的帳戶。

### 收集必要的設定詳細資料 {#configuration-details}

若要將Experience Platform連線至[!DNL Nextdoor]，您需要下列資訊：

| 認證 | 說明 | 安全性注意事項 |
| --- | --- | --- |
| 資料Source ID | [!DNL Nextdoor]的唯一資料來源識別碼，您可存取Assets > Pixels頁面並產生Nextdoor Pixel，在[!DNL Nextdoor Ads Manager]帳戶中找到。 | 在您的組織內共用此專案是很安全的。 |
| 存取權杖 | 您用於安全通訊的API驗證存取權杖。 您可以登入您的[!DNL Nextdoor Ads Manager]帳戶並存取API設定來產生此Token。 | 確保此Token的安全，因為它可讓您存取帳戶。 |

## 安裝並設定[!DNL Nextdoor]擴充功能 {#install}

若要安裝擴充功能，請在左側導覽中選取&#x200B;**[!UICONTROL Extensions]**。 在&#x200B;**[!UICONTROL Catalog]**&#x200B;索引標籤中，選取&#x200B;**[!UICONTROL Nextdoor Conversion API Extension]**，然後選取&#x200B;**[!UICONTROL Install]**。

![顯示[!DNL Nextdoor]擴充卡醒目提示安裝的擴充功能目錄。](../../../images/extensions/server/nextdoor/install-extension.png)

在下一個畫面中，輸入您從[!DNL Nextdoor Ads Manager]產生的設定值：

* **[!UICONTROL Data Source ID]**
* **[!UICONTROL Access Token]**

完成後，選取&#x200B;**[!UICONTROL Save]**。

![[!DNL Nextdoor]轉換API擴充功能的[!DNL Nextdoor]設定畫面。](../../../images/extensions/server/nextdoor/configure.png)

## 設定事件轉送規則 {#config-rule}

設定好所有資料元素後，您就可以建立事件轉送規則，以決定將事件傳送至[!DNL Nextdoor]的時間和方式。

在您的事件轉送屬性中建立新的[規則](../../../ui/managing-resources/rules.md)。 在&#x200B;**[!UICONTROL Actions]**&#x200B;底下，新增動作並將擴充功能設為&#x200B;**[!UICONTROL Nextdoor Conversion API Extension]**。 若要將Edge Network事件傳送至[!DNL Nextdoor]，請將&#x200B;**[!UICONTROL Action Type]**&#x200B;設為&#x200B;**[!UICONTROL Report Web Conversions]**。

![正在資料收集UI中為[!UICONTROL Report Web Conversions]規則選取[!DNL Nextdoor]動作型別。](../../../images/extensions/server/nextdoor/select-action.png)

進行此選擇後，會出現其他控制項，讓您進一步設定事件，如下所述。 完成後，選取&#x200B;**[!UICONTROL Keep Changes]**&#x200B;以儲存規則。

**主體引數**

這些核心引數會定義您的轉換事件：

| 參數 | 說明 | 資料類型 | 必要 | 選項/格式 | 範例 |
| ------------------------------------ | -------------- | -------------- | -------------- | -------------- | -------------- |
| [!UICONTROL Event Name] | 指定要追蹤的轉換事件型別。 | 字串（下拉式清單） | 必要 | <ul><li>購買</li><li>銷售機會</li><li>註冊</li><li>新增至購物車</li><li>啟動簽出</li><li>頁面檢視</li><li>搜尋</li><li>檢視內容</li><li>新增至願望清單</li><li>訂閱</li><li>自訂</li></li>轉換1-10</li></ul> | `Purchase` |
| [!UICONTROL Event ID] | 防止重複事件報告的唯一識別碼。 如果空白，此專案將自動產生。 | 字串 | 選填 | 唯一字串識別碼 | `order_12345` |
| [!UICONTROL Event Time (Unix Epoch)] | 轉換事件發生時的時間戳記。 如果保留為空白，則預設為目前時間。 | 整數 | 選填 | Unix時間戳記（以秒為單位） | `1703980800` （2023年12月30日） |
| [!UICONTROL Action Source] | 發生轉換的管道或平台。 | 字串（下拉式清單） | 必要 | <ul><li>網站</li><li>電子郵件</li><li>app</li><li>phone_call</li><li>聊天</li><li>physical_store</li><li>system_generated</li><li>其他</li></ul> | `website` |
| [!UICONTROL Data Source ID] | 覆寫特定事件的全域資料來源ID。 如果留白，將繼承自設定。 | 字串 | 選填 | 英數字串 | `12345` |
| [!UICONTROL Action Source URL] | 發生轉換的特定URL。 | 字串 | 選填 | 包含通訊協定的完整URL | https://example.com/checkout/success |

**隱私權與法規遵循引數**

請使用以下引數確保隱私權法規遵循：

| 參數 | 說明 | 資料類型 | 必要 | 值/格式 | 範例 |
| -------------------------------------------- | ---------------------------------------------------  | --------- | -------- | ---------------------------------------------------------- | ---------- |
| [!UICONTROL Restricted Data Usage] | 針對隱私權合規性限制資料使用的標幟。 | 整數 | 選填 | <ul><li>0 =無限制</li><li>1 =限制</li></ul> | `0` |
| [!UICONTROL Restricted Data Usage (Country)] | 特定國家的資料處理限制。 | 整數 | 選填 | 1 =美國（可能支援其他程式碼） | `1` |
| [!UICONTROL Restricted Data Usage (State)] | 美國使用者的州特定限制。 | 整數 | 選填 | 1000 = CA、1001 = CO等 | `1000` |
| [!UICONTROL Test Event] | 將事件標籤為開發/偵錯的測試。 | 字串 | 選填 | 任何非空白字串 | `test` |

**客戶資訊引數**

>[!IMPORTANT]
>
>您必須至少提供一個客戶資訊引數，才能正確進行事件歸因和比對。

| 參數 | 說明 | 資料類型 | 必要 | 格式 | 範例 |
| ------------------------------ | ----------------------------------------------- | --------- | ------------------------------------ | ------------------------------------ | -------------------------- |
| [!UICONTROL Email] | 用於身分比對的客戶電子郵件地址。 | 字串 | 至少需要一個客戶欄位 | 純文字或SHA-256雜湊 | `user@example.com` |
| [!UICONTROL Phone Number] | 用於身分比對的客戶電話號碼。 | 字串 | 至少需要一個客戶欄位 | E.164格式（以SHA-256雜湊） | `+15551234567` |
| [!UICONTROL First Name] | 用於增強型比對的客戶名字。 | 字串 | 至少需要一個客戶欄位 | 純文字或SHA-256雜湊 | `John` |
| [!UICONTROL Last Name] | 用於增強比對的客戶姓氏。 | 字串 | 至少需要一個客戶欄位 | 純文字或SHA-256雜湊 | `Smith` |
| [!UICONTROL Date of Birth] | 人口統計比對的客戶出生日期。 | 字串 | 選填 | YYYYMMDD （SHA-256雜湊） | `19900115` |
| [!UICONTROL Gender] | 用於人口統計目標定位的客戶性別。 | 字串 | 選填 | M/F/O （SHA-256雜湊） | `M` |
| [!UICONTROL External ID] | 您的內部客戶識別碼。 | 字串 | 選填 | 任何唯一字串 | `customer_12345` |
| [!UICONTROL Street Address] | 客戶的街道地址。 | 字串 | 選填 | SHA-256雜湊 | `123 Main Street` （雜湊） |
| [!UICONTROL City] | 客戶的城市。 | 字串 | 選填 | SHA-256雜湊 | `San Francisco` （雜湊） |
| [!UICONTROL State] | 客戶的州/省。 | 字串 | 選填 | 雙字母代碼（SHA-256雜湊） | `CA` （雜湊） |
| [!UICONTROL Zip Code] | 客戶的郵遞區號。 | 字串 | 選填 | 美國的前5位數（SHA-256雜湊） | `94102` （雜湊） |
| [!UICONTROL Country] | 客戶的國家/地區。 | 字串 | 選填 | ISO-3166-1 alpha-2 （SHA-256雜湊） | `US` （雜湊） |
| [!UICONTROL Click ID] | 歸因的下一個門點選識別碼。 | 字串 | 選填 | 已從`ndclid` URL引數擷取 | `nd_click_12345abcdef` |
| [!UICONTROL Client IP Address] | 使用者裝置的IP位址。 | 字串 | 選填 | Ipv4或IPv6位址 | `192.168.1.1` |
| [!UICONTROL Client User Agent] | 瀏覽器使用者代理字串。 | 字串 | 選填 | 原始瀏覽器使用者代理字串 | `Mozilla/5.0 (Windows...)` |

**自訂參數**

這些引數提供有關轉換事件的其他內容：

| 參數 | 說明 | 資料類型 | 必要 | 格式 | 範例 |
| ------------------------------ | ---------------------------------------------- | ------------------- | -------------------------------- | --------------------------------------- | ----------------------- |
| [!UICONTROL Order Value] | 購買交易的總值。 | 字串 | 購買事件需要&#x200B;**&#x200B;** | ISO 4217貨幣+金額（無空格） | `USD123.45` |
| [!UICONTROL Order ID] | 唯一交易或訂單識別碼。 | 字串 | 選填 | 任何唯一字串 | `order_12345` |
| [!UICONTROL Delivery Category] | 產品/服務交付方法。 | 字串 | 選填 | <ul><li>`in_store`</li><li>`curbside`</li><li>`home_delivery`</li></ul> | `home_delivery` |
| [!UICONTROL Product Context] | 有關購買產品的詳細資訊。 | 字串（JSON陣列） | 選填 | 產品物件的JSON陣列 | `[{"id":"SKU123","content_name":"Widget","item_price":29.99,"quantity":1}]` |

**行動應用程式引數**

`Action Source = 'APP'`時，您必須包含這些引數：

| 參數 | 說明 | 資料類型 | 必要 | 格式 | 範例 |
| --------------------------------- | --------------------------------------------- | --------- | --------------------------- | ----------------------------------------- | ----------------- |
| [!UICONTROL App ID*] | 行動應用程式識別碼。 | 字串 | 應用程式事件需要&#x200B;**&#x200B;** | <ul><li>套件ID (iOS)</li><li>封裝名稱(Android)</li></ul> | `com.company.app` |
| [!UICONTROL App Tracking Enabled] | iOS應用程式追蹤透明度同意狀態。 | 字串 | 應用程式事件需要&#x200B;**&#x200B;** | 布林值字串 | `true` |
| [!UICONTROL Platform] | 行動作業系統。 | 字串 | 應用程式事件需要&#x200B;**&#x200B;** | <ul><li>`iOS`</li><li>`Android`</li></ul> | `Android` |
| [!UICONTROL App Version] | 行動應用程式的版本。 | 字串 | 應用程式事件需要&#x200B;**&#x200B;** | 應用程式定義的版本字串 | `2.0.0-beta` |

## 事件類型 {#event-types}

不同的轉換案例支援下列事件型別：

| 活動名稱 | 活動類型 | 說明 | 使用案例 | 必要欄位 | 附註 |
| ------------------------ | ---------- | -------------------------------------- | --------------------------------------- | -------------------------------------- | ------------------------------------- |
| [!UICONTROL Purchase] | 標準 | 已完成的購買交易。 | 電子商務轉換 | <ul><li>活動名稱</li><li>訂單值</li><li>客戶資訊</li></ul> | 對於ROAS最佳化最重要 |
| [!UICONTROL Lead] | 標準 | 潛在客戶產生或查詢。 | 表單提交、連絡人要求 | <ul><li>活動名稱</li><li>客戶資訊</li></ul> | B2B的高值轉換 |
| [!UICONTROL Sign Up] | 標準 | 使用者註冊或帳戶建立。 | 電子報註冊、帳戶註冊 | <ul><li>活動名稱</li><li>客戶資訊</li></ul> | Top-funnel轉換追蹤 |
| [!UICONTROL Add to Cart] | 標準 | 產品已新增至購物車。 | 電子商務funnel追蹤 | <ul><li>活動名稱</li><li>客戶資訊</li></ul> | Mid-funnel參與訊號 |
| [!UICONTROL Initiate Checkout] | 標準 | 結帳程式已開始。 | 購買意圖追蹤 | <ul><li>活動名稱</li><li>客戶資訊</li></ul> | 強大的購買意向指標 |
| [!UICONTROL Page View] | 標準 | 已瀏覽的重要頁面。 | 內容參與，登陸頁面 | <ul><li>活動名稱</li><li>客戶資訊</li></ul> | 僅用於高價值頁面 |
| [!UICONTROL Search] | 標準 | 在網站上執行的搜尋。 | 產品/內容探索 | <ul><li>活動名稱</li><li>客戶資訊</li></ul> | 表示作用中的使用者參與 |
| [!UICONTROL View Content] | 標準 | 已檢視的內容或產品。 | 產品頁面檢視、內容參與 | <ul><li>活動名稱</li><li>客戶資訊</li></ul> | 對再行銷對象很有用 |
| [!UICONTROL Add to Wishlist] | 標準 | 產品已新增至願望清單。 | 未來購買意圖 | <ul><li>活動名稱</li><li>客戶資訊</li></ul> | 表示強烈的產品興趣 |
| [!UICONTROL Subscribe] | 標準 | 訂閱服務/電子報。 | 經常性收入、參與 | <ul><li>活動名稱</li><li>客戶資訊</li></ul> | 高期限值指標 |
| [!UICONTROL Custom Conversion 1 - 10] | 自訂 | 特定企業轉換事件。 | 定義您自己的轉換型別 | <ul><li>活動名稱</li><li>客戶資訊</li></ul> | 針對不重複的業務動作進行自訂 |

## 資料元素整合 {#data-element}

所有欄位都支援Adobe事件轉送資料元素。 選取任何欄位旁的資料元素圖示![資料元素](../../../images/extensions/server/nextdoor/data-element-icon.png)，以：

* **選取現有的資料元素**：從已建立的資料元素中選取。
* **新增資料元素**：視需要建立和定義新資料元素。
* **套用動態值**：將來自您網站的動態內容填入欄位。

## 最佳做法 {#best-practices}

請遵循這些最佳實務，以確保精確的轉換追蹤、改善資料品質並遵守隱私權法規。 這些建議可協助您將[!DNL Nextdoor] Conversion API整合發揮到極致，並最佳化您的廣告效能。

### 資料品質和隱私權法規遵循

正確的資料處理對於最大化轉換歸因正確性並同時維護使用者隱私和法規遵循至關重要。 這些實務有助於確保您的客戶資料格式正確、處理安全，並根據隱私權法規處理。

* **使用一致的資料格式**：一致地格式化電子郵件、電話號碼和其他資料：

   * **電子郵件標準化**：將電子郵件轉換為小寫、修剪空白字元，並從[!DNL Gmail]個地址移除點。
   * **電話號碼標準化**：使用E.164格式(+1234567890)以獲得國際相容性。
   * **位址標準化**：標準化街道縮寫(St.、Ave.、Rd.)，並移除任何額外的空格。
   * **名稱格式**：將名稱轉換為小寫、移除多餘的空格，並一致處理特殊字元。

* **雜湊敏感資料**：請考慮在傳送敏感客戶資料前先進行雜湊處理。 在雜湊處理前，請一律標準化資料，以確保一致的雜湊值：

   * 對電話號碼、地址及其他PII使用SHA-256雜湊。
   * 擴充功能會自動雜湊純文字電子郵件 — 您可以傳送任一格式。
   * 在所有追蹤實作中以雜湊資料一致的方式。
      * **範例**：在雜湊前將「John@Example.COM」→「john@example.com」標準化。

* **提供完整的資訊**：儘可能包含更多的客戶資訊，以更符合條件：

   * 可用時包含多個識別碼（電子郵件+電話，或電子郵件+姓名+地址）。
   * 使用外部客戶ID將轉換事件連結至您的CRM資料。
   * 提供人口統計資料（年齡、性別），前提是資料可用且符合隱私權法律。

* **同意管理**：確保您對資料收集有適當的同意：

   * 在收集客戶資料之前，實作適當的同意機制。
   * 遵守使用者選擇退出偏好設定和資料刪除請求。
   * 對已選擇退出之使用者使用「受限制的資料使用方式」引數。
   * **資源**：
      * [GDPR法規遵循指南](https://gdpr.eu/compliance/)
      * [CCPA隱私權要求](https://oag.ca.gov/privacy/ccpa)

* **資料最小化**：僅傳送轉換追蹤所需的資料：

   * 僅收集和傳送歸因和最佳化所需的資料。
   * 定期檢閱及稽核您傳送的資料欄位。
   * 移除不必要的客戶資訊，以降低隱私風險。

* **使用正確的時間戳記**：請確定事件時間戳記正確無誤，才能正確歸因。
   * 請使用轉換發生的實際時間，而非您處理資料時的實際時間。
   * 確保時間戳記採用Unix紀元格式（自1970年1月1日起的秒數）。
   * 計算時間戳記時的時區差異。

### 事件重複資料刪除

避免重複的轉換事件，以確保精確的行銷活動測量並避免誇大的績效量度。 實施適當的重複資料刪除，讓每個轉換只計算一次，為您的最佳化決策提供可靠的資料。

* **提供唯一事件ID**：一律使用唯一事件ID以避免重複轉換。
* **使用一致的命名**：在您的實作中套用一致的事件命名。

### 速率限制

[!DNL Nextdoor]轉換API受限於速率限制。 目前的速率限製為每位廣告商&#x200B;**100個請求/分鐘**。 如果您超過速率限制，API將會傳回`HTTP 429 Too Many Requests`錯誤碼。

## 結論 {#conclusion}

[!DNL Nextdoor] Conversion API Extension提供強大的方法來追蹤轉換，並測量[!DNL Nextdoor]廣告行銷活動的有效性。 依照本指南並實作最佳實務，您可以確保轉換追蹤準確無誤，並最佳化您的廣告效能。

如需最新資訊和其他資源，請造訪[[!DNL Nextdoor Ads Manager]](https://ads.nextdoor.com)。

## 後續步驟 {#next-steps}

本指南說明如何使用[!DNL Nextdoor] Conversion API擴充功能將伺服器端事件資料傳送至[!DNL Nextdoor]。 若要進一步瞭解[!DNL Adobe Experience Platform]中的事件轉送功能，請參閱[事件轉送概觀](../../../ui/event-forwarding/overview.md)。
