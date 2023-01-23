---
title: （測試版）交易台 — CRM連接
description: 將設定檔啟用至您的交易台帳戶，以根據CRM資料鎖定受眾並抑制受眾。
exl-id: e09eaede-5525-4a51-a0e6-00ed5fdc662b
source-git-commit: 271a9ad9848db855372a4ce5346f97cf48400901
workflow-type: tm+mt
source-wordcount: '1084'
ht-degree: 1%

---

# （測試版） [!DNL Trade Desk] - CRM連線

>[!IMPORTANT]
>
>[!DNL The Trade Desk - CRM] Platform中的目的地目前為測試版。 檔案和功能可能會有所變更。
>
>隨著EUID（歐洲統一ID）的發行，您現在會看到兩個 [!DNL The Trade Desk - CRM] 目的地 [目的地目錄](/help/destinations/catalog/overview.md).
>* 如果您在歐盟中來源資料，請使用 **[!DNL The Trade Desk - CRM (EU)]** 目的地。
>* 如果您在APAC或NAMER地區來源資料，請使用 **[!DNL The Trade Desk - CRM (NAMER & APAC)]** 目的地。
>
>Experience Platform中的兩個目的地目前都是測試版。 本檔案頁面由 *[!DNL Trade Desk]* 團隊。 如有任何查詢或更新請求，請聯繫您的 [!DNL Trade Desk] 代表：說明檔案和功能可能會有所變更。

## 總覽 {#overview}

本檔案旨在協助您為 [!DNL Trade Desk] 帳戶，以根據CRM資料鎖定和隱藏對象。

[!DNL The Trade Desk(TTD)] 不會隨時直接處理電子郵件地址的上傳檔案，也不會 [!DNL The Trade Desk] 儲存原始（未雜湊）電子郵件。

>[!TIP]
>
>使用 [!DNL The Trade Desk] 用於CRM資料對應的CRM目的地，例如電子郵件或雜湊電子郵件地址。 使用 [其他交易台目的地](/help/destinations/catalog/advertising/tradedesk.md) 在Adobe Experience Platform目錄中，取得cookie和裝置ID對應。

## 先決條件 {#prerequisites}

啟用區段至 [!DNL The Trade Desk]，您必須連絡 [!DNL The Trade Desk] 客戶經理，以簽署CRM入門合約。 [!DNL The Trade Desk] 然後會授予權限並共用廣告商ID以設定您的目的地。

## ID比對需求 {#id-matching-requirements}

視您擷取至Adobe Experience Platform的ID類型而定，您必須遵守其對應要求。 請閱讀 [身分命名空間概觀](/help/identity-service/namespaces.md) 以取得更多資訊。

## 支援的身分 {#supported-identities}

[!DNL The Trade Desk] 支援啟用下表所述的身分。 深入了解 [身分](/help/identity-service/namespaces.md).

Adobe Experience Platform支援純文字和SHA256雜湊電子郵件地址。 請依照ID比對需求一節中的指示操作，並分別將適當的命名空間用於純文字和雜湊電子郵件地址。

| Target身分 | 說明 | 考量事項 |
|---|---|---|
| 電子郵件 | 電子郵件地址（清除文本） | 輸入 `email` 作為目標標識（如果源標識是電子郵件命名空間或屬性）。 |
| Email_LC_SHA256 | 電子郵件地址必須使用SHA256和小寫進行雜湊處理。 請務必遵循任何 [電子郵件標準化](https://github.com/UnifiedID2/uid2docs/tree/main/api#email-address-normalization) 規則為必要。 您以後將無法更改此設定。 | 輸入 `hashed_email` 當源標識為Email_LC_SHA256命名空間或屬性時，作為目標標識。 |

{style=&quot;table-layout:auto&quot;}

## 電子郵件雜湊要求 {#hashing-requirements}

您可以先雜湊電子郵件地址，再將其擷取至Adobe Experience Platform或使用原始電子郵件地址。

若要了解如何在Experience Platform中擷取電子郵件地址，請閱讀 [批次匯入概觀](/help/ingestion/batch-ingestion/overview.md).

如果您選取自行雜湊電子郵件地址，請務必符合下列要求：

* 移除前導和尾隨空格。
* 將所有ASCII字元轉換為小寫。
* 在 `gmail.com` 電子郵件地址中，從電子郵件地址的使用者名稱部分移除下列字元：
   * 期間(. （ASCII碼46）。 例如，標準化 `jane.doe@gmail.com` to `janedoe@gmail.com`.
   * 加號(+（ASCII碼43）)和所有後續字元。 例如，標準化 `janedoe+home@gmail.com` to `janedoe@gmail.com`.

## 匯出類型和頻率 {#export-type-frequency}

有關目標導出類型和頻率的資訊，請參閱下表。

| 項目 | 類型 | 附註 |
---------|----------|---------|
| 匯出類型 | **[!UICONTROL 區段匯出]** | 您正在匯出區段（對象）的所有成員，其中包含「交易台」目的地中使用的識別碼（電子郵件或雜湊電子郵件）。 |
| 匯出頻率 | **[!UICONTROL 每日批]** | 隨著根據區段評估在Experience Platform中更新設定檔，設定檔（身分）每天會在下游至目的地平台時更新一次。 深入了解 [批次匯出](/help/destinations/destination-types.md#file-based). |

{style=&quot;table-layout:auto&quot;}

## 連接到目標 {#connect}

### 驗證到目標 {#authenticate}

[!DNL The Trade Desk] CRM目標是每日批次檔案上傳，不需要使用者驗證。

### 填寫目標詳細資訊 {#fill-in-details}

您必須先設定與您自己的目的地平台的連線，才能傳送或啟用對象資料至目的地。 同時 [設定](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html?lang=en) 此目的地時，您必須提供下列資訊：

* **[!UICONTROL 帳戶類型]**:請選擇 **[!UICONTROL 現有帳戶]** 選項。
* **[!UICONTROL 名稱]**:日後您將透過此名稱識別此目的地。
* **[!UICONTROL 說明]**:未來可協助您識別此目的地的說明。
* **[!UICONTROL 廣告商ID]**:您的 [!DNL Trade Desk Advertiser ID]，您的 [!DNL Trade Desk] 客戶經理或 [!DNL Advertiser Preferences] 在 [!DNL Trade Desk] UI。

![Platform UI螢幕擷取畫面，顯示如何填入目的地詳細資訊。](/help/destinations/assets/catalog/advertising/tradedesk/configuredestination2.png)

連接到目標時，設定資料控管策略是完全可選的。 請查看Experience Platform [資料控管概觀](/help/data-governance/policies/overview.md) 以取得更多詳細資訊。

## 啟用此目的地的區段 {#activate}

閱讀 [啟用對象資料，以批次匯出設定檔目的地](/help/destinations/ui/activate-batch-profile-destinations.md) 關於在目的地啟用受眾區段的指示。

在 **[!UICONTROL 排程]** 頁面，您可以為要匯出的每個區段設定排程和檔案名稱。 必須設定排程，但設定檔案名稱為選用。

![Platform UI螢幕擷取畫面，排程區段啟動。](/help/destinations/assets/catalog/advertising/tradedesk/schedulesegment1.png)

>[!NOTE]
>
>所有已啟動至的區段 [!DNL The Trade Desk] CRM目標會自動設為每日頻率和完整檔案匯出。

![Platform UI螢幕擷取畫面，排程區段啟動。](/help/destinations/assets/catalog/advertising/tradedesk/schedulesegment2.png)

在 **[!UICONTROL 對應]** 頁，則必須從源列選擇屬性或標識命名空間，並映射到目標列。

![Platform UI螢幕擷取圖可對應區段啟用。](/help/destinations/assets/catalog/advertising/tradedesk/mappingsegment1.png)

以下是將區段啟用至時的正確身分對應範例 [!DNL The Trade Desk] CRM目的地。

>[!IMPORTANT]
>
> [!DNL The Trade Desk] CRM目的地不接受相同啟動流程中原始和雜湊電子郵件地址做為身分。 為原始和雜湊電子郵件地址建立個別的啟用流程。

選擇源欄位：

* 選取 `Email` 命名空間或屬性做為來源身分（若在資料擷取時使用原始電子郵件地址）。
* 選取 `Email_LC_SHA256` 將客戶電子郵件地址雜湊至Platform中時，使用命名空間或屬性做為來源身分。

選擇目標欄位：

* 輸入  `email` 作為目標標識（在您的源命名空間或屬性中） `Email`.
* 輸入  `hashed_email` 作為目標標識（在您的源命名空間或屬性中） `Email_LC_SHA256`.

## 驗證資料匯出 {#validate}

驗證資料是否正確匯出至Experience Platform外，並匯入 [!DNL The Trade Desk]，請在的「Adobe1PD資料」方塊下方找到區段 [!DNL The Trade Desk] 資料管理平台(DMP)。 以下是在中尋找對應ID的步驟 [!DNL Trade Desk] UI:

1. 首先，按一下 **[!UICONTROL 資料]** 標籤，並查看 **[!UICONTROL 第一方]**.
2. 向下捲動頁面，位於 **[!UICONTROL 匯入的資料]**，您會找到 **[!UICONTROL Adobe1PD磁貼]**.
3. 按一下**[!UICONTROL Adobe1PD]**方塊中，並且會列出所有啟動至的區段 [!DNL Trade Desk] 廣告商的目的地。 您也可以使用搜尋函式。
4. 來自Experience Platform的區段ID#會顯示為 [!DNL Trade Desk] UI。

## 資料使用與控管 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 處理資料時，目的地符合資料使用原則。 有關如何 [!DNL Adobe Experience Platform] 強制實施資料控管，請參閱 [資料控管概觀](/help/data-governance/home.md).
