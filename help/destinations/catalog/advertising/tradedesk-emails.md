---
title: 交易台 — CRM連線
description: 對您的交易台帳戶啟用設定檔，以根據CRM資料進行受眾目標定位和隱藏。
last-substantial-update: 2025-01-16T00:00:00Z
exl-id: e09eaede-5525-4a51-a0e6-00ed5fdc662b
source-git-commit: 47d4078acc73736546d4cbb2d17b49bf8945743a
workflow-type: tm+mt
source-wordcount: '1643'
ht-degree: 2%

---

# [!DNL Trade Desk] - CRM連線

>[!IMPORTANT]
>
>[目的地目錄](/help/destinations/catalog/overview.md)中有兩個Trade Desk - CRM目的地。
>
>* 如果您將資料來源設在歐盟，請使用&#x200B;**[!DNL The Trade Desk - CRM (EU)]**&#x200B;目的地。
>* 如果您在APAC或NAMER地區取得資料來源，請使用&#x200B;**[!DNL The Trade Desk - CRM (NAMER & APAC)]**&#x200B;目的地。
>
>此目的地聯結器和檔案頁面是由&#x200B;*[!DNL Trade Desk]*&#x200B;團隊建立和維護。 若有任何查詢或更新要求，請連絡您的[!DNL Trade Desk]代表。

## 概觀 {#overview}

瞭解如何為您的[!DNL Trade Desk]帳戶啟用設定檔，以根據CRM資料鎖定受眾目標和隱藏。

此聯結器會將資料傳送至[!DNL The Trade Desk]以進行第一方資料啟用。 [!DNL The Trade Desk]儲存您的原始（未雜湊）電子郵件和電話號碼。

>[!TIP]
>
>使用[!DNL The Trade Desk - CRM]目的地來傳送CRM資料（例如電子郵件和電話號碼）和其他第一方資料識別碼（例如Cookie和裝置ID）。 您可以繼續使用Experience Platform目錄中的[交易台目的地](/help/destinations/catalog/advertising/tradedesk.md)來進行Cookie與裝置ID對應。

## 先決條件 {#prerequisites}

>[!IMPORTANT]
>
>您必須先連絡您的[!DNL Trade Desk]客戶經理以啟用此功能，才能啟用交易台的對象。 如果您要傳送電子郵件、電話號碼和UID2/EUID，您必須與[!DNL The Trade Desk]共用已簽署的UID2/EUID合約。

## ID比對要求 {#id-matching-requirements}

根據您擷取至Adobe Experience Platform的ID型別，您必須遵守其對應的要求。 如需詳細資訊，請閱讀[身分名稱空間概觀](/help/identity-service/features/namespaces.md)。

## 支援的身分 {#supported-identities}

[!DNL The Trade Desk]支援下表所述的身分啟用。 深入瞭解[身分](/help/identity-service/features/namespaces.md)。

Adobe Experience Platform支援非雜湊和雜湊電子郵件地址和電話號碼。 請依照ID比對需求一節中的指示，針對純文字和雜湊電子郵件地址分別使用適當的名稱空間。

| 目標身分 | 說明 |
|---|---|
| 電子郵件 | 電子郵件地址（純文字） |
| Email_LC_SHA256 | 電子郵件地址需要使用SHA256和小寫進行雜湊處理。 您稍後將無法變更此設定。 |
| 電話(E.164) | 需要以E.164格式正規化的電話號碼。 E.164格式包含加號(+)、國際國家/地區撥號代碼、當地區碼和電話號碼。 例如：(+)（國家代碼）（區號）（電話號碼）。 此識別碼不適用於交易台 — 第一方資料(EU)。 |
| 電話(SHA256_E.164) | 電話號碼已標準化為E.164格式，然後使用SHA-256進行雜湊處理，並產生雜湊的Base64編碼。 此識別碼不適用於交易台 — 第一方資料(EU)。 |
| TDID | 交易台中的Cookie ID |
| GAID | GOOGLE ADVERTISING ID |
| IDFA | 廣告商適用的Apple ID |
| UID2 | 原始UID2值 |
| UID2Token | 加密的UID2 Token，也稱為廣告代號。 |
| EUID | 原始歐盟ID值 |
| EUIDToken | 加密的EUID權杖，也稱為廣告權杖。 |
| 斜坡ID | 49個字元或70個字元的RampID （先前稱為IdentityLink或IDL）。 這必須是來自LiveRamp且專為Trade Desk對應的RampID。 |
| netID | 使用者的netID，如70個字元的base64編碼字串。 此ID僅於歐洲支援。 |
| 第一ID | 使用者的第一方ID，即通常由法國發佈者設定的第一方Cookie。 此ID僅於歐洲支援。 |

{style="table-layout:auto"}

## 電子郵件雜湊需求 {#email-hashing}

您可以將電子郵件地址雜湊再擷取至Adobe Experience Platform中，或使用原始電子郵件地址。

若要瞭解如何在Experience Platform中擷取電子郵件地址，請閱讀[批次擷取總覽](/help/ingestion/batch-ingestion/overview.md)。

如果您選擇自行雜湊電子郵件地址，請務必遵守下列要求：

* 移除開頭和結尾的空格。
* 將所有ASCII字元轉換為小寫。
* 在`gmail.com`個電子郵件地址中，從電子郵件地址的使用者名稱部分移除下列字元：

      *句點(&#39;.&#39;) 字元（ASCII代碼46）。 例如，將「jane.doe@gmail.com」標準化為「janedoe@gmail.com」。
     *加號(&#39;+&#39;)字元（ASCII代碼43）和所有後續字元。 例如，將&#39;janedoe+home@gmail.com&#39;標準化為&#39;janedoe@gmail.com&#39;。
  

## 電話號碼正規化和雜湊需求 {#phone-hashing}

以下是上傳電話號碼時您需要瞭解的事項：

* 無論您是在要求中傳送雜湊或解除雜湊的電話號碼，都必須在要求中傳送號碼前將其標準化。
* 若要上傳標準化、雜湊和編碼的資料，您必須以標準化電話號碼的Base64編碼SHA-256雜湊傳送。

無論您是要上傳原始或雜湊的電話號碼，您都必須將其標準化。

>[!IMPORTANT]
>
>在雜湊處理前進行標準化可確保產生的ID值永遠相同，而且可準確比對資料。

以下是您需要瞭解的電話號碼標準化要求：

* UID2電信業者接受E.164格式的電話號碼，這是可確保全域唯一性的國際電話號碼格式。
* E.164電話號碼最多可有15位數。
* 標準化的E.164電話號碼使用下列語法： `[+][country code][subscriber number including area code]`不含空格、連字型大小、括弧或其他特殊字元。 以下是一些範例：

      *美國： 1 (234) 567-8901已標準化為+12345678901。
     *新加坡： 65 1243 5678已標準化為+6512345678。
     *澳洲：行動電話號碼0491 570 006已標準化，以新增國碼並捨棄前導零： +61491570006。
     * UK：行動電話號碼07812 345678已標準化，以新增國碼並捨棄前導零： +447812345678。
  
請確定標準化電話號碼是UTF-8，而不是其他編碼系統，例如UTF-16。

電話號碼雜湊是標準化電話號碼的Base64編碼SHA-256雜湊。 首先標準化電話號碼，然後使用SHA-256雜湊演演算法執行雜湊處理，接著使用Base64編碼來編碼雜湊值的結果位元組。 請注意，Base64編碼會套用至雜湊值的位元組，而非十六進位編碼字串表示法。
下表顯示簡單輸入電話號碼的範例，以及套用每個步驟以得到安全、不透明值的結果。

| 類型 | 範例 | 註解和使用情況 |
|---|---|---|
| 原始電話號碼 | 1 (234) 567-8901 | 這是起點。 |
| 標準化電話號碼 | +12345678901 | 標準化永遠是第一步。 |
| 標準化電話號碼的SHA-256雜湊 | 10e6f0b47054a83359477dcb35231db6de5c69fb1816e1a6b98e192de9e5b9ee | 此64個字元的字串是32位元組SHA-256的十六進位編碼表示法。 |
| 規範化和雜湊電話號碼的十六進位至Base64 SHA-256編碼 | EObwtHBUqDNZR33LNSMdtt5cafsYFuGmuY4ZLenlue4 | 此44個字元的字串是32位元組SHA-256的Base64編碼表示法。 SHA-256雜湊是十六進位值。 您必須使用以十六進位值作為輸入的Base64編碼器。 對要求內文中傳送的phone_hash值使用此編碼。 |

>[!IMPORTANT]
>
>套用Base64編碼時，請務必使用接受十六進位值作為輸入的函式。 如果您使用接受文字作為輸入的函式，則結果會是較長的字串，對UID2而言無效。

## 匯出型別和頻率 {#export-type-frequency}

請參閱下表以取得目的地匯出型別和頻率的資訊。

| 項目 | 類型 | 附註 |
|---------|----------|---------|
| 匯出類型 | **[!UICONTROL Audience export]** | 您正在匯出某個對象的所有成員，其中包含交易台目的地所使用的識別碼（電子郵件或雜湊電子郵件）。 |
| 匯出頻率 | **[!UICONTROL Daily Batch]** | 由於設定檔會根據對象評估在Experience Platform中更新，因此設定檔（身分）會每天更新一次，從下游到目的地平台。 深入瞭解[批次匯出](/help/destinations/destination-types.md#file-based)。 |

{style="table-layout:auto"}

## 連線到目標 {#connect}

### 驗證至目的地 {#authenticate}

[!DNL The Trade Desk] CRM目的地是每日批次檔案上傳，不需要使用者驗證。

### 填寫目的地詳細資料 {#fill-in-details}

您必須先設定與您自己的目的地平台的連線，才能將對象資料傳送或啟用至目的地。 在[設定](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html)此目的地時，您必須提供下列資訊：

* **[!UICONTROL Account Type]**：請選擇&#x200B;**[!UICONTROL Existing Account]**&#x200B;選項。
* **[!UICONTROL Name]**：您日後可辨識此目的地的名稱。
* **[!UICONTROL Description]**：可協助您日後識別此目的地的說明。
* **[!UICONTROL Advertiser ID]**：您的[!DNL Trade Desk Advertiser ID]，可由您的[!DNL Trade Desk]帳戶管理員共用，或可在[!DNL Advertiser Preferences] UI的[!DNL Trade Desk]下找到。

![Experience Platform UI熒幕擷圖顯示如何填寫目的地詳細資料。](/help/destinations/assets/catalog/advertising/tradedesk/configuredestination2.png)

連線到目的地時，設定資料治理原則是完全選用的。 如需詳細資訊，請檢閱Experience Platform [資料控管概觀](/help/data-governance/policies/overview.md)。

## 啟動此目標的對象 {#activate}

>[!IMPORTANT]
> 
>* 若要啟用資料，您需要&#x200B;**[!UICONTROL View Destinations]**、**[!UICONTROL Activate Destinations]**、**[!UICONTROL View Profiles]**&#x200B;和&#x200B;**[!UICONTROL View Segments]** [存取控制許可權](/help/access-control/home.md#permissions)。 閱讀[存取控制總覽](/help/access-control/ui/overview.md)或連絡您的產品管理員以取得必要的許可權。
>* 若要匯出&#x200B;*身分*，您需要&#x200B;**[!UICONTROL View Identity Graph]** [存取控制許可權](/help/access-control/home.md#permissions)。<br> ![選取工作流程中反白的身分名稱空間，以啟用目的地的對象。](/help/destinations/assets/overview/export-identities-to-destination.png "選取工作流程中反白顯示的身分名稱空間，以啟用目的地的對象。"){width="100" zoomable="yes"}

讀取[啟用批次設定檔匯出目的地的對象資料](/help/destinations/ui/activate-batch-profile-destinations.md)，以取得啟用對象至目的地的指示。

在&#x200B;**[!UICONTROL Scheduling]**&#x200B;頁面中，您可以針對要匯出的每個對象設定排程和檔案名稱。 必須設定排程，但可選擇是否設定檔案名稱。

![Experience Platform UI熒幕擷圖以排程對象啟用。](/help/destinations/assets/catalog/advertising/tradedesk/schedulesegment1.png)

>[!NOTE]
>
>所有啟用至[!DNL The Trade Desk] CRM目的地的對象都會自動設定為每日頻率和完整檔案匯出。

![Experience Platform UI熒幕擷圖以排程對象啟用。](/help/destinations/assets/catalog/advertising/tradedesk/schedulesegment2.png)

在&#x200B;**[!UICONTROL Mapping]**&#x200B;頁面中，您必須從來源資料行選取屬性或身分識別名稱空間，並對應至目標資料行。

![用來對應對象啟用的Experience Platform UI熒幕擷取畫面。](/help/destinations/assets/catalog/advertising/tradedesk/mappingsegment1.png)

以下是啟用對象至[!DNL The Trade Desk] CRM目的地時的正確身分對應範例。

選取來源和目標欄位：

| 來源欄位 | 目標欄位 |
|---|---|
| 電子郵件 | 電子郵件 |
| Email_LC_SHA256 | hashed_email |
| 電話(E.164) | 電話 |
| 電話(SHA256_E.164) | hashed_phone |
| TDID | tdid |
| GAID | daid |
| IDFA | idfa |
| UID2 | uid2 |
| UID2Token | uid2_token |
| EUID | euid |
| EUIDToken | euid_token |
| 斜坡ID | idl |
| ID5 | id5 |
| netID | net_id |
| 第一ID | first_id |


## 驗證資料匯出 {#validate}

若要驗證資料是否已正確從Experience Platform匯出並匯入[!DNL The Trade Desk]，請在[!DNL The Trade Desk]「廣告商資料和身分」資料庫的Adobe 1PD標籤下找到對象。 以下是在[!DNL Trade Desk] UI中尋找對應ID的步驟：

1. 首先，選取「**[!UICONTROL Libraries]**」標籤，並檢閱「**[!UICONTROL Advertiser data and identity]**」區段。
2. 按一下&#x200B;**[!UICONTROL Adobe 1PD]**，它就會列出所有啟用至[!DNL The Trade Desk]的對象。
3. Experience Platform的區段名稱或區段ID會顯示為[!DNL Trade Desk] UI中的區段名稱。

## 資料使用與控管 {#data-usage-governance}

處理您的資料時，所有[!DNL Adobe Experience Platform]目的地都符合資料使用原則。 如需[!DNL Adobe Experience Platform]如何強制資料控管的詳細資訊，請參閱[資料控管概觀](/help/data-governance/home.md)。
