---
title: 交易台 — CRM連線
description: 對您的交易台帳戶啟用設定檔，以根據CRM資料進行受眾目標定位和隱藏。
last-substantial-update: 2025-01-16T00:00:00Z
exl-id: e09eaede-5525-4a51-a0e6-00ed5fdc662b
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1122'
ht-degree: 5%

---

# [!DNL Trade Desk] - CRM連線

>[!IMPORTANT]
>
>隨著 EUID (歐洲統一 ID) 的發行，您現在可以查看兩個 [!DNL The Trade Desk - CRM] 目的地 (從[目的地目錄](/help/destinations/catalog/overview.md))。
>* 如果您要在歐盟獲取資料，請使用 **[!DNL The Trade Desk - CRM (EU)]** 目的地。
>* 如果您要在亞太 (APAC) 或北美 (NAMER) 區域獲取資料，請使用 **[!DNL The Trade Desk - CRM (NAMER & APAC)]** 目的地。
>
>此目的地聯結器和檔案頁面是由&#x200B;*[!DNL Trade Desk]*&#x200B;團隊建立和維護。 若有任何查詢或更新要求，請連絡您的[!DNL Trade Desk]代表。

## 概觀 {#overview}

瞭解如何為您的[!DNL Trade Desk]帳戶啟用設定檔，以根據CRM資料鎖定受眾目標和隱藏。

此聯結器會將資料傳送至[!DNL The Trade Desk]第一方端點。 Adobe Experience Platform與[!DNL The Trade Desk]之間的整合不支援匯出資料至[!DNL The Trade Desk]第三方端點。

[!DNL The Trade Desk(TTD)]不會隨時直接處理電子郵件地址的上傳檔案，[!DNL The Trade Desk]也不會儲存您的原始（未雜湊）電子郵件。

>[!TIP]
>
>使用[!DNL The Trade Desk]個CRM目的地進行CRM資料對應，例如電子郵件或雜湊電子郵件地址。 使用Adobe Experience Platform目錄中的[其他交易台目的地](/help/destinations/catalog/advertising/tradedesk.md)進行Cookie和裝置ID對應。

## 先決條件 {#prerequisites}

>[!IMPORTANT]
>
>您必須先聯絡您的[!DNL Trade Desk]客戶經理以簽署CRM入門合約，才能在交易台啟用對象。 [!DNL The Trade Desk]將啟用UID2 / EUID的使用並共用其他詳細資料來協助您設定目的地。

## ID比對要求 {#id-matching-requirements}

根據您擷取至Adobe Experience Platform的ID型別，您必須遵守其對應的要求。 如需詳細資訊，請閱讀[身分名稱空間概觀](/help/identity-service/features/namespaces.md)。

## 支援的身分 {#supported-identities}

[!DNL The Trade Desk]支援下表所述的身分啟用。 深入瞭解[身分](/help/identity-service/features/namespaces.md)。

Adobe Experience Platform同時支援純文字和SHA256雜湊電子郵件地址。 請依照ID比對需求一節中的指示，針對純文字和雜湊電子郵件地址分別使用適當的名稱空間。

| 目標身分 | 說明 | 考量事項 |
|---|---|---|
| 電子郵件 | 電子郵件地址（純文字） | 當您的來源識別是電子郵件名稱空間或屬性時，請輸入`email`作為目標識別。 |
| Email_LC_SHA256 | 電子郵件地址需要使用SHA256和小寫進行雜湊處理。 您稍後將無法變更此設定。 | 當您的來源身分是Email_LC_SHA256名稱空間或屬性時，輸入`hashed_email`作為目標身分。 |

{style="table-layout:auto"}

## 電子郵件雜湊需求 {#hashing-requirements}

您可以將電子郵件地址雜湊再擷取至Adobe Experience Platform中，或使用原始電子郵件地址。

若要瞭解如何在Experience Platform中擷取電子郵件地址，請閱讀[批次擷取總覽](/help/ingestion/batch-ingestion/overview.md)。

如果您選擇自行雜湊電子郵件地址，請務必遵守下列要求：

* 移除開頭和結尾的空格。
* 將所有ASCII字元轉換為小寫。
* 在`gmail.com`個電子郵件地址中，從電子郵件地址的使用者名稱部分移除下列字元：
   * 句點(. （ASCII代碼46）。 例如，將`jane.doe@gmail.com`標準化為`janedoe@gmail.com`。
   * 加號(+ （ASCII代碼43）)和所有後續字元。 例如，將`janedoe+home@gmail.com`標準化為`janedoe@gmail.com`。

## 匯出型別和頻率 {#export-type-frequency}

請參閱下表以取得目的地匯出型別和頻率的資訊。

| 項目 | 類型 | 附註 |
---------|----------|---------|
| 匯出類型 | **[!UICONTROL 對象匯出]** | 您正在匯出某個對象的所有成員，其中包含交易台目的地所使用的識別碼（電子郵件或雜湊電子郵件）。 |
| 匯出頻率 | **[!UICONTROL 每日批次]** | 由於設定檔會根據對象評估在Experience Platform中更新，因此設定檔（身分）會每天更新一次，從下游到目的地平台。 深入瞭解[批次匯出](/help/destinations/destination-types.md#file-based)。 |

{style="table-layout:auto"}

## 連線到目標 {#connect}

### 驗證至目的地 {#authenticate}

[!DNL The Trade Desk] CRM目的地是每日批次檔案上傳，不需要使用者驗證。

### 填寫目的地詳細資料 {#fill-in-details}

您必須先設定與您自己的目的地平台的連線，才能將對象資料傳送或啟用至目的地。 在[設定](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html)此目的地時，您必須提供下列資訊：

* **[!UICONTROL 帳戶型別]**：請選擇&#x200B;**[!UICONTROL 現有帳戶]**&#x200B;選項。
* **[!UICONTROL 名稱]**：您日後可辨識此目的地的名稱。
* **[!UICONTROL 描述]**：可協助您日後識別此目的地的描述。
* **[!UICONTROL 廣告商ID]**：您的[!DNL Trade Desk Advertiser ID]，可由您的[!DNL Trade Desk]帳戶管理員共用，或可在[!DNL Trade Desk] UI的[!DNL Advertiser Preferences]下找到。

![Experience Platform UI熒幕擷圖顯示如何填寫目的地詳細資料。](/help/destinations/assets/catalog/advertising/tradedesk/configuredestination2.png)

連線到目的地時，設定資料治理原則是完全選用的。 如需詳細資訊，請檢閱Experience Platform [資料控管概觀](/help/data-governance/policies/overview.md)。

## 啟動此目標的對象 {#activate}

>[!IMPORTANT]
> 
>* 若要啟用資料，您需要&#x200B;**[!UICONTROL 檢視目的地]**、**[!UICONTROL 啟用目的地]**、**[!UICONTROL 檢視設定檔]**&#x200B;和&#x200B;**[!UICONTROL 檢視區段]** [存取控制許可權](/help/access-control/home.md#permissions)。 閱讀[存取控制總覽](/help/access-control/ui/overview.md)或連絡您的產品管理員以取得必要的許可權。
>* 若要匯出&#x200B;*身分*，您需要&#x200B;**[!UICONTROL 檢視身分圖表]** [存取控制許可權](/help/access-control/home.md#permissions)。<br> ![選取工作流程中反白的身分名稱空間，以啟用目的地的對象。](/help/destinations/assets/overview/export-identities-to-destination.png "選取工作流程中反白顯示的身分名稱空間，以啟用目的地的對象。"){width="100" zoomable="yes"}

讀取[啟用批次設定檔匯出目的地的對象資料](/help/destinations/ui/activate-batch-profile-destinations.md)，以取得啟用對象至目的地的指示。

在&#x200B;**[!UICONTROL 排程]**&#x200B;頁面中，您可以設定排程和要匯出之每個對象的檔案名稱。 必須設定排程，但可選擇是否設定檔案名稱。

![Experience Platform UI熒幕擷圖以排程對象啟用。](/help/destinations/assets/catalog/advertising/tradedesk/schedulesegment1.png)

>[!NOTE]
>
>所有啟用至[!DNL The Trade Desk] CRM目的地的對象都會自動設定為每日頻率和完整檔案匯出。

![Experience Platform UI熒幕擷圖以排程對象啟用。](/help/destinations/assets/catalog/advertising/tradedesk/schedulesegment2.png)

在&#x200B;**[!UICONTROL 對應]**&#x200B;頁面中，您必須從來源資料行選取屬性或身分識別名稱空間，並對應到目標資料行。

![用來對應對象啟用的Experience Platform UI熒幕擷取畫面。](/help/destinations/assets/catalog/advertising/tradedesk/mappingsegment1.png)

以下是啟用對象至[!DNL The Trade Desk] CRM目的地時的正確身分對應範例。

>[!IMPORTANT]
>
> [!DNL The Trade Desk] CRM目的地不接受原始和雜湊電子郵件地址作為相同啟用流程中的身分。 為原始和雜湊電子郵件地址建立個別啟用流程。

選取來源欄位：

* 如果在資料擷取時使用原始電子郵件地址，請選取`Email`名稱空間或屬性作為來源身分。
* 如果您在資料擷取至Experience Platform時雜湊了客戶電子郵件地址，請選取`Email_LC_SHA256`名稱空間或屬性作為來源身分。

選取目標欄位：

* 當來源名稱空間或屬性為`Email`時，輸入`email`作為目標身分。
* 當來源名稱空間或屬性為`Email_LC_SHA256`時，輸入`hashed_email`作為目標身分。

## 驗證資料匯出 {#validate}

若要驗證資料是否已正確從Experience Platform匯出並匯入[!DNL The Trade Desk]，請在[!DNL The Trade Desk]資料管理平台(DMP)的Adobe 1PD資料方塊下找到對象。 以下是在[!DNL Trade Desk] UI中尋找對應ID的步驟：

1. 首先，選取&#x200B;**[!UICONTROL 資料]**&#x200B;標籤，並檢閱&#x200B;**[!UICONTROL 第一方]**&#x200B;區段。
2. 向下捲動頁面，在&#x200B;**[!UICONTROL 匯入的資料]**&#x200B;下方，您會找到&#x200B;**[!UICONTROL Adobe 1PD磚]**。
3. 按一下**[!UICONTROL Adobe 1PD]**圖磚，系統會列出所有啟用至廣告商[!DNL Trade Desk]目的地的對象。 您也可以使用搜尋功能。
4. 來自Experience Platform的區段ID #將顯示為[!DNL Trade Desk] UI中的區段名稱。

## 資料使用與控管 {#data-usage-governance}

處理您的資料時，所有[!DNL Adobe Experience Platform]目的地都符合資料使用原則。 如需[!DNL Adobe Experience Platform]如何強制資料控管的詳細資訊，請參閱[資料控管概觀](/help/data-governance/home.md)。
