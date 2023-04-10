---
title: （測試版）Experience Cloud對象
description: 了解如何將區段從Experience Platform分享至各種Experience Platform解決方案。
last-substantial-update: 2023-01-25T00:00:00Z
source-git-commit: a8f6bb8c3e35f4c17812ef944440210b7fe3f87b
workflow-type: tm+mt
source-wordcount: '1509'
ht-degree: 2%

---


# （測試版） [!UICONTROL Experience Cloud對象] 連接

此目的地可讓您將區段從Experience Platform共用至各種Experience Cloud解決方案，例如Audience Manager、Analytics、Advertising Cloud、Adobe Campaign、Target或Marketo。

![Experience Cloud對象目的地，在目的地目錄中反白顯示。](/help/destinations/assets/catalog/adobe/experience-cloud-audiences/experience-cloud-audiences-destination-catalog.png)

>[!IMPORTANT]
>
>* 此目的地會取代 [舊式區段共用整合](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=en#aep-segments-in-aam) 從Experience Platform到各種Experience Cloud解決方案。
>* 此目的地目前處於測試狀態。 檔案和功能可能會有所變更。


## 使用案例和優點 {#use-cases}

以協助您更清楚了解應如何及何時使用 [!UICONTROL Experience Cloud對象] 目的地，以下是Adobe Experience Platform客戶可透過此目的地解決的範例使用案例。

### 啟用Data Management Platform使用案例 {#dmp-use-cases}

在「Audience Manager」中，您可以將「Experience Platform」區段用於「資料管理平台」使用案例，例如：

* 新增 [第三方資料](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-types-collected.html?lang=en#third-party-data) 至您的區段；
* [演算法塑型](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/algorithmic-models/look-alike-modeling/understanding-models.html?lang=en);
* 對Experience Platform目的地目錄尚未支援的Cookie型目的地啟用區段。

### 精細控制匯出的區段 {#segments-control}

透過「Experience Cloud對象」目的地使用全新的自助區段共用整合，以選取要匯出至Audience Manager及其他區段。 這可讓您決定要與其他Experience Cloud解決方案共用的區段，以及要專門保留Experience Platform的區段。

舊式區段共用整合不允許精細控制應匯出至Audience Manager及其他區段。

### 與其他Experience Platform解決方案共用Experience Cloud區段 {#share-segments-with-other-solutions}

除了與Audience Manager共用區段外，「Experience Platform對象」目的地卡還可讓您與您布建的任何其他Experience Cloud解決方案共用區段，包括：

* Adobe Campaign
* Adobe Target
* Advertising Cloud
* Analytics
* Marketo

<!--

Note: briefly talk about when to share segments to these destinations using the existing destination cards and when to share using the new Experience Cloud Audiences destination. 

-->

## 先決條件 {#prerequisites}

>[!IMPORTANT]
>
> * 此目標可用於 [Adobe Real-time Customer Data Platform Prime與Ultimate](https://helpx.adobe.com/jp/legal/product-descriptions/real-time-customer-data-platform.html) 客戶。
> * 您需要Audience Manager授權才能啟用 [Data Management Platform使用案例](#dmp-use-cases) 上述。
> * 您 *不需要* 與Adobe Advertising Cloud、Adobe Target、Marketo和其他Experience Cloud解決方案共用Experience Platform區段的Audience Manager授權，如 [上一節](#share-segments-with-other-solutions).


### 針對使用舊式區段共用解決方案的客戶

如果您已透過以下連結共用區段：從Experience Platform共用至Audience Manager和其他Experience Cloud解決方案 [舊式區段共用整合](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html#aep-segments-in-aam)，您必須聯絡客戶服務或您的Adobe帳戶團隊，以停用舊版整合。 客戶服務和Adobe帳戶團隊必須提交Jira票證(請參閱範本票證AAM-52354)，才能停用整合。

解決測試版客戶取消資源調配票證的週轉時間為6個工作日或更短時間。 停用現有舊版整合後，您可以繼續 [建立連線](#connect) 透過自助服務目的地卡。

>[!IMPORTANT]
>
>從Experience Platform匯出至其他解決方案的區段，將在Jira票證解決方案與透過目的地卡片建立新連線之間的時間停止。 關閉Jira票證後，您可以透過目的地卡建立連線，將停機時間減到最少。

## 已知限制和圖說文字 {#known-limitations}

請注意「Experience Cloud對象」卡片測試版中的下列已知限制和重要圖說文字：

* [資料流監視](/help/dataflows/ui/monitor-destinations.md) 不支援。
* 連線至目的地時，您可以看到 [啟用資料流警報](#enable-alerts). 雖然可見於UI中，但 **不支援啟用警報選項** 在測試版中。
* **不支援回填**. 第一個匯出至Audience Manager或其他Experience Cloud解決方案不包含區段的歷史母體。
* 在測試版中，您可以建立 **連線至「Experience Cloud對象」目的地的單一目的地**，覆蓋屬於您Experience Platform組織的所有沙箱。
* 有 **4小時延遲** 從資料在Experience Platform中啟動到資料準備好在Audience Manager和其他Experience Cloud解決方案中使用的時間。

## 支援的身分 {#supported-identities}

匯出至的設定檔 [!UICONTROL Experience Cloud對象] 目的地會對應至下表所述的身分。 深入了解 [身分](/help/identity-service/namespaces.md).

| Target身分 | 說明 | 考量事項 |
|---|---|---|
| ECID | Experience Cloud ID | 代表ECID的命名空間。 此命名空間也可由下列別名引用：&quot;Adobe Marketing Cloud ID&quot;、&quot;Adobe Experience Cloud ID&quot;、&quot;Adobe Experience Platform ID&quot;。 請參閱下列檔案，內容如下 [ECID](/help/identity-service/ecid.md) 以取得更多資訊。 |
| GAID | Google Advertising ID | 擷取至具有Google Advertising ID(GAID)主要身分之Experience Platform的設定檔，可匯出至此目的地。 |
| IDFA | Apple ID for Advertisers | 以Apple ID for Advertisers(IDFA)主要身分擷取至Experience Platform的設定檔，可匯出至此目的地。 |
| email_lc_sha256 | 使用SHA256演算法雜湊的電子郵件地址 | 以雜湊電子郵件地址主要身分擷取至Experience Platform的設定檔，可匯出至此目的地。 |

{style="table-layout:auto"}

## 匯出類型和頻率 {#export-type-frequency}

有關目標導出類型和頻率的資訊，請參閱下表。

| 項目 | 類型 | 附註 |
|---------|----------|---------|
| 匯出類型 | **[!UICONTROL 區段匯出]** | 您正在匯出區段（對象）的所有成員，以將上方區段所列的身分識別作為輸入。 |
| 匯出頻率 | **[!UICONTROL 串流]** | 串流目的地是「一律開啟」API型連線。 一旦根據區段評估在Experience Platform中更新設定檔，連接器就會將更新傳送至下游的目的地平台。 深入了解 [串流目的地](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## 連接到目標 {#connect}

>[!IMPORTANT]
> 
>若要連線至目的地，您需要 **[!UICONTROL 管理目的地]** [存取控制權限](/help/access-control/home.md#permissions). 閱讀 [存取控制概觀](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得所需的權限。

若要連線至此目的地，請依照 [目的地設定教學課程](../../ui/connect-destination.md). 在設定目標工作流程中，填寫下列兩節所列的欄位。

>[!IMPORTANT]
> 
>在測試版中，您可以跨屬於您Experience Cloud組織的所有沙箱，建立與Experience Platform對象目的地的單一目的地連線。

### 驗證到目標 {#authenticate}

要驗證到目標，請選擇 **[!UICONTROL 設定]** 在目錄中的目的地卡片檢視中，並選取 **[!UICONTROL 連接到目標]**.

![檢視「Experience Cloud對象」目的地的「連線至目的地」選項。](/help/destinations/assets/catalog/adobe/experience-cloud-audiences/experience-cloud-audiences-authenticate-to-destination.png)

### 填寫目的地詳細資訊 {#destination-details}

若要設定目的地的詳細資訊，請填寫下方的必填和選填欄位。 UI中欄位旁的星號表示該欄位為必要欄位。

![設定新目的地畫面，顯示連線至「Experience Cloud對象」目的地的必要和選用設定。](/help/destinations/assets/catalog/adobe/experience-cloud-audiences/connect-to-destination.png)

* **[!UICONTROL 名稱]**:日後您將透過此名稱識別此目的地。
* **[!UICONTROL 說明]**:未來可協助您識別此目的地的說明。

<!--

Commenting this part out for the duration of the beta program

### Enable alerts {#enable-alerts}

You can enable alerts to receive notifications on the status of the dataflow to your destination. Select an alert from the list to subscribe to receive notifications on the status of your dataflow. For more information on alerts, see the guide on [subscribing to destinations alerts using the UI](../../ui/alerts.md).
-->

完成提供目標連接的詳細資訊後，請選擇 **[!UICONTROL 下一個]**.


## 啟用此目的地的區段 {#activate}

>[!IMPORTANT]
> 
>若要啟用資料，您需要 **[!UICONTROL 管理目的地]**, **[!UICONTROL 啟動目的地]**, **[!UICONTROL 檢視設定檔]**，和 **[!UICONTROL 檢視區段]** [存取控制權限](/help/access-control/home.md#permissions). 閱讀 [存取控制概觀](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得所需的權限。

閱讀 [啟動設定檔和區段至串流區段匯出目的地](/help/destinations/ui/activate-segment-streaming-destinations.md) 以取得啟用受眾區段至此目的地的指示。 請注意否 [對應步驟](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) 為必要項目，否 [排程步驟](/help/destinations/ui/activate-segment-streaming-destinations.md#scheduling) 可用於此目的地。

## 驗證資料匯出 {#exported-data}

若要驗證資料匯出是否成功，您可以檢查您的區段是否已成功匯出至您需要的Experience Cloud解決方案。

### 驗證Audience Manager中的資料

您的Experience Platform區段在Audience Manager中顯示為 [訊號](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=en#aep-segments-as-aam-signals), [特徵](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=en#aep-segments-as-aam-traits)，和 [區段](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=en#aep-segments-as-aam-segments). 您可以在Audience Manager中確認資料是否如上述檔案連結所述顯示。

## 資料使用與控管 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 處理資料時，目的地符合資料使用原則。 有關如何 [!DNL Adobe Experience Platform] 強制實施資料治理，讀取 [資料控管概觀](/help/data-governance/home.md).

Experience Platform中的資料控管由兩者強制執行 [資料使用量標籤](/help/data-governance/labels/reference.md) 和行銷動作。
資料使用量標籤會傳輸至應用程式，但行銷動作不會。 這表示在登陸Audience Manager後，Experience Platform的區段即可匯出至任何可用的目的地。 在Audience Manager中，您可以使用 [資料匯出控制](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/data-export-controls.html?lang=en) 來阻止區段匯出至特定目的地。

### Audience Manager中的權限管理

Audience Manager中的區段和特徵受 [基於角色的訪問控制](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/administration/administration-overview.html?lang=zh-Hant) (RBAC)。

從Experience Platform匯出的區段會指派給Audience Manager中的特定資料來源，稱為 **[!UICONTROL Experience Platform區段]**.

若要僅允許特定使用者存取區段，您可以將存取控制套用至屬於資料來源的區段。 您必須在Audience Manager中為這些區段和從Experience Platform區段建立的特徵設定新的存取控制權限。