---
title: Adobe Advertising Cloud DSP連線
description: Adobe Advertising Cloud DSP是Adobe Real-time Customer Data Platform的整合式目的地，可讓您與核准的廣告商和使用者共用已驗證的第一方受眾，以啟用行銷活動。
exl-id: 11ff7797-a9c6-4334-b843-ae9df9a48e54
source-git-commit: ba39f62cd77acedb7bfc0081dbb5f59906c9b287
workflow-type: tm+mt
source-wordcount: '1055'
ht-degree: 2%

---

# Adobe Advertising Cloud DSP連線

## 概觀 {#overview}

Adobe Advertising Cloud [!DNL Demand-Side Platform] (DSP)目的地可讓您與已核准的廣告商和使用者共用已驗證的第一方對象，以便透過DSP啟用行銷活動。 若要深入瞭解Real-Time CDP與DSP的整合，請參閱[關於從受眾來源啟用已驗證受眾](https://experienceleague.adobe.com/docs/advertising-cloud/dsp/audiences/sources/source-about.html?lang=zh-Hant)。

>[!IMPORTANT]
>
>此頁面是由DSP團隊建立。 若有任何查詢或更新要求，請直接透過`adcloud_support@adobe.com`聯絡Advertising Cloud支援。

## 使用案例 {#use-cases}

為協助您更清楚瞭解如何使用Advertising Cloud DSP目的地，以下是Adobe Experience Platform客戶可使用此目的地解決的範例使用案例。

### 品牌廣告使用案例

線上零售商想要透過顯示行銷活動重新鎖定高價值客戶，而不使用Cookie進行目標定位。 該零售商分享其高價值客戶(從其Adobe Real-time Customer Data Platform (Real-Time CDP)帳戶至其DSP帳戶)的雜湊電子郵件ID對象。 然後DSP會透過DSP與LiveRamp之間的合作關係，將雜湊電子郵件ID轉換為已驗證的[!DNL RampIDs]。 產生的[!DNL RampIDs]可用於顯示促銷活動，以鎖定對象。

### 機構使用案例

一家擁有DSP帳戶的媒體代理公司，代表其客戶（旅館業最頂尖的品牌）執行重新目標定位行銷活動。 該品牌想要以新的促銷優惠重新鎖定去年所有訪客。 品牌在[!DNL Real-Time CDP]中代管所有來賓資訊。 品牌可以共用一個對象，該對象包含從其[!DNL Real-Time CDP]帳戶到媒體代理商的DSP帳戶的訪客雜湊電子郵件ID，以便透過媒體促銷活動重新鎖定訪客。

## 先決條件 {#prerequisites}

* DSP帳戶層級和促銷活動層級設定可啟用與[!DNL LiveRamp RampID]的對象共用，這會將客戶資料轉譯為[!DNL RampIDs]以建立可定位的區段。 您的DSP帳戶團隊將執行此設定。 [!DNL RampID]可透過DSP與[!DNL LiveRamp]之間的合作關係使用，而且您不需要自己的[!DNL LiveRamp]成員資格即可使用。
* Experience Platform帳戶的Experience Cloud組織ID。 您可以在[!DNL Real-Time CDP]使用者設定檔頁面上找到您的識別碼。
* DSP[&#128279;](https://experienceleague.adobe.com/docs/advertising-cloud/dsp/audiences/sources/source-create.html?lang=zh-Hant)中用於接收促銷活動啟用對象的[!DNL Real-Time CDP] 來源。 您的DSP帳戶團隊將使用您的Experience Cloud組織ID建立來源。
* DSP帳戶或廣告商的來源金鑰，是在DSP[&#128279;](https://experienceleague.adobe.com/docs/advertising-cloud/dsp/audiences/sources/source-create.html?lang=zh-Hant)中建立[!DNL Real-Time CDP] 來源時產生的。 您的DSP帳戶團隊將會與您共用此金鑰。 您將在Experience Platform中使用它來建立與Advertising Cloud DSP目的地的目的地連線，如下文[所述](#authenticate)。
* 由電子郵件或雜湊電子郵件組成的客戶資料。

## 支援的身分 {#supported-identities}

Adobe Advertising Cloud DSP目的地支援下表所述的身分啟用。 深入瞭解[身分](/help/identity-service/features/namespaces.md)。

| 目標身分 | 說明 | 考量事項 |
|---|---|---|
| email_lc_sha256 | 使用SHA256演演算法雜湊的電子郵件地址 | Experience Platform支援純文字和SHA256雜湊電子郵件地址。 當您的來源欄位包含未雜湊的屬性時，請核取&#x200B;**[!UICONTROL 套用轉換]**&#x200B;選項，讓Experience Platform在啟動時自動雜湊資料。 |

{style="table-layout:auto"}

## 匯出型別和頻率 {#export-type-frequency}

請參閱下表以取得目的地匯出型別和頻率的資訊。

| 項目 | 類型 | 附註 |
---------|----------|---------|
| 匯出類型 | **[!UICONTROL 對象匯出]** | 您正在匯出某個對象的所有成員，而這些成員具有Advertising Cloud DSP目的地所使用的識別碼（電子郵件或雜湊電子郵件）。 |
| 匯出頻率 | **[!UICONTROL 串流]** | 串流目的地是「一律開啟」的API型連線。 當根據對象評估在Experience Platform中更新設定檔時，聯結器會將更新傳送至下游的目標平台。 深入瞭解[串流目的地](/help/destinations/destination-types.md#streaming-destinations)。 |

{style="table-layout:auto"}

## 連線到目標 {#connect}

>[!IMPORTANT]
> 
>若要連線到目的地，您需要&#x200B;**[!UICONTROL 檢視目的地]**&#x200B;和&#x200B;**[!UICONTROL 管理目的地]** [Experience Platform存取控制許可權](/help/access-control/home.md#permissions)。 閱讀[存取控制總覽](/help/access-control/ui/overview.md)或連絡您的產品管理員以取得必要的許可權。

若要連線到目的地，請依照指示使用Experience Platform使用者介面[建立目的地連線](/help/destinations/ui/connect-destination.md)。 在目標設定工作流程中，填寫以下兩個區段中列出的欄位。

### 驗證目標 {#authenticate}

若要連線到目的地，請在[!UICONTROL 連線型別]區段中提供下列引數，然後選取&#x200B;**[!UICONTROL 連線到目的地]**：

* **[!UICONTROL 帳戶或廣告商金鑰]**：在DSP使用者介面[&#128279;](https://experienceleague.adobe.com/docs/advertising-cloud/dsp/audiences/sources/source-create.html?lang=zh-Hant)中建立[!DNL Real-Time CDP] 來源時，會產生此[!UICONTROL Source金鑰]。 您的DSP帳戶團隊會在建立來源後，與您共用此金鑰。

![連線型別欄位](/help/destinations/assets/catalog/advertising/adobe-advertising-cloud-connection/authenticate-destination.png)

### 填寫目標詳細資訊 {#destination-details}

若要設定目的地的詳細資訊，請填寫下方的必填和選用欄位。 UI中欄位旁的星號表示該欄位為必填欄位。

* **[!UICONTROL 名稱]**：您日後可辨識此目的地的名稱。
* **[!UICONTROL 描述]**：可協助您日後識別此目的地的描述。

![目的地詳細資料欄位](/help/destinations/assets/catalog/advertising/adobe-advertising-cloud-connection/destination-details.png)

### 啟用警示 {#enable-alerts}

您可以啟用警報以接收有關傳送到您目的地的資料流狀態的通知。 從清單中選取警報以訂閱接收有關資料流狀態的通知。 如需警示的詳細資訊，請參閱[使用UI訂閱目的地警示](../../ui/alerts.md)的指南。

當您完成提供目的地連線的詳細資訊後，請選取&#x200B;**[!UICONTROL 下一步]**。

## 啟動此目標的對象 {#activate}

>[!IMPORTANT]
> 
>* 若要啟用資料，您需要&#x200B;**[!UICONTROL 檢視目的地]**、**[!UICONTROL 啟用目的地]**、**[!UICONTROL 檢視設定檔]**&#x200B;和&#x200B;**[!UICONTROL 檢視區段]** [存取控制許可權](/help/access-control/home.md#permissions)。 閱讀[存取控制總覽](/help/access-control/ui/overview.md)或連絡您的產品管理員以取得必要的許可權。
>* 若要匯出&#x200B;*身分*，您需要&#x200B;**[!UICONTROL 檢視身分圖表]** [存取控制許可權](/help/access-control/home.md#permissions)。<br> ![選取工作流程中反白的身分名稱空間，以啟用目的地的對象。](/help/destinations/assets/overview/export-identities-to-destination.png "選取工作流程中反白顯示的身分名稱空間，以啟用目的地的對象。"){width="100" zoomable="yes"}

閱讀[將設定檔和對象啟用至串流對象匯出目的地](/help/destinations/ui/activate-segment-streaming-destinations.md)，以瞭解啟用此目的地對象的指示。

## 驗證資料匯出 {#exported-data}

若要確認資料對象已與Advertising Cloud共用，請檢查下列專案：

* [!DNL Real-Time CDP]目的地中的資料流程成功。

* 在DSP中，當您從[!UICONTROL 對象] > [!UICONTROL 所有對象]或從位置設定的[!UICONTROL 對象鎖定目標]區段建立或編輯對象時，可以使用對象。 對象應會顯示在[!UICONTROL Real-Time CDP]資料夾下的[!UICONTROL Adobe區段]標籤中。

DSP對象設定中的![Real-Time CDP對象](/help/destinations/assets/catalog/advertising/adobe-advertising-cloud-connection/segments-in-dsp.png)

## 資料使用與控管 {#data-usage-governance}

處理您的資料時，所有[!DNL Adobe Experience Platform]目的地都符合資料使用原則。 如需[!DNL Adobe Experience Platform]如何強制資料控管的詳細資訊，請參閱[資料控管概觀](/help/data-governance/home.md)。
