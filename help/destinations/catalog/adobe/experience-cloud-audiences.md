---
title: (Beta)Experience Cloud對象
description: 瞭解如何將Experience Platform的受眾分享至各種Experience Platform解決方案。
last-substantial-update: 2023-01-25T00:00:00Z
exl-id: 2bdbcda3-2efb-4a4e-9702-4fd9991e9461
source-git-commit: 72225ac673ed921b5857a14070660134949e7e3e
workflow-type: tm+mt
source-wordcount: '1611'
ht-degree: 2%

---

# (Beta) [!UICONTROL Experience Cloud對象] 連線

此目的地可讓您將Experience Platform的受眾分享至各種Experience Cloud解決方案，例如Audience Manager、Analytics、Advertising Cloud、Adobe Campaign、Target或Marketo。

![Experience Cloud對象目的地，在目的地目錄中反白顯示。](/help/destinations/assets/catalog/adobe/experience-cloud-audiences/experience-cloud-audiences-destination-catalog.png)

>[!IMPORTANT]
>
>* 此目的地會取代 [舊版對象共用整合](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=en#aep-segments-in-aam) 從Experience Platform到各種Experience Cloud解決方案。
>* 此目的地目前處於Beta版。 檔案和功能可能會有所變更。

## 使用案例和優點 {#use-cases}

為了協助您更清楚瞭解您應如何及何時使用 [!UICONTROL Experience Cloud對象] 目的地，以下是Adobe Experience Platform客戶可以使用此目的地解決的範例使用案例。

### 啟用資料管理平台使用案例 {#dmp-use-cases}

在Audience Manager中，您可以針對Data Management Platform使用案例使用Experience Platform對象，例如：

* 新增 [第三方資料](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-types-collected.html?lang=en#third-party-data) 至您的區段；
* [演算法塑型](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/algorithmic-models/look-alike-modeling/understanding-models.html?lang=en);
* 將您的對象啟用至Experience Platform目的地目錄中尚未支援的Cookie型目的地。

### 對匯出對象的精細控制 {#segments-control}

透過Experience Cloud Audiences目的地使用新的自助受眾共用整合，以選取要匯出至Audience Manager及其他地方的受眾。 這可讓您決定要與其他Experience Cloud解決方案共用的受眾，以及要專門保留在Experience Platform中的受眾。

舊版對象共用整合無法精確控制應將哪些對象匯出至Audience Manager及其後。

### 與其他Experience Platform解決方案共用Experience Cloud對象 {#share-segments-with-other-solutions}

除了與Audience Manager共用受眾之外，Experience Platform受眾目的地卡可讓您與您布建的任何其他Experience Cloud解決方案共用受眾，包括：

* Adobe Campaign
* Adobe Target
* Advertising Cloud
* Analytics
* Marketo

<!--

Note: briefly talk about when to share audiences to these destinations using the existing destination cards and when to share using the new Experience Cloud Audiences destination. 

-->

## 先決條件 {#prerequisites}

>[!IMPORTANT]
>
> * 此目的地適用於 [Adobe Real-time Customer Data Platform Prime和Ultimate](https://helpx.adobe.com/jp/legal/product-descriptions/real-time-customer-data-platform.html) 客戶。
> * 您需要Audience Manager授權才能啟用 [資料管理平台使用案例](#dmp-use-cases) 如上所述。
> * 您 *不需要* Audience Manager授權可與Adobe Advertising Cloud、Adobe Target、Marketo和其他Experience Platform解決方案共用Experience Cloud對象，詳情請參閱 [上一節](#share-segments-with-other-solutions).

### 適用於使用舊版受眾共用解決方案的客戶

如果您已透過將受眾從Experience Platform分享到Audience Manager和其他Experience Cloud解決方案 [舊版對象共用整合](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html#aep-segments-in-aam)，您必須聯絡客戶服務或您的Adobe客戶團隊，才能停用舊版整合。 客戶服務及Adobe帳戶團隊必須檔案Jira票證(請參閱範本票證PLAT-160986)才能停用整合。

針對Beta版客戶解決取消布建票證的週轉時間為六個工作日或以下。 停用現有的舊版整合後，您可以繼續前往 [建立連線](#connect) 透過自助目的地卡。

>[!IMPORTANT]
>
>從Experience Platform到您其他解決方案的對象匯出作業，將在Jira票證解析與透過目的地卡建立新連線之間的時間停止。 您可以在Jira票證關閉後立即透過目的地卡建立連線，藉此將停機時間降到最低。

## 已知限制和圖說文字 {#known-limitations}

請注意Experience Cloud Audiences卡片Beta版中的下列已知限制和重要圖說：

* [資料流監視](/help/dataflows/ui/monitor-destinations.md) 不受支援。
* 連線到目的地時，您可以看到以下選項： [啟用資料流警報](#enable-alerts). 雖然可在UI中看見，但 **不支援啟用警示選項** （在測試版中）。
* **不支援回填**. 首次匯出至Audience Manager或其他Experience Cloud解決方案時，不包含對象的歷史母體。
* 在Beta版中，您可以建立 **與「Experience Cloud對象」目的地的單一目的地連線**，針對屬於您Experience Platform組織的所有沙箱。

### 啟用對象時的延遲 {#audience-activation-latency}

對象首次在Experience Platform中啟動的時間，與他們準備用於特定使用案例的Audience Manager和其他Experience Cloud解決方案的時間之間，會延遲四小時。

可能需要24小時的時間，對象才會在Audience Manager中完全可用於所有使用案例，而Experience Cloud對象的對象最多可能需要48小時的時間，才會出現在Audience Manager報表中。

設定匯出至「Experience Cloud對象」目的地後的數分鐘內，即可使用Audience Manager中繼資料，例如對象名稱。

## 支援的身分 {#supported-identities}

匯出至 [!UICONTROL Experience Cloud對象] 目的地會對應至下表所述的身分。 進一步瞭解 [身分](/help/identity-service/namespaces.md).

| 目標身分 | 說明 | 考量事項 |
|---|---|---|
| ECID | Experience Cloud ID | 代表ECID的名稱空間。 此名稱空間也可以以下列别名表示：「Adobe Marketing Cloud ID」、「Adobe Experience Cloud ID」、「Adobe Experience Platform ID」。 請參閱以下檔案： [ECID](/help/identity-service/ecid.md) 以取得詳細資訊。 |
| GAID | Google廣告ID | 擷取至Experience Platform且主要身分為Google Advertising ID (GAID)的設定檔可匯出至此目的地。 |
| IDFA | 廣告商適用的Apple ID | 廣告商(IDFA)之主要身分識別為Apple ID的設定檔擷取至Experience Platform，可匯出至此目的地。 |
| email_lc_sha256 | 使用SHA256演演算法雜湊的電子郵件地址 | 以雜湊電子郵件地址為主要身分擷取至Experience Platform的設定檔，可匯出至此目的地。 |

{style="table-layout:auto"}

## 支援的對象 {#supported-audiences}

本節說明您可以將哪些型別的對象匯出至此目的地。

| 對象來源 | 支援 | 說明 |
---------|----------|----------|
| [!DNL Segmentation Service] | ✓ (A) | 透過Experience Platform產生的對象 [分段服務](../../../segmentation/home.md). |
| 自訂上傳 | ✓ | 受眾 [已匯入](../../../segmentation/ui/overview.md#import-audience) 從CSV檔案Experience Platform為。 |

{style="table-layout:auto"}

## 匯出型別和頻率 {#export-type-frequency}

請參閱下表以取得目的地匯出型別和頻率的資訊。

| 項目 | 類型 | 附註 |
|---------|----------|---------|
| 匯出型別 | **[!UICONTROL 對象匯出]** | 您正在匯出以上一節所列的身分識別中斷之對象的所有成員。 |
| 匯出頻率 | **[!UICONTROL 串流]** | 串流目的地是「一律開啟」的API型連線。 一旦根據對象評估在Experience Platform中更新了設定檔，聯結器就會將更新傳送至下游的目的地平台。 深入瞭解 [串流目的地](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## 連線到目的地 {#connect}

>[!IMPORTANT]
> 
>若要連線到目的地，您需要 **[!UICONTROL 管理目的地]** [存取控制許可權](/help/access-control/home.md#permissions). 閱讀 [存取控制總覽](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得必要許可權。

若要連線至此目的地，請遵循以下說明的步驟： [目的地設定教學課程](../../ui/connect-destination.md). 在設定目標工作流程中，填寫以下兩個區段中列出的欄位。

>[!IMPORTANT]
> 
>在測試版中，您可以在屬於您的Experience Platform組織的所有沙箱中，建立與Experience Cloud對象目的地的單一目的地連線。

### 驗證到目的地 {#authenticate}

若要驗證目的地，請選取 **[!UICONTROL 設定]** 在目錄中的目的地卡片檢視中，然後選取 **[!UICONTROL 連線到目的地]**.

![「Experience Cloud對象」目的地的「連線至目的地」選項檢視。](/help/destinations/assets/catalog/adobe/experience-cloud-audiences/experience-cloud-audiences-authenticate-to-destination.png)

### 填寫目的地詳細資料 {#destination-details}

若要設定目的地的詳細資訊，請填寫下方的必填和選用欄位。 UI中欄位旁的星號表示該欄位為必填欄位。

![設定新的目的地畫面，顯示連線至Experience Cloud Audiences目的地的必要和選用設定。](/help/destinations/assets/catalog/adobe/experience-cloud-audiences/connect-to-destination.png)

* **[!UICONTROL 名稱]**：您日後可辨識此目的地的名稱。
* **[!UICONTROL 說明]**：可協助您日後識別此目的地的說明。

<!--

Commenting this part out for the duration of the beta program

### Enable alerts {#enable-alerts}

You can enable alerts to receive notifications on the status of the dataflow to your destination. Select an alert from the list to subscribe to receive notifications on the status of your dataflow. For more information on alerts, see the guide on [subscribing to destinations alerts using the UI](../../ui/alerts.md).
-->

當您完成提供目的地連線的詳細資訊時，請選取「 」 **[!UICONTROL 下一個]**.


## 啟用此目的地的對象 {#activate}

>[!IMPORTANT]
> 
>若要啟用資料，您需要 **[!UICONTROL 管理目的地]**， **[!UICONTROL 啟用目的地]**， **[!UICONTROL 檢視設定檔]**、和 **[!UICONTROL 檢視區段]** [存取控制許可權](/help/access-control/home.md#permissions). 閱讀 [存取控制總覽](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得必要許可權。

讀取 [將設定檔和受眾啟用至串流受眾匯出目標](/help/destinations/ui/activate-segment-streaming-destinations.md) 以取得啟用此目的地對象的指示。 請注意，否 [對應步驟](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) 為必要且否 [排程步驟](/help/destinations/ui/activate-segment-streaming-destinations.md#scheduling) 可用於此目的地。

## 驗證資料匯出 {#exported-data}

若要驗證資料匯出是否成功，您可以檢查受眾是否已成功匯出至您想要的Experience Cloud解決方案。

### 驗證Audience Manager中的資料

您的Experience Platform對象在Audience Manager中顯示為 [訊號](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=en#aep-segments-as-aam-signals)， [特徵](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=en#aep-segments-as-aam-traits)、和 [區段](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=en#aep-segments-as-aam-segments). 您可以在Audience Manager中確認資料是否已如上述檔案連結所述顯示。

## 資料使用與控管 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 處理您的資料時，目的地符合資料使用原則。 如需如何操作的詳細資訊 [!DNL Adobe Experience Platform] 強制執行資料控管，讀取 [資料控管概觀](/help/data-governance/home.md).

Experience Platform中的資料控管由兩者強制執行 [資料使用情況標籤](/help/data-governance/labels/reference.md) 和行銷動作。
資料使用標籤將會傳輸至應用程式，但行銷動作不會。 這表示當受眾著陸Audience Manager後，Experience Platform的受眾可以匯出至任何可用的目的地。 在Audience Manager中，您可以使用 [資料匯出控制項](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/data-export-controls.html?lang=en) 以封鎖將對象匯出至特定目的地的作業。

### Audience Manager中的許可權管理

Audience Manager中的對象和特徵須遵循 [角色型存取控制](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/administration/administration-overview.html?lang=zh-Hant) (RBAC)。

從Experience Platform匯出的對象會指派給Audience Manager中名為的特定資料來源 **[!UICONTROL Experience Platform區段]**.

若要僅允許特定使用者存取對象，您可以將存取控制套用至屬於資料來源的對象。 您必須在Audience Manager為這些對象和從Experience Platform區段建立的特徵，設定新的存取控制許可權。
