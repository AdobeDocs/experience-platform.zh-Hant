---
title: (Beta)交易台 — CRM連線
description: 對您的交易台帳戶啟用設定檔，以根據CRM資料進行受眾目標定位和隱藏。
last-substantial-update: 2023-01-25T00:00:00Z
exl-id: e09eaede-5525-4a51-a0e6-00ed5fdc662b
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '1148'
ht-degree: 5%

---

# (Beta) [!DNL Trade Desk] - CRM連線

>[!IMPORTANT]
>
>[!DNL The Trade Desk - CRM] Platform中的目的地目前是測試版。 檔案和功能可能會有所變更。
>
>隨著 EUID (歐洲統一 ID) 的發行，您現在可以查看兩個 [!DNL The Trade Desk - CRM] 目的地 (從[目的地目錄](/help/destinations/catalog/overview.md))。
>* 如果您要在歐盟獲取資料，請使用 **[!DNL The Trade Desk - CRM (EU)]** 目的地。
>* 如果您要在亞太 (APAC) 或北美 (NAMER) 區域獲取資料，請使用 **[!DNL The Trade Desk - CRM (NAMER & APAC)]** 目的地。
>
>Experience Platform中的兩個目的地目前都是測試版。 此目的地聯結器和檔案頁面是由 *[!DNL Trade Desk]* 團隊。 如有任何查詢或更新要求，請連絡 [!DNL Trade Desk] 代表，檔案和功能可能會有所變更。

## 概觀 {#overview}

本檔案旨在協助您對啟動設定檔 [!DNL Trade Desk] 根據CRM資料設定對象目標和隱藏的帳戶。

[!DNL The Trade Desk(TTD)] 不會隨時直接處理電子郵件地址的上傳檔案，也不會 [!DNL The Trade Desk] 儲存您的原始（未雜湊）電子郵件。

>[!TIP]
>
>使用 [!DNL The Trade Desk] CRM資料對應的CRM目的地，例如電子郵件或雜湊電子郵件地址。 使用 [其他交易台目的地](/help/destinations/catalog/advertising/tradedesk.md) Adobe Experience Platform目錄中的Cookie與裝置ID對應。

## 先決條件 {#prerequisites}

在您可以啟用對象之前，請 [!DNL The Trade Desk]，您必須聯絡 [!DNL The Trade Desk] 帳戶管理員簽署CRM入門合約。 [!DNL The Trade Desk] 然後會授予許可權並共用您的廣告商ID，以設定您的目的地。

## ID比對要求 {#id-matching-requirements}

根據您擷取至Adobe Experience Platform的ID型別，您必須遵守其對應的要求。 請閱讀 [身分名稱空間總覽](/help/identity-service/namespaces.md) 以取得詳細資訊。

## 支援的身分 {#supported-identities}

[!DNL The Trade Desk] 支援下表所述的身分啟用。 進一步瞭解 [身分](/help/identity-service/namespaces.md).

Adobe Experience Platform同時支援純文字和SHA256雜湊電子郵件地址。 請依照ID比對需求一節中的指示，針對純文字和雜湊電子郵件地址分別使用適當的名稱空間。

| 目標身分 | 說明 | 考量事項 |
|---|---|---|
| 電子郵件 | 電子郵件地址（純文字） | 輸入 `email` 當您的來源身分是電子郵件名稱空間或屬性時，作為目標身分。 |
| Email_LC_SHA256 | 電子郵件地址需要使用SHA256和小寫進行雜湊處理。 請務必遵循下列任一項 [電子郵件標準化](https://github.com/UnifiedID2/uid2docs/tree/main/api#email-address-normalization) 需要規則。 您稍後將無法變更此設定。 | 輸入 `hashed_email` 當您的來源身分是Email_LC_SHA256名稱空間或屬性時，作為目標身分。 |

{style="table-layout:auto"}

## 電子郵件雜湊需求 {#hashing-requirements}

您可以將電子郵件地址雜湊再擷取至Adobe Experience Platform中，或使用原始電子郵件地址。

若要瞭解如何在Experience Platform中擷取電子郵件地址，請參閱 [批次擷取概觀](/help/ingestion/batch-ingestion/overview.md).

如果您選擇自行雜湊電子郵件地址，請務必遵守下列要求：

* 移除開頭和結尾的空格。
* 將所有ASCII字元轉換為小寫。
* 在 `gmail.com` 電子郵件地址，從電子郵件地址的使用者名稱部分移除下列字元：
   * 句點(. （ASCII代碼46）。 例如，標準化 `jane.doe@gmail.com` 至 `janedoe@gmail.com`.
   * 加號(+ （ASCII代碼43）)和所有後續字元。 例如，標準化 `janedoe+home@gmail.com` 至 `janedoe@gmail.com`.

## 匯出型別和頻率 {#export-type-frequency}

請參閱下表以取得目的地匯出型別和頻率的資訊。

| 項目 | 類型 | 附註 |
---------|----------|---------|
| 匯出型別 | **[!UICONTROL 對象匯出]** | 您正在匯出某個對象的所有成員，其中包含交易台目的地所使用的識別碼（電子郵件或雜湊電子郵件）。 |
| 匯出頻率 | **[!UICONTROL 每日批次]** | 由於設定檔會根據對象評估在Experience Platform中更新，因此設定檔（身分）會每天更新一次，從下游到目的地平台。 深入瞭解 [批次匯出](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## 連線到目標 {#connect}

### 驗證至目的地 {#authenticate}

[!DNL The Trade Desk] CRM目的地是每日批次檔案上傳，不需要使用者驗證。

### 填寫目的地詳細資料 {#fill-in-details}

您必須先設定與您自己的目的地平台的連線，才能將對象資料傳送或啟用至目的地。 當 [設定](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html) 您必須提供下列資訊給此目的地：

* **[!UICONTROL 帳戶型別]**：請選擇 **[!UICONTROL 現有帳戶]** 選項。
* **[!UICONTROL 名稱]**：您日後可辨識此目的地的名稱。
* **[!UICONTROL 說明]**：可協助您日後識別此目的地的說明。
* **[!UICONTROL 廣告商ID]**：您的 [!DNL Trade Desk Advertiser ID]，可由您的網站共用 [!DNL Trade Desk] 客戶經理或位於以下位置： [!DNL Advertiser Preferences] 在 [!DNL Trade Desk] UI。

![顯示如何填寫目的地詳細資訊的平台UI熒幕擷圖。](/help/destinations/assets/catalog/advertising/tradedesk/configuredestination2.png)

連線到目的地時，設定資料治理原則是完全選用的。 請檢閱Experience Platform [資料治理總覽](/help/data-governance/policies/overview.md) 以取得更多詳細資料。

## 啟動此目標的對象 {#activate}

>[!IMPORTANT]
> 
>* 若要啟用資料，您需要 **[!UICONTROL 管理目的地]**， **[!UICONTROL 啟用目的地]**， **[!UICONTROL 檢視設定檔]**、和 **[!UICONTROL 檢視區段]** [存取控制許可權](/help/access-control/home.md#permissions). 閱讀 [存取控制總覽](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得必要許可權。
>* 要匯出 *身分*，您需要 **[!UICONTROL 檢視身分圖表]** [存取控制許可權](/help/access-control/home.md#permissions). <br> ![選取工作流程中反白顯示的身分名稱空間，以將對象啟用至目的地。](/help/destinations/assets/overview/export-identities-to-destination.png "選取工作流程中反白顯示的身分名稱空間，以將對象啟用至目的地。"){width="100" zoomable="yes"}

讀取 [啟用對象資料至批次設定檔匯出目的地](/help/destinations/ui/activate-batch-profile-destinations.md) 以取得啟用目標對象的指示。

在 **[!UICONTROL 正在排程]** 頁面，您可以為要匯出的每個對象設定排程和檔案名稱。 必須設定排程，但可選擇是否設定檔案名稱。

![平台UI熒幕擷取畫面可排程對象啟用。](/help/destinations/assets/catalog/advertising/tradedesk/schedulesegment1.png)

>[!NOTE]
>
>所有啟用對象至 [!DNL The Trade Desk] CRM目的地會自動設定為每日頻率和完整檔案匯出。

![平台UI熒幕擷取畫面可排程對象啟用。](/help/destinations/assets/catalog/advertising/tradedesk/schedulesegment2.png)

在 **[!UICONTROL 對應]** 頁面，您必須從來源資料欄選取屬性或身分識別名稱空間，並對應至目標資料欄。

![用於對應對象啟用的平台UI熒幕擷取畫面。](/help/destinations/assets/catalog/advertising/tradedesk/mappingsegment1.png)

以下範例說明將受眾啟用至時正確的身分對應 [!DNL The Trade Desk] CRM目的地。

>[!IMPORTANT]
>
> [!DNL The Trade Desk] CRM目的地不接受原始和雜湊電子郵件地址作為相同啟用流程中的身分。 為原始和雜湊電子郵件地址建立個別啟用流程。

選取來源欄位：

* 選取 `Email` 使用原始電子郵件地址進行資料擷取時，以名稱空間或屬性作為來源身分。
* 選取 `Email_LC_SHA256` 如果您在資料擷取至Platform時雜湊客戶電子郵件地址，請使用名稱空間或屬性作為來源身分。

選取目標欄位：

* 輸入  `email` 當來源名稱空間或屬性為 `Email`.
* 輸入  `hashed_email` 當來源名稱空間或屬性為 `Email_LC_SHA256`.

## 驗證資料匯出 {#validate}

驗證資料是否已正確從Experience Platform匯出並匯入 [!DNL The Trade Desk]，請在「Adobe1PD」資料方塊下找到對象，在 [!DNL The Trade Desk] 資料管理平台(DMP)。 以下是尋找內對應ID的步驟 [!DNL Trade Desk] UI：

1. 首先，按一下 **[!UICONTROL 資料]** 標籤和檢閱 **[!UICONTROL 第一方]**.
2. 向下捲動頁面，在底下 **[!UICONTROL 匯入的資料]**，您會找到 **[!UICONTROL Adobe1PD圖磚]**.
3. 按一下**[!UICONTROL Adobe1PD]**圖磚，會列出所有啟用至 [!DNL Trade Desk] 您的廣告商目的地。 您也可以使用搜尋功能。
4. Experience Platform的區段ID #會顯示為 [!DNL Trade Desk] UI。

## 資料使用與控管 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 處理您的資料時，目的地符合資料使用原則。 如需如何操作的詳細資訊 [!DNL Adobe Experience Platform] 強制執行資料控管，請參閱 [資料控管概觀](/help/data-governance/home.md).
