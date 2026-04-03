---
title: Adobe Advertising DSP連線
description: 瞭解如何使用多種身分型別，與Adobe Advertising Demand-Side Platform (DSP)共用已驗證和未驗證的第一方對象。
feature: Destinations
exl-id: 0ff80d38-993f-4609-bf2a-01a3e6cfe10b
source-git-commit: 58f69a78fb3c622c8741d7a1618f15509c160a5b
workflow-type: tm+mt
source-wordcount: '1469'
ht-degree: 6%

---

# Adobe Advertising DSP連線

## 概觀 {#overview}

Adobe Advertising Demand-Side Platform (DSP)目的地可讓使用者與DSP帳戶或帳戶內的特定廣告商共用已驗證和未驗證的第一方受眾。

此目的地可讓客戶與以下任何或所有ID共用第一方受眾：

* 雜湊電子郵件ID，已轉換為[!DNL LiveRamp RampID]或[!DNL Unified ID 2.0] (UID2.0)以便在DSP中鎖定目標

* Experience Cloud ID (ECID)和Adobe Advertising第三方Cookie

* 行動廣告ID (MAID)：

   * [!DNL Google]個裝置的[!DNL Android]個Advertising ID (GAID)

   * [!DNL Apple iOS]個裝置的廣告商(IDFA)識別碼

此連線取代[舊版Adobe Advertising Cloud DSP連線](adobe-advertising-cloud-dsp-connection-legacy.md)，此連線僅支援雜湊電子郵件地址。

>[!IMPORTANT]
>
>此頁面是由Adobe Advertising [!DNL DSP]團隊建立。 若有任何查詢或更新要求，請直接透過`adcloud_support@adobe.com`聯絡Advertising支援。

## 使用案例 {#use-cases}

此目的地可讓廣告商在具有Cookie和不具有Cookie的情況下，跨瀏覽器觸及其受眾。

廣告商可以選擇使用已驗證的第一方識別碼（例如[!DNL RampID]和[!DNL UID2.0]）或作為未驗證的ID （例如Cookie和MAID）共用區段。

## 先決條件 {#prerequisites}

* 針對[!DNL RampID activation]、[!DNL DSP]帳戶層級和行銷活動層級設定，啟用與[!DNL LiveRamp RampID]的對象共用，這會將客戶資料轉譯為[!DNL RampIDs]以建立可定位的區段。 您的Adobe帳戶團隊將執行此設定。 [!DNL RampID]可透過[!DNL DSP]與[!DNL LiveRamp]之間的合作關係使用，而且您不需要自己的[!DNL LiveRamp]成員資格即可使用。

* 對象ID：

   * 針對[!DNL RampID]和[!DNL UID2.0]，設定檔必須包含雜湊電子郵件ID。

   * 針對Cookie，請使用[!DNL Web SDK]資料串流或[!DNL Experience Cloud ID Service]設定Cookie同步處理序。 請參閱下方的[設定ID同步以共用Cookie](#cookie-sync)。

   * 對於具有MAID的設定檔：

      * 對於每個GAID，在IdentityMap資料行中包含值`GAID`。

      * 對於每個IDFA，在IdentityMap資料行中包含值`IDFA`。

* Experience Platform帳戶的Experience Cloud組織ID。 您可以在Adobe [!DNL Real-Time Customer Data Platform] ([!DNL Real-Time CDP])使用者設定檔頁面上找到您的識別碼。

* DSP[[!DNL Real-Time CDP] 中用於接收促銷活動啟用對象的](https://experienceleague.adobe.com/en/docs/advertising/dsp/audiences/sources/source-manage)來源。 您的Adobe帳戶團隊將使用您的Experience Cloud組織ID建立來源。

* 在[!DNL DSP][[!DNL Real-Time CDP] 中建立 [!DNL DSP]來源時產生的](https://experienceleague.adobe.com/en/docs/advertising/dsp/audiences/sources/source-manage)帳戶或廣告商的來源金鑰。 您的[!DNL DSP]帳戶團隊將會與您共用此金鑰。 您將在Experience Platform中使用它來建立與Advertising DSP目的地的目的地連線，如下所述。

### 設定ID同步以共用Cookie {#cookie-sync}

ID同步是共用協力廠商Cookie的先決條件。 使用[!DNL Web SDK]資料串流或[!DNL Experience Cloud ID Service]設定Cookie同步處理序。 如需第三方Cookie識別處理的詳細內容，請參閱依賴第三方Cookie整合的[Advertising目的地](/help/destinations/how-destinations-work/identity-handling.md#third-party-cookie-destinations)。

**啟用協力廠商ID與[!DNL Web SDK]**&#x200B;同步

如果您使用[!DNL Experience Platform Web SDK]，請在進階設定中設定[!UICONTROL Third Party ID Sync]選項，以在您的資料流上啟用協力廠商ID同步。 如需指示，請參閱資料串流檔案中的[設定進階選項](/help/datastreams/configure.md#advanced-options)。

**啟用協力廠商ID與[!DNL Experience Cloud ID Service]**&#x200B;同步

如果您使用[!DNL Experience Platform]標籤搭配[!DNL Experience Cloud ID Service]，請使用[Experience Cloud ID服務擴充功能](/help/tags/extensions/client/id-service/overview.md)設定協力廠商ID同步處理。 這可讓您在從[!DNL Real-Time CDP]啟用對象時，可以使用特定ECID的相符Adobe Advertising Cookie。

## 支援的身分 {#supported-identities}

Adobe Advertising DSP目的地支援下表所述的身分啟用。 深入瞭解[身分](/help/identity-service/features/namespaces.md)。

| 目標身分 | 說明 | 考量事項 |
| --------------- | ----------- | -------------- |
| `email_lc_sha256` | 使用SHA256演演算法雜湊的電子郵件地址 | Experience Platform支援純文字和SHA256雜湊電子郵件地址。 當您的來源欄位包含未雜湊的屬性時，請核取&#x200B;**[!UICONTROL Apply transformation]**&#x200B;選項，讓Experience Platform在啟用時自動雜湊資料。 |
| `ECID` | Experience Cloud的第一方Cookie | 建立Cookie型區段時需要。 |
| `adcloud` | 適用於Adobe Advertising的第三方Cookie | 建立Cookie型區段時需要。 |
| `GAID` | [!DNL Android]裝置識別碼 | 定位[!DNL Android]裝置時需要。 |
| `IDFA` | [!DNL iOS]裝置識別碼 | 定位[!DNL iOS]裝置時需要。 |

{style="table-layout:auto"}

## 支援的對象 {#supported-audiences}

本節說明您可以將哪些型別的對象匯出至此目的地。

| 對象來源 | 支援 | 說明 |
|---------|----------|----------|
| [!DNL Segmentation Service] | 是 | 透過Experience Platform [細分服務](../../../segmentation/home.md)產生的對象。 |
| 所有其他受眾來源 | 是 | 此類別包含透過[!DNL Segmentation Service]產生的對象以外的所有對象來源。 閱讀[各種對象來源](/help/segmentation/ui/audience-portal.md#customize)。 部分範例包括： <ul><li> 自訂上傳對象[從CSV檔案匯入](../../../segmentation/ui/audience-portal.md#import-audience)至Experience Platform，</li><li> 相似受眾， </li><li> 同盟對象， </li><li> 其他Experience Platform應用程式中產生的對象，例如[!DNL Adobe Journey Optimizer]、 </li><li> 及更多內容。 </li></ul> |

{style="table-layout:auto"}

依受眾資料型別支援的受眾：

| 對象資料型別 | 支援 | 說明 | 使用案例 |
| -------------------- | --------- | ----------- | --------- |
| [人員對象](/help/segmentation/types/people-audiences.md) | 是 | 根據客戶設定檔，可讓您針對行銷活動的特定人群進行定位。 | 經常購買者、購物車放棄者 |
| [帳戶對象](/help/segmentation/types/account-audiences.md) | 無 | 針對帳戶型行銷策略，鎖定特定組織內的個人。 | B2B行銷 |
| [潛在客戶對象](/help/segmentation/types/prospect-audiences.md) | 無 | 將目標定位為尚未成為客戶但與目標受眾具有相同特性的個人。 | 使用第三方資料進行勘探 |
| [資料集匯出](/help/catalog/datasets/overview.md) | 無 | 儲存在[!DNL Adobe Experience Platform]資料湖中的結構化資料集合。 | 報告、資料科學工作流程 |

{style="table-layout:auto"}

## 匯出型別和頻率 {#export-type-frequency}

請參閱下表以取得目的地匯出型別和頻率的資訊。

| 項目 | 類型 | 附註 |
| ---- | ---- | ----- |
| 匯出類型 | **[!UICONTROL Audience export]** | 您正在匯出具有所選識別碼之對象的所有成員。 |
| 匯出頻率 | **[!UICONTROL Streaming]** | 串流目的地是「一律開啟」的API型連線。 當根據對象評估在Experience Platform中更新設定檔時，聯結器會將更新傳送至下游的目標平台。 深入瞭解[串流目的地](/help/destinations/destination-types.md#streaming-destinations)。 |

{style="table-layout:auto"}

## 連線到目標 {#connect}

>[!IMPORTANT]
>
>若要連線到目的地，您需要Experience Platform的&#x200B;**[!UICONTROL View Destinations]**&#x200B;和&#x200B;**[!UICONTROL Manage Destinations]** [存取控制許可權](/help/access-control/home.md#permissions)。 閱讀[存取控制總覽](/help/access-control/ui/overview.md)或連絡您的產品管理員以取得必要的許可權。

若要連線到目的地，請依照指示使用Experience Platform使用者介面[建立目的地連線](/help/destinations/ui/connect-destination.md)。 在目標設定工作流程中，填寫以下子區段中列出的欄位。

### 驗證目標 {#authenticate}

若要連線到目的地，請在[!UICONTROL Connection type]區段中提供下列引數，然後選取&#x200B;**[!UICONTROL Connect to destination]**：

* **[!UICONTROL Account or Advertiser Key]**：在DSP使用者介面[!UICONTROL Source Key]中建立[[!DNL Real-Time CDP] 來源時，會產生此](https://experienceleague.adobe.com/en/docs/advertising/dsp/audiences/sources/source-manage)。 您的Adobe客戶團隊會在建立來源後，與您共用此金鑰。

![顯示[帳戶]或[廣告商金鑰]欄位之[連線型別]區段的熒幕擷圖。](/help/destinations/assets/catalog/advertising/adobe-advertising-cloud-connection/authenticate-destination.png)

### 填寫目標詳細資訊 {#destination-details}

若要設定目的地的詳細資訊，請填寫下方的必填和選用欄位。 UI中欄位旁的星號表示該欄位為必填欄位。

* **[!UICONTROL Name]**：您日後可辨識此目的地的名稱。
* **[!UICONTROL Description]**：可協助您日後識別此目的地的說明。

![顯示「名稱」和「描述」輸入之目的地詳細資料欄位的熒幕擷圖。](/help/destinations/assets/catalog/advertising/adobe-advertising-cloud-connection/destination-details.png)

### 啟用警示 {#enable-alerts}

您可以啟用警報以接收有關傳送到您目的地的資料流狀態的通知。 從清單中選取警報以訂閱接收有關資料流狀態的通知。 如需警示的詳細資訊，請參閱[使用UI訂閱目的地警示](../../ui/alerts.md)的指南。

當您完成提供目的地連線的詳細資訊時，請選取&#x200B;**[!UICONTROL Next]**。

## 啟動此目標的對象 {#activate}

>[!CONTEXTUALHELP]
>id="platform_destinations_required_mappings_adcloud_dsp"
>title="預先設定的對應集"
>abstract="我們已為您預先設定這兩個對應集：ECID 和 [!DNL adcloud] Cookie。當您將資料啟用至 Adobe Advertising DSP 時，符合已啟用客群資格的輪廓必須至少有一個與其輪廓相關聯的 ECID 身分識別，才能成功匯出至目標。"
>additional-url="https://experienceleague.adobe.com/zh-hant/docs/experience-platform/destinations/catalog/advertising/adobe-advertising-dsp-connection#preconfigured-mappings" text="深入了解預先設定的對應"

>[!IMPORTANT]
>
>* 若要啟用資料，您需要&#x200B;**[!UICONTROL View Destinations]**、**[!UICONTROL Activate Destinations]**、**[!UICONTROL View Profiles]**&#x200B;和&#x200B;**[!UICONTROL View Segments]** [存取控制許可權](/help/access-control/home.md#permissions)。 閱讀[存取控制總覽](/help/access-control/ui/overview.md)或連絡您的產品管理員以取得必要的許可權。
>* 若要匯出身分，您需要&#x200B;**[!UICONTROL View Identity Graph]** [存取控制許可權](/help/access-control/home.md#permissions)。<br> ![選取工作流程中反白的身分名稱空間，以啟用目的地的對象。](/help/destinations/assets/overview/export-identities-to-destination.png "選取工作流程中反白顯示的身分名稱空間，以啟用目的地的對象。"){width="100" zoomable="yes"}

閱讀[將設定檔和對象啟用至串流對象匯出目的地](/help/destinations/ui/activate-segment-streaming-destinations.md)，以瞭解啟用此目的地對象的指示。

### 對應屬性和身分 {#map}

已部分預先設定此目的地的身分對應。 檢閱下列預先設定的對應，並新增您要包含的任何選擇性身分識別。

### 預先設定的對應 {#preconfigured-mappings}

下列身分對應已預先設定&#x200B;**，並在對象啟用工作流程期間自動填入**：

* **`ECID`** (Experience Cloud ID)
* **`adcloud`** （Adobe Advertising第三方Cookie）

![身分對應區段的熒幕擷圖顯示Cookie識別碼、雜湊電子郵件、IDFA和GAID選項。](/help/destinations/assets/catalog/advertising/adobe-advertising-cloud-connection/identity-mapping.png)

這些對應會呈現灰色，而且是唯讀的。 您不需要在此步驟中設定任何專案。 您可以選擇新增下列對應：

* **`email_lc_sha256`** （雜湊電子郵件）
* **IDFA** （[!DNL Apple iOS]裝置識別碼）
* **GAID** （[!DNL Android]裝置識別碼）

選取&#x200B;**[!UICONTROL Next]**&#x200B;以繼續。

>[!IMPORTANT]
>
>需要&#x200B;**ECID才能成功匯出以Cookie為基礎的檔案。不含ECID的**&#x200B;個設定檔將不會包含在Cookie型區段中。 針對使用[!DNL RampID]或[!DNL UID2.0]的已驗證對象區段，設定檔必須包含雜湊電子郵件ID。

如需指示，請參閱[對應屬性和身分](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping)。

## 驗證資料匯出 {#exported-data}

若要確認對象資料已與Adobe Advertising共用，請檢查下列專案：

* [!DNL Real-Time CDP]目的地中的資料流程成功。

* 在DSP中，當您從&#x200B;**[!UICONTROL Audiences]** > **[!UICONTROL All Audiences]**&#x200B;或從位置設定的&#x200B;**[!UICONTROL Audience Targeting]**&#x200B;區段建立或編輯對象時，可以使用對象。 對象應會顯示在[!UICONTROL Adobe Segments]資料夾下的[!UICONTROL Real-Time CDP]標籤中。

![DSP Audiences介面的熒幕擷圖顯示[!DNL Real-Time CDP]資料夾，「Adobe區段」索引標籤下列出已匯入的對象區段。](/help/destinations/assets/catalog/advertising/adobe-advertising-cloud-connection/segments-in-dsp.png)

## 資料使用與控管 {#data-usage-governance}

處理您的資料時，所有[!DNL Adobe Experience Platform]目的地都符合資料使用原則。 如需[!DNL Adobe Experience Platform]如何強制資料控管的詳細資訊，請參閱[資料控管概觀](/help/data-governance/home.md)。
