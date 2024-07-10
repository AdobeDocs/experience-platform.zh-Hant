---
title: Experience Cloud 對象
description: 瞭解如何從Real-time Customer Data Platform將受眾分享至各種Experience Cloud應用程式。
last-substantial-update: 2023-09-28T00:00:00Z
exl-id: 2bdbcda3-2efb-4a4e-9702-4fd9991e9461
source-git-commit: c35b43654d31f0f112258e577a1bb95e72f0a971
workflow-type: tm+mt
source-wordcount: '1703'
ht-degree: 2%

---


# [!UICONTROL Experience Cloud對象] 連線

>[!AVAILABILITY]
>
> 此目的地適用於 [Adobe Real-time Customer Data Platform Prime和Ultimate](https://helpx.adobe.com/jp/legal/product-descriptions/real-time-customer-data-platform.html) 客戶。

使用此目的地可啟用從Real-Time CDP到Audience Manager和Adobe Analytics的受眾。

若要將受眾傳送至Adobe Analytics，您需要Audience Manager授權。 如需詳細資訊，請參閱 [Audience Analytics概觀](https://experienceleague.adobe.com/docs/analytics/integration/audience-analytics/mc-audiences-aam.html?lang=en).

若要將受眾傳送至其他Adobe解決方案，請使用從Real-Time CDP到的直接連線 [Adobe Target](../personalization/adobe-target-connection.md)， [Adobe Advertising](../advertising/adobe-advertising-cloud-connection.md)， [Adobe Campaign](../email-marketing/adobe-campaign.md) 和 [Marketo Engage](../adobe/marketo-engage.md).

>[!IMPORTANT]
>
>此目的地會取代 [舊版對象共用整合](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html#aep-segments-in-aam) 從Real-time Customer Data Platform到各種Experience Cloud解決方案。
> 
>如果您已透過將受眾從Real-Time CDP分享到Audience Manager和其他Experience Cloud解決方案 [舊版對象共用整合](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html#aep-segments-in-aam)，您必須先聯絡客戶服務以停用舊版整合，才能使用此目的地。

![Experience Cloud對象目的地，在目的地目錄中反白顯示。](../../assets/catalog/adobe/experience-cloud-audiences/experience-cloud-audiences-destination-catalog.png)

## 使用案例和優點 {#use-cases}

為了協助您更清楚瞭解您應如何及何時使用 [!UICONTROL Experience Cloud對象] 目的地，以下是Real-Time CDP客戶可以使用此目的地解決的範例使用案例。

### 啟用資料管理平台使用案例 {#dmp-use-cases}

在Audience Manager中，您可以針對資料管理平台使用案例使用Real-Time CDP對象，例如：

* 新增 [第三方資料](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-types-collected.html#third-party-data) 至您的區段；
* [演演算法建模](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/algorithmic-models/look-alike-modeling/understanding-models.html)；
* 將您的對象啟用至Real-Time CDP目的地目錄尚未支援的Cookie型目的地。

### 對匯出對象的精細控制 {#segments-control}

若要選取要匯出至Audience Manager及其他專案的受眾，請透過Experience Cloud受眾目的地使用新的自助受眾共用整合。  這可讓您決定要與其他Experience Cloud解決方案共用的受眾，以及只想保留在Real-Time CDP中的受眾。

舊版對象共用整合無法精確控制應將哪些對象匯出至Audience Manager及其後。

### 與Adobe Analytics共用Real-Time CDP受眾 {#share-audiences-with-analytics}

您傳送至「Experience Cloud對象」目的地的對象不會自動出現在Adobe Analytics中。

您必須先將受眾傳送至Adobe Analytics，才能執行 [實作適用於Analytics和Audience Manager的Experience Cloud Identity服務](https://experienceleague.adobe.com/docs/id-service/using/implementation/setup-aam-analytics.html?lang=en).

>[!IMPORTANT]
>
>若要透過Real-Time CDP受眾目的地將受眾從Experience Cloud傳送至Adobe Analytics，您必須擁有Audience Manager授權。

### 與其他Experience Cloud解決方案共用Real-Time CDP對象 {#share-segments-with-other-solutions}

您可以使用Real-Time CDP受眾目的地卡片，將受眾與其他Experience Cloud解決方案共用。

不過，如果您想要與這些解決方案共用受眾，Adobe強烈建議使用以下專用的目的地卡：

* [Adobe Campaign](../email-marketing/adobe-campaign.md)
* [Adobe Target](../personalization/adobe-target-connection.md)
* [Advertising Cloud](../advertising/adobe-advertising-cloud-connection.md)
* [Marketo](../adobe/marketo-engage.md)

## 先決條件 {#prerequisites}

>[!IMPORTANT]
>
> * 您需要Audience Manager授權才能啟用 [資料管理平台使用案例](#dmp-use-cases) 如上所述。
> * 您 *do* 需要Audience Manager授權，才能與Adobe Analytics共用Real-Time CDP對象。
> * 您 *不需要* 用於與Adobe Advertising Cloud、Adobe Target、Marketo和其他Audience Manager解決方案共用Real-Time CDP受眾的Experience Cloud授權，詳情請參閱 [上一節](#share-segments-with-other-solutions).

### 適用於使用舊版受眾共用解決方案的客戶

如果您已透過將受眾從Real-Time CDP分享到Audience Manager和其他Experience Cloud解決方案 [舊版對象共用整合](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html#aep-segments-in-aam)，您必須聯絡客戶服務以停用舊版整合。

解決取消布建票證的週轉時間為六個工作天或更短。 停用現有的舊版整合後，您可以繼續前往 [建立連線](#connect) 透過自助目的地卡。

>[!IMPORTANT]
>
>從Real-Time CDP匯出至您其他解決方案的對象，會在票證解析與透過目的地卡建立新連線之間的時間停止。 您可以在票證關閉後，透過目的地卡片建立連線，將停機時間降到最低。

## 已知限制和圖說文字 {#known-limitations}

使用「Experience Cloud對象」卡時，請注意下列已知限制和重要圖說文字：

* 目前支援單一Experience Cloud對象目的地。 嘗試設定第二個目的地連線會導致錯誤。
* 連線到目的地時，您可以看到以下選項： [啟用資料流警報](../../ui/alerts.md). 雖然可在UI中看見，但 **目前不支援啟用警示選項**.
* **對象回填支援**：首次匯出至Audience Manager或其他Experience Cloud解決方案時，會包含對象的歷史母體。 的使用者 [舊版對象共用整合](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html#aep-segments-in-aam) 設定此目的地的訪客預期回填差異約為6小時。
* 源自於的對象 [對象構成](../../../segmentation/ui/audience-composition.md) 不直接支援。 若要啟用此目的地的複合對象，您必須透過以下方式建立對象定義 [區段產生器](../../../segmentation/ui/segment-builder.md) 根據您的複合對象，並啟用新建立的對象。

### 啟用對象時的延遲 {#audience-activation-latency}

對象首次在Real-Time CDP中啟動的時間，和他們準備用於Audience Manager和其他Experience Cloud解決方案的時間之間，會延遲4小時。

可能需要24小時的時間，對象才能在Audience Manager中完全可用於所有使用案例。 來自Experience Cloud Audiences的對象最多可能需要48小時才會出現在Audience Manager報表中。

設定匯出至「Experience Cloud對象」目的地後的數分鐘內，即可使用Audience Manager中繼資料，例如對象名稱。

## 支援的身分 {#supported-identities}

匯出至 [!UICONTROL Experience Cloud對象] 目的地會對應至下表所述的身分。 進一步瞭解 [身分](/help/identity-service/features/namespaces.md).

| 目標身分 | 說明 | 考量事項 |
|---|---|---|
| ECID | Experience Cloud ID | 代表ECID的名稱空間。 此名稱空間也可以以下列别名表示：「Adobe Marketing Cloud ID」、「Adobe Experience Cloud ID」、「Adobe Experience Platform ID」。 請參閱以下檔案： [ECID](/help/identity-service/features/ecid.md) 以取得詳細資訊。 |
| GAID | GOOGLE ADVERTISING ID | 擷取至Real-Time CDP並具有Google Advertising ID (GAID)主要身分的設定檔可匯出至此目的地。 |
| IDFA | 廣告商適用的Apple ID | 使用廣告商Apple ID (IDFA)的主要身分識別擷取至Real-Time CDP的設定檔可匯出至此目的地。 |
| email_lc_sha256 | 使用SHA256演演算法雜湊的電子郵件地址 | 擷取至Real-Time CDP的主要身分識別為雜湊電子郵件地址的設定檔可匯出至此目的地。 |

{style="table-layout:auto"}

## 支援的對象 {#supported-audiences}

本節說明您可以將哪種型別的對象匯出至此目的地。

| 對象來源 | 支援 | 說明 |
| ---------|----------|----------|
| [!DNL Segmentation Service] | ✓ (A) | 透過Experience Platform產生的對象 [分段服務](../../../segmentation/home.md). |
| 自訂上傳 | ✓ (A) | 受眾 [已匯入](../../../segmentation/ui/audience-portal.md#import-audience) 從CSV檔案Experience Platform為。 |

{style="table-layout:auto"}

## 匯出型別和頻率 {#export-type-frequency}

請參閱下表以取得目的地匯出型別和頻率的資訊。

| 項目 | 類型 | 附註 |
|---------|----------|---------|
| 匯出類型 | **[!UICONTROL 對象匯出]** | 您正在匯出以上一節所列的身分識別中斷之對象的所有成員。 |
| 匯出頻率 | **[!UICONTROL 串流]** | 串流目的地是「一律開啟」的API型連線。 當根據對象評估在Real-Time CDP中更新設定檔時，聯結器會將更新傳送至下游的目標平台。 深入瞭解 [串流目的地](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## 連線到目標 {#connect}

>[!IMPORTANT]
> 
>若要連線到目的地，您需要 **[!UICONTROL 檢視目的地]** 和 **[!UICONTROL 管理目的地]** [存取控制許可權](/help/access-control/home.md#permissions). 閱讀 [存取控制總覽](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得必要許可權。

若要連線至此目的地，請遵循以下說明的步驟： [目的地設定教學課程](../../ui/connect-destination.md). 在設定目標工作流程中，填寫以下兩個區段中列出的欄位。

### 驗證目標 {#authenticate}

若要驗證目的地，請選取 **[!UICONTROL 設定]** 在目錄中的目的地卡片檢視中，然後選取 **[!UICONTROL 連線到目的地]**.

![「Experience Cloud對象」目的地的「連線至目的地」選項檢視。](../../assets/catalog/adobe/experience-cloud-audiences/experience-cloud-audiences-authenticate-to-destination.png)

### 填寫目標詳細資訊 {#destination-details}

若要設定目的地的詳細資訊，請填寫下方的必填和選用欄位。 UI中欄位旁的星號表示該欄位為必填欄位。

![設定新的目的地畫面，顯示連線至Experience Cloud Audiences目的地的必要和選用設定。](../..//assets/catalog/adobe/experience-cloud-audiences/connect-to-destination.png)

* **[!UICONTROL 名稱]**：您日後可辨識此目的地的名稱。
* **[!UICONTROL 說明]**：可協助您日後識別此目的地的說明。

## 啟動此目標的對象 {#activate}

>[!IMPORTANT]
> 
>若要啟用資料，您需要 **[!UICONTROL 檢視目的地]**， **[!UICONTROL 啟用目的地]**， **[!UICONTROL 檢視設定檔]**、和 **[!UICONTROL 檢視區段]** [存取控制許可權](/help/access-control/home.md#permissions). 閱讀 [存取控制總覽](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得必要許可權。

讀取 [將設定檔和受眾啟用至串流受眾匯出目標](/help/destinations/ui/activate-segment-streaming-destinations.md) 以取得啟用此目的地對象的指示。 否 [對應步驟](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) 為必要且否 [排程步驟](/help/destinations/ui/activate-segment-streaming-destinations.md#scheduling) 可用於此目的地。

## 驗證資料匯出 {#exported-data}

若要驗證資料匯出是否成功，您可以檢查受眾是否已成功匯出至您想要的Experience Cloud解決方案。

### 驗證Audience Manager中的資料

您的Real-Time CDP對象在Audience Manager中顯示為 [訊號](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html#aep-segments-as-aam-signals)， [特徵](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html#aep-segments-as-aam-traits)、和 [區段](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html#aep-segments-as-aam-segments). 您可以在Audience Manager中確認資料是否已如上述檔案連結所述顯示。

從Real-Time CDP傳送對象後15分鐘，區段名稱就會開始在Audience Manager中填入。

區段母體在從Real-Time CDP傳送後6小時內開始流入Audience Manager，並在Audience Manager中每24小時更新一次。

72小時後，Audience Manager中會顯示完整母體，而母體除非從Real-Time CDP中的目的地移除對象，否則會持續流入Audience Manager。

## 資料使用與控管 {#data-usage-governance}

全部 [!DNL Real-Time CDP] 處理您的資料時，目的地符合資料使用原則。 如需如何操作的詳細資訊 [!DNL Adobe Experience Platform] 強制執行資料控管，讀取 [資料控管概觀](/help/data-governance/home.md).

Real-Time CDP中的資料控管由兩者強制執行 [資料使用情況標籤](/help/data-governance/labels/reference.md) 和行銷動作。
資料使用標籤會傳輸到應用程式，但行銷動作不會。 這表示當受眾著陸Audience Manager後，就可以將來自Real-Time CDP的受眾匯出至任何可用的目的地。 在Audience Manager中，您可以使用 [資料匯出控制項](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/data-export-controls.html) 以封鎖將對象匯出至特定目的地的作業。

標示為的對象 [!DNL HIPAA] 行銷動作不會從Real-Time CDP傳送至Audience Manager。

### Audience Manager中的許可權管理

Audience Manager中的對象和特徵須遵循 [角色型存取控制](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/administration/administration-overview.html) (RBAC)。

從Real-Time CDP匯出的受眾會指派給Audience Manager為的特定資料來源，稱為 **[!UICONTROL Experience Platform區段]**.

若要僅允許特定使用者存取對象，請使用 [角色型存取控制](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/administration/administration-overview.html) 設定使用者對從Real-Time CDP受眾建立的受眾和特徵的存取權。
