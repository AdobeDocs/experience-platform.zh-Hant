---
title: Amazon Ads
description: Amazon Ads提供一系列選項，可協助您為註冊銷售商、廠商、書籍廠商、Kindle Direct Publishing(KDP)作者、應用程式開發人員和/或代理商達成廣告目標。 Amazon Ads與Adobe Experience Platform的整合提供Amazon Ads產品(包括Amazon DSP(ADSP))的轉換金鑰整合。 使用Adobe Experience Platform中的Amazon Ads目的地，使用者可以定義廣告商對象，以便在Amazon DSP上鎖定和啟用。
last-substantial-update: 2023-03-29T00:00:00Z
source-git-commit: 732e6d3d53d983f3390941f4694d2c542d882004
workflow-type: tm+mt
source-wordcount: '1277'
ht-degree: 1%

---


# (Beta)Amazon Ads連線 {#amazon-ads}

## 總覽 {#overview}

Amazon Ads提供一系列選項，可協助您為註冊銷售商、廠商、書籍廠商、Kindle Direct Publishing(KDP)作者、應用程式開發人員和/或代理商達成廣告目標。

Amazon Ads與Adobe Experience Platform的整合提供Amazon Ads產品(包括Amazon DSP(ADSP))的轉換金鑰整合。 使用Adobe Experience Platform中的Amazon Ads目的地，使用者可以定義廣告商對象，以便在Amazon DSP上鎖定和啟用。

此連線支援在下列Amazon Marketplace中建立受眾： `US`, `CA`, `MX`, `BR`.

>[!IMPORTANT]
>
>本檔案頁面由 *Amazon Ads* 團隊。 這目前是測試版產品，功能可能會有所變更。 如有任何查詢或更新請求，請直接與他們聯繫，地址為 *`amc-support@amazon.com`.*

## 使用案例 {#use-cases}

以協助您更清楚了解應如何及何時使用 *Amazon Ads* 目的地，以下是Adobe Experience Platform客戶可透過此目的地解決的範例使用案例。

### 啟動與鎖定 {#activation-and-targeting}

此與Amazon DSP的整合可讓Amazon Ads廣告商將廣告商CDP區段從Adobe Experience Platform傳遞至Amazon DSP，以建立廣告商對象以用於廣告鎖定目標。 可在Amazon DSP中選取對象，以進行正面鎖定目標，以及負面鎖定目標（隱藏）。 此外，廣告商可使用透過AmazonMarketing Cloud產生的訊號，最佳化其廣告商對象，以便將對象變更與Amazon DSP同步。

## 先決條件 {#prerequisites}

若要與Adobe Experience Platform使用Amazon Ads連線，使用者必須先擁有Amazon DSP廣告商帳戶的存取權。  若要布建這些例項，請造訪Amazon Ads網站上的下列頁面：

* [開始使用Amazon DSP](https://advertising.amazon.com/solutions/products/amazon-dsp?ref_=a20m_us_hnav_p_dsp_adtech)

## 支援的身分 {#supported-identities}

此 *Amazon Ads* connection支援啟用下表中所述的身分。 深入了解 [身分](/help/identity-service/namespaces.md). 如需Amazon Ads支援身分的詳細資訊，請造訪 [Amazon DSP支援中心](https://advertising.amazon.com/dsp/help/ss/en/audiences#GA6BC9BW52YFXBNE).

| Target身分 | 說明 | 考量事項 |
|---|---|---|
| phone_sha256 | 使用SHA256演算法雜湊的電話號碼 | Adobe Experience Platform支援純文字和SHA256雜湊電話號碼。 當來源欄位包含未雜湊屬性時，請檢查 **[!UICONTROL 套用轉換]** 選項，必須 [!DNL Platform] 啟動時自動雜湊資料。 |
| email_lc_sha256 | 使用SHA256演算法雜湊的電子郵件地址 | Adobe Experience Platform支援純文字和SHA256雜湊電子郵件地址。 當來源欄位包含未雜湊屬性時，請檢查 **[!UICONTROL 套用轉換]** 選項，必須 [!DNL Platform] 啟動時自動雜湊資料。 |

{style="table-layout:auto"}

## 匯出類型和頻率 {#export-type-frequency}

有關目標導出類型和頻率的資訊，請參閱下表。

| 項目 | 類型 | 附註 |
---------|----------|---------|
| 匯出類型 | **[!UICONTROL 區段匯出]** | 您正在匯出區段（對象）的所有成員，其中包含 *Amazon Ads* 目的地。 |
| 匯出頻率 | **[!UICONTROL 串流]** | 串流目的地是「一律開啟」API型連線。 一旦根據區段評估在Experience Platform中更新設定檔，連接器就會將更新傳送至下游的目的地平台。 深入了解 [串流目的地](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## 連接到目標 {#connect}

>[!IMPORTANT]
> 
>若要連線至目的地，您需要 **[!UICONTROL 管理目的地]** [存取控制權限](/help/access-control/home.md#permissions). 閱讀 [存取控制概觀](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得所需的權限。

若要連線至此目的地，請依照 [目的地設定教學課程](../../ui/connect-destination.md). 在設定目標工作流程中，填寫下列兩節所列的欄位。

### 驗證到目標 {#authenticate}

若要驗證目的地，請填寫必填欄位並選取 **[!UICONTROL 連接到目標]**.

系統會將您帶往Amazon Ads連線介面，您會先在其中選取您要連線的廣告商帳戶。  連線時，系統會將您重新導向回Adobe Experience Platform，其中包含您所選廣告商帳戶的ID。 在目標設定畫面上選取適當的廣告商帳戶以繼續。

* **[!UICONTROL 承載令牌]**:填入承載權杖，以驗證目的地。

### 填寫目的地詳細資訊 {#destination-details}

若要設定目的地的詳細資訊，請填寫下方的必填和選填欄位。 UI中欄位旁的星號表示該欄位為必要欄位。

* **[!UICONTROL 名稱]**:日後您將透過此名稱識別此目的地。
* **[!UICONTROL 說明]**:未來可協助您識別此目的地的說明。
* **[!UICONTROL Amazon Ads廣告商ID]**:選取用於目的地的目標Amazon Ads帳戶ID。

注意：選取此Amazon Ads廣告商ID後，您需要建立新目的地才能變更此ID。 如果您重新驗證OAuth憑證並選取新的廣告商ID，您的變更將不會套用。

![配置新目標](../../assets/catalog/advertising/amazon_ads_image_1.png)

### 啟用警報 {#enable-alerts}

您可以啟用警報，接收有關資料流到目標狀態的通知。 從清單中選擇要訂閱的警報，以接收有關資料流狀態的通知。 如需警報的詳細資訊，請參閱 [使用UI訂閱目的地警報](../../ui/alerts.md).

完成提供目標連接的詳細資訊後，請選擇 **[!UICONTROL 下一個]**.

## 啟用此目的地的區段 {#activate}

>[!IMPORTANT]
> 
>若要啟用資料，您需要 **[!UICONTROL 管理目的地]**, **[!UICONTROL 啟動目的地]**, **[!UICONTROL 檢視設定檔]**，和 **[!UICONTROL 檢視區段]** [存取控制權限](/help/access-control/home.md#permissions). 閱讀 [存取控制概觀](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得所需的權限。

閱讀 [啟動設定檔和區段至串流區段匯出目的地](/help/destinations/ui/activate-segment-streaming-destinations.md) 以取得啟用受眾區段至此目的地的指示。

### 對應屬性和身分 {#map}

Amazon Ads連線支援雜湊電子郵件地址和雜湊電話號碼，以用於身分比對用途。  下方螢幕擷取畫面提供與Amazon Ads連線相容的相符範例：

![Adobe至Amazon Ads的對應](../../assets/catalog/advertising/amazon_ads_image_2.png)

* 若要對應雜湊電子郵件地址，請選取 `Email_LC_SHA256` 身分命名空間作為來源欄位。
* 若要對應雜湊電話號碼，請選取 `Phone_SHA256` 身分命名空間作為來源欄位。
* 若要對應未雜湊的電子郵件地址或電話號碼，請選取對應的身分命名空間作為來源欄位，然後檢查 `Apply Transformation` 啟用時讓Platform雜湊身分識別的選項。

強烈建議您對應可用的欄位數。 如果只有一個來源屬性可用，則可以映射單個欄位。  Amazon廣告目的地會利用所有對應欄位進行對應，如果提供更多欄位，則可獲得更高的匹配率。 如需接受識別碼的詳細資訊，請造訪 [Amazon Ads雜湊對象說明頁面](https://advertising.amazon.com/dsp/help/ss/en/audiences#GA6BC9BW52YFXBNE).

## 匯出的資料/驗證資料匯出 {#exported-data}

上傳對象後，您可以使用下列步驟來驗證對象是否已建立並正確上傳：

**適用於Amazon DSP**

導覽至您的廣告商ID → Audiences →廣告商受眾。 如果對象已成功建立且符合對象成員的最少數量，您會看到狀態為 `Active`.  您可在Amazon DSP使用者介面右側的「預測觸及」面板中，找到有關您的對象大小和觸及的其他詳細資料。

![Amazon DSP受眾建立驗證](../../assets/catalog/advertising/amazon_ads_image_3.png)

## 資料使用與控管 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 處理資料時，目的地符合資料使用原則。 有關如何 [!DNL Adobe Experience Platform] 強制實施資料治理，讀取 [資料控管概觀](/help/data-governance/home.md).

## 其他資源 {#additional-resources}

如需其他說明檔案，請造訪下列Amazon Ads說明資源：

* [Amazon DSP說明中心](https://advertising.amazon.com/dsp/help/ss/en/audiences#/)
