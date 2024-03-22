---
title: Amazon Ads
description: Amazon Ads提供一系列選項，協助您為註冊賣家、廠商、圖書供應商、Kindle Direct Publishing (KDP)作者、應用程式開發人員和/或代理商達成廣告目標。 Amazon Ads與Adobe Experience Platform的整合提供與Amazon Ads產品(包括Amazon DSP (ADSP))的鑰匙式整合。 使用Adobe Experience Platform中的Amazon Ads目的地，使用者能在Amazon DSP上定義用於鎖定和啟用的廣告商對象。
last-substantial-update: 2024-02-20T00:00:00Z
exl-id: 724f3d32-65e0-4612-a882-33333e07c5af
source-git-commit: 8e34e5488ab80cd1f3c8086bf7c16d3f22527540
workflow-type: tm+mt
source-wordcount: '1646'
ht-degree: 2%

---

# （測試版） Amazon Ads連線 {#amazon-ads}

## 概觀 {#overview}

[!DNL Amazon Ads] 提供一系列選項，協助您為註冊銷售商、廠商、圖書廠商、Kindle Direct Publishing (KDP)作者、應用程式開發人員和/或代理商達成廣告目標。

此 [!DNL Amazon Ads] 與Adobe Experience Platform的整合提供以下專案的統整整合： [!DNL Amazon Ads] 產品，包括Amazon DSP (ADSP)和AmazonMarketing Cloud(AMC)。

使用 [!DNL Amazon Ads] 目的地：在Adobe Experience Platform中，使用者能定義廣告商對象，以在Amazon DSP上鎖定和啟用。  此外，使用者可將其資料上傳至 [!DNL Amazon Marketing Cloud] 若要依對象瞭解成效，廣告商提供的維度、Amazon區段中的成員資格，或AMC中可用的其他訊號。 將廣告商受眾上傳至AMC後，使用者可以使用 [!DNL Amazon Marketing Cloud] 若要使用中的Amazon訊號來修改、增強或附加至對象成員 [!DNL Amazon Marketing Cloud].

AMC將Amazon擁有和運營的屬性所產生的獨特訊號整合在一起，橫跨多種媒體，包括顯示器、視訊、串流電視、音訊和贊助廣告。 使用者可以輕鬆地從Adobe Experience Platform將已組織的區段傳送至AMC，以增強學習，例如受眾的市場內群組、生活方式同類群組及品牌參與模式。 然後可以使用增強的區段來最佳化Amazon DSP中的媒體啟用。

>[!IMPORTANT]
>
>此目的地聯結器和檔案頁面是由 *[!DNL Amazon Ads]* 團隊。 此產品目前為測試版，功能可能會有所變更。 如有任何查詢或更新要求，請直接聯絡他們： *`amc-support@amazon.com`.*

## 使用案例 {#use-cases}

為了協助您更清楚瞭解您應如何及何時使用 *[!DNL Amazon Ads]* 目的地，以下是Adobe Experience Platform客戶可以使用此目的地解決的範例使用案例。

### 啟用與定位 {#activation-and-targeting}

此與Amazon DSP的整合可讓 [!DNL Amazon Ads] 廣告商從Adobe Experience Platform將廣告商CDP受眾傳遞至Amazon的DSP，以建立廣告商受眾以用於廣告鎖定目標。 您可以在Amazon DSP中選取正面目標定位和負面目標定位（隱藏）的對象。

### Analytics與Measurement {#analytics-and-measurement}

此項與的整合 [!DNL Amazon Marketing Cloud] (AMC)允許 [!DNL Amazon Ads] 廣告商從Adobe Experience Platform表單傳遞CDP區段至AMC。 廣告商隨後可透過以下方式加入CDP輸入 [!DNL Amazon Ads] 會以符合隱私權要求的格式，針對媒體影響、受眾區段和客戶歷程等主題發出訊號並進行自訂分析。 例如，廣告商可能會上傳其現有客戶的清單，以瞭解彙總的廣告促銷活動成效，或Amazon上轉換事件的彙總統計資料，例如檢視產品詳細資料頁面、將產品新增至購物車或購買產品。

### Advertising最佳化

此項與的整合 [!DNL Amazon Marketing Cloud] (AMC)可讓廣告商上傳自己的客戶清單，並使用 [!DNL Amazon Marketing Cloud] SQL，在Amazon DSP中建立可啟動的受眾以進行目標定位之前，會定期對受眾執行重疊分析、隱藏、新增或最佳化。

## 先決條件 {#prerequisites}

若要使用 [!DNL Amazon Ads] 與Adobe Experience Platform的連線中，使用者必須首先能存取Amazon DSP廣告商帳戶或 [!DNL Amazon Marketing Cloud] 執行個體。 若要布建這些執行個體，請造訪以下頁面： [!DNL Amazon Ads] 網站：

* [開始使用Amazon DSP](https://advertising.amazon.com/solutions/products/amazon-dsp)
* [開始使用AmazonMarketing Cloud](https://advertising.amazon.com/solutions/products/amazon-marketing-cloud)

## 支援的身分 {#supported-identities}

此 *[!DNL Amazon Ads]* 連線支援下表所述的身分啟用。 進一步瞭解 [身分](/help/identity-service//features/namespaces.md). 有關支援的身分的更多詳細資訊 [!DNL Amazon Ads]，造訪 [Amazon DSP支援中心](https://advertising.amazon.com/dsp/help/ss/en/audiences#GA6BC9BW52YFXBNE).

| 目標身分 | 說明 | 考量事項 |
|---|---|---|
| phone_sha256 | 使用SHA256演演算法雜湊的電話號碼 | Adobe Experience Platform同時支援純文字和SHA256雜湊電話號碼。 當來源欄位包含未雜湊屬性時，請核取 **[!UICONTROL 套用轉換]** 選項，擁有 [!DNL Platform] 啟動時自動雜湊資料。 |
| email_lc_sha256 | 使用SHA256演演算法雜湊的電子郵件地址 | Adobe Experience Platform同時支援純文字和SHA256雜湊電子郵件地址。 當來源欄位包含未雜湊屬性時，請核取 **[!UICONTROL 套用轉換]** 選項，擁有 [!DNL Platform] 啟動時自動雜湊資料。 |

{style="table-layout:auto"}

## 匯出型別和頻率 {#export-type-frequency}

請參閱下表以取得目的地匯出型別和頻率的資訊。

| 項目 | 類型 | 附註 |
---------|----------|---------|
| 匯出型別 | **[!UICONTROL 對象匯出]** | 您正在匯出某個對象的所有成員，而這些成員中都有用於的識別碼（名稱、電話號碼或其他）。 *[!DNL Amazon Ads]* 目的地。 |
| 匯出頻率 | **[!UICONTROL 串流]** | 串流目的地是「一律開啟」的API型連線。 一旦根據對象評估在Experience Platform中更新了設定檔，聯結器就會將更新傳送至下游的目的地平台。 深入瞭解 [串流目的地](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## 連線到目標 {#connect}

>[!IMPORTANT]
> 
>若要連線到目的地，您需要 **[!UICONTROL 檢視目的地]** 和 **[!UICONTROL 管理目的地]** [存取控制許可權](/help/access-control/home.md#permissions). 閱讀 [存取控制總覽](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得必要許可權。

若要連線至此目的地，請遵循以下說明的步驟： [目的地設定教學課程](../../ui/connect-destination.md). 在設定目標工作流程中，填寫以下兩個區段中列出的欄位。

### 驗證目標 {#authenticate}

若要向目的地進行驗證，請填寫必填欄位並選取 **[!UICONTROL 連線到目的地]**.

您被帶到 [!DNL Amazon Ads] 連線介面，您可在其中先選取要連線的廣告商帳戶。 連線後，系統會將您重新導向回Adobe Experience Platform，並顯示您選取的廣告商帳戶ID，其中包含新的連線。 在目的地設定畫面上選取適當的廣告商帳戶以繼續。

* **[!UICONTROL 持有人權杖]**：填寫持有人權杖以對目的地進行驗證。

### 填寫目標詳細資訊 {#destination-details}

若要設定目的地的詳細資訊，請填寫下方的必填和選用欄位。 UI中欄位旁的星號表示該欄位為必填欄位。

* **[!UICONTROL 名稱]**：您日後可辨識此目的地的名稱。
* **[!UICONTROL 說明]**：可協助您日後識別此目的地的說明。
* **[!UICONTROL Amazon Ads連線]**：選取目標的ID [!DNL Amazon Ads] 用於目的地的帳戶。

>[!NOTE]
>
>儲存目的地設定後，您將無法變更 [!DNL Amazon Ads] 廣告商ID，即使您透過Amazon帳戶重新驗證亦然。 使用不同的 [!DNL Amazon Ads] 廣告商ID，您必須建立新的目的地連線。

* **[!UICONTROL 廣告商地區]**：選取您的廣告商託管所在的適當區域。 如需各個區域支援之市場環境的詳細資訊，請造訪 [Amazon Ads檔案](https://advertising.amazon.com/API/docs/en-us/info/api-overview#api-endpoints).



![設定新目的地](../../assets/catalog/advertising/amazon_ads_image_4.png)

### 啟用警示 {#enable-alerts}

您可以啟用警報以接收有關傳送到您目的地的資料流狀態的通知。 從清單中選取警報以訂閱接收有關資料流狀態的通知。 如需警示的詳細資訊，請參閱以下指南： [使用UI訂閱目的地警報](../../ui/alerts.md).

當您完成提供目的地連線的詳細資訊時，請選取「 」 **[!UICONTROL 下一個]**.

## 啟動此目標的對象 {#activate}

>[!IMPORTANT]
> 
>* 若要啟用資料，您需要 **[!UICONTROL 檢視目的地]**， **[!UICONTROL 啟用目的地]**， **[!UICONTROL 檢視設定檔]**、和 **[!UICONTROL 檢視區段]** [存取控制許可權](/help/access-control/home.md#permissions). 閱讀 [存取控制總覽](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得必要許可權。
>* 要匯出 *身分*，您需要 **[!UICONTROL 檢視身分圖表]** [存取控制許可權](/help/access-control/home.md#permissions). <br> ![選取工作流程中反白顯示的身分名稱空間，以將對象啟用至目的地。](/help/destinations/assets/overview/export-identities-to-destination.png "選取工作流程中反白顯示的身分名稱空間，以將對象啟用至目的地。"){width="100" zoomable="yes"}

讀取 [將設定檔和受眾啟用至串流受眾匯出目標](/help/destinations/ui/activate-segment-streaming-destinations.md) 以取得啟用此目的地對象的指示。

### 對應屬性和身分 {#map}

此 [!DNL Amazon Ads] 連線支援雜湊電子郵件地址和雜湊電話號碼，以進行身分比對。 底下熒幕擷圖提供相容於 [!DNL Amazon Ads] 連線：

![Adobe至Amazon Ads對應](../../assets/catalog/advertising/amazon_ads_image_2.png)

* 若要對應雜湊電子郵件地址，請選取 `Email_LC_SHA256` 身分名稱空間作為來源欄位。
* 若要對應雜湊電話號碼，請選取 `Phone_SHA256` 身分名稱空間作為來源欄位。
* 若要對應未雜湊的電子郵件地址或電話號碼，請選取對應的身分名稱空間作為來源欄位，然後核取 `Apply Transformation` 啟用時讓Platform雜湊身分的選項。

您只能在的目的地設定中選取一次指定的目標欄位 [!DNL Amazon Ads] 聯結器。  例如，如果您提交商務電子郵件，您就無法在同一目的地設定中對應個人電子郵件。

強烈建議您儘量對應可用欄位。 如果只有一個來源屬性可用，您可以對應單一欄位。 此 [!DNL Amazon Ads] 目的地會將所有對應的欄位用於對應目的，如果提供更多欄位，可提供較高的匹配率。 如需關於接受之識別碼的詳細資訊，請造訪 [Amazon Ads雜湊對象說明頁面](https://advertising.amazon.com/dsp/help/ss/en/audiences#GA6BC9BW52YFXBNE).

## 匯出的資料/驗證資料匯出 {#exported-data}

上傳對象後，您可使用以下步驟驗證對象是否已正確建立及上傳：

**適用於Amazon DSP**

導覽至 **[!UICONTROL 廣告商ID]** > **[!UICONTROL 受眾]** > **[!UICONTROL 廣告商受眾]**. 如果您的對象已成功建立並符合對象成員的最低數量，您將會看到「 」狀態 `Active`. 您可以在Amazon DSP使用者介面右側的預測觸及面板中，找到有關您對象人數和觸及率的其他詳細資訊。

![Amazon DSP對象建立驗證](../../assets/catalog/advertising/amazon_ads_image_3.png)

**的[!DNL Amazon Marketing Cloud]**

在左側結構描述瀏覽器中，在下方找到您的對象 **[!UICONTROL 廣告商已上傳]** > **[!UICONTROL aep_audiences]**. 然後，您可以在AMC SQL編輯器中使用下列子句查詢您的對象：

`select count(user_id) from aep_audiences where audienceId = '1234567'`

![AmazonMarketing Cloud對象建立驗證](../../assets/catalog/advertising/amazon_ads_image_5.png)


## 資料使用與控管 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 處理您的資料時，目的地符合資料使用原則。 如需如何操作的詳細資訊 [!DNL Adobe Experience Platform] 強制執行資料控管，讀取 [資料控管概觀](/help/data-governance/home.md).

## 其他資源 {#additional-resources}

如需其他說明檔案，請造訪下列專案 [!DNL Amazon Ads] 說明資源：

* [Amazon DSP說明中心](https://www.amazon.com/ap/signin?openid.pape.max_auth_age=28800&amp;openid.return_to=https%3A%2F%2Fadvertising.amazon.com%2Fdsp%2Fhelp%2Fss%2Fen%2Faudiences&amp;openid.identity=http%3A%2F%2Fspecs.openid.net%2Fauth%2F2.0%2Fidentifier_select&amp;openid.assoc_handle=amzn_bt_desktop_us&amp;openid.mode=checkid_setup&amp;openid.claimed_id=http%3A%2F%2Fspecs.openid.net%2Fauth%2F2.0%2Fidentifier_select&amp;openid.ns=http%3A%2F%2Fspecs.openid.net%2Fauth%2F2.0)

## Changelog {#changelog}

本節擷取此目的地聯結器的功能和重要檔案更新。

+++ 檢視變更記錄檔

| 發行月份 | 更新型別 | 說明 |
|---|---|---|
| 2024 年 3 月 | 功能和檔案更新 | 新增匯出對象以用於以下專案的選項： [!DNL Amazon Marketing Cloud] (AMC)。 |
| 2023 年 5 月 | 功能和檔案更新 | <ul><li>在中新增對廣告商區域選取的支援 [目的地連線工作流程](#destination-details).</li><li>更新說明檔案，反映新增廣告商地區選擇。 如需選取正確廣告商地區的詳細資訊，請參閱 [Amazon檔案](https://advertising.amazon.com/API/docs/en-us/info/api-overview#api-endpoints).</li></ul> |
| 2023 年 3 月 | 首次發行 | 已發佈初始目的地版本和檔案。 |

{style="table-layout:auto"}

+++
