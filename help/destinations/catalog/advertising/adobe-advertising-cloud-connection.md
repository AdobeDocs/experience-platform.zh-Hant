---
title: Adobe Advertising Cloud DSP連線
description: Adobe Advertising Cloud DSP是Adobe Real-time Customer Data Platform的整合目的地，可讓您與核准的廣告商和使用者共用已驗證的第一方區段，以便進行促銷活動啟用。
exl-id: 11ff7797-a9c6-4334-b843-ae9df9a48e54
source-git-commit: e67b3a6f9f57a3971a5bfa755db3b1043bebc96b
workflow-type: tm+mt
source-wordcount: '1055'
ht-degree: 1%

---

# Adobe Advertising Cloud DSP連線

## 總覽 {#overview}

Adobe Advertising Cloud [!DNL Demand-Side Platform] (DSP)目的地可讓您與已核准的廣告商和使用者共用已驗證的第一方區段，以便透過DSP啟動促銷活動。 若要進一步了解Real-Time CDP與DSP的整合，請參閱 [關於從受眾來源啟用已驗證的區段](https://experienceleague.adobe.com/docs/advertising-cloud/dsp/audiences/sources/source-about.html).

>[!IMPORTANT]
>
>此頁面由DSP團隊建立。 如有任何查詢或更新請求，請直接聯絡Advertising Cloud支援人員，網址為 `adcloud_support@adobe.com`.

## 使用案例 {#use-cases}

為協助您更清楚了解應如何及何時使用Advertising Cloud DSP目的地，以下是Adobe Experience Platform客戶可透過此目的地解決的範例使用案例。

### 品牌廣告使用案例

線上零售商想要透過顯示促銷活動重新鎖定其高價值客戶，而不要使用Cookie進行定位。 零售商會與其DSP帳戶共用一個區段，其中包含其Adobe Real-time Customer Data Platform(Real-Time CDP)帳戶之高價值客戶的雜湊電子郵件ID。 DSP接著會將雜湊電子郵件ID轉換為已驗證 [!DNL RampIDs] 通過DSP和LiveRamp的合作關係。 產生的 [!DNL RampIDs] 可用於顯示促銷活動以鎖定對象。

### 代理使用案例

擁有DSP帳戶的媒體代理代表其客戶（酒店業的頂尖品牌）執行重新定位的促銷活動。 該品牌希望以新的促銷優惠來重新定位去年的所有客人。 品牌會主控 [!DNL Real-Time CDP]. 品牌可以共用區段，該區段包含來自其之訪客的雜湊電子郵件ID [!DNL Real-Time CDP] 帳戶至媒體代理的DSP帳戶，以透過媒體行銷活動重新定位訪客。

## 先決條件 {#prerequisites}

* DSP帳戶層級和促銷活動層級的設定，以啟用區段共用，與 [!DNL LiveRamp RampID]，會將客戶資料轉譯為 [!DNL RampIDs] 來建立可定位的區段。 您的DSP帳戶團隊將執行此設定。 [!DNL RampID] 可透過DSP與的合作關係取得 [!DNL LiveRamp]，而且您不需要自己的 [!DNL LiveRamp] 會籍來使用。
* Experience Cloud帳戶的Experience Platform組織ID。 您可以在 [!DNL Real-Time CDP] 使用者設定檔頁面。
* A [[!DNL Real-Time CDP] DSP中的來源](https://experienceleague.adobe.com/docs/advertising-cloud/dsp/audiences/sources/source-create.html) 接收促銷活動啟用的區段。 您的DSP帳戶團隊將使用您的Experience Cloud組織ID建立來源。
* DSP帳戶或廣告商的來源金鑰，會在 [[!DNL Real-Time CDP] 來源於DSP中建立](https://experienceleague.adobe.com/docs/advertising-cloud/dsp/audiences/sources/source-create.html). 您的DSP帳戶團隊會與您共用此金鑰。 您將在Experience Platform內使用它來建立與Advertising Cloud DSP目的地的目的地連線，如 [說明如下](#authenticate).
* 由電子郵件或雜湊電子郵件組成的客戶資料。

## 支援的身分 {#supported-identities}

Adobe Advertising Cloud DSP目的地支援啟用下表所述的身分。 深入了解 [身分](/help/identity-service/namespaces.md).

| Target身分 | 說明 | 考量事項 |
|---|---|---|
| email_lc_sha256 | 使用SHA256演算法雜湊的電子郵件地址 | Experience Platform支援純文字和SHA256雜湊電子郵件地址。 當來源欄位包含未雜湊屬性時，請檢查 **[!UICONTROL 套用轉換]** 選項，讓Experience Platform在啟動時自動雜湊資料。 |

{style=&quot;table-layout:auto&quot;}

## 匯出類型和頻率 {#export-type-frequency}

有關目標導出類型和頻率的資訊，請參閱下表。

| 項目 | 類型 | 附註 |
---------|----------|---------|
| 匯出類型 | **[!UICONTROL 區段匯出]** | 您正在匯出區段（對象）的所有成員，以及Advertising Cloud DSP目的地中使用的識別碼（電子郵件或雜湊電子郵件）。 |
| 匯出頻率 | **[!UICONTROL 串流]** | 串流目的地是「一律開啟」API型連線。 當設定檔根據區段評估以Experience Platform更新時，連接器會將更新下游傳送至目的地平台。 深入了解 [串流目的地](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## 連接到目標 {#connect}

>[!IMPORTANT]
> 
>若要連線至目的地，您需要 **[!UICONTROL 管理目的地]** [存取控制權限](/help/access-control/home.md#permissions) Experience Platform。 閱讀 [存取控制概觀](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得所需的權限。

要連接到目標，請按照以下說明操作： [建立目標連線](/help/destinations/ui/connect-destination.md) 使用Experience Platform使用者介面。 在目標設定工作流程中，填寫下列兩節中列出的欄位。

### 驗證到目標 {#authenticate}

若要連線至目的地，請在 [!UICONTROL 連線類型] ，然後選取 **[!UICONTROL 連接到目標]**.:

* **[!UICONTROL 帳戶或廣告商金鑰]**:此 [!UICONTROL 源密鑰] 當 [[!DNL Real-Time CDP] 來源是在DSP使用者介面中建立](https://experienceleague.adobe.com/docs/advertising-cloud/dsp/audiences/sources/source-create.html). 您的DSP帳戶團隊在建立來源後，會與您共用此金鑰。

![連接類型欄位](/help/destinations/assets/catalog/advertising/adobe-advertising-cloud-connection/authenticate-destination.png)

### 填寫目的地詳細資訊 {#destination-details}

若要設定目的地的詳細資訊，請填寫下方的必填和選填欄位。 UI中欄位旁的星號表示該欄位為必要欄位。

* **[!UICONTROL 名稱]**:日後您將透過此名稱識別此目的地。
* **[!UICONTROL 說明]**:未來可協助您識別此目的地的說明。

![目標詳細資訊欄位](/help/destinations/assets/catalog/advertising/adobe-advertising-cloud-connection/destination-details.png)

### 啟用警報 {#enable-alerts}

您可以啟用警報，接收有關資料流到目標狀態的通知。 從清單中選擇要訂閱的警報，以接收有關資料流狀態的通知。 如需警報的詳細資訊，請參閱 [使用UI訂閱目的地警報](../../ui/alerts.md).

完成提供目標連接的詳細資訊後，請選擇 **[!UICONTROL 下一個]**.

## 啟用此目的地的區段 {#activate}

>[!IMPORTANT]
> 
>若要啟用資料，您需要 **[!UICONTROL 管理目的地]**, **[!UICONTROL 啟動目的地]**, **[!UICONTROL 檢視設定檔]**，和 **[!UICONTROL 檢視區段]** [存取控制權限](/help/access-control/home.md#permissions). 閱讀 [存取控制概觀](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得所需的權限。

閱讀 [啟動設定檔和區段至串流區段匯出目的地](/help/destinations/ui/activate-segment-streaming-destinations.md) 以取得啟用受眾區段至此目的地的指示。

## 驗證資料匯出 {#exported-data}

若要確認資料區段已與Advertising Cloud共用，請檢查下列項目：

* 您 [!DNL Real-Time CDP] 目標成功。

* 在DSP中，當您從 [!UICONTROL 對象] > [!UICONTROL 所有對象] 或從 [!UICONTROL 對象鎖定] 版位設定區段。 區段應會顯示在 [!UICONTROL Adobe區段] 標籤 [!UICONTROL Real-Time CDP] 檔案夾。

![Real-Time CDP對象設定中的DSP區段](/help/destinations/assets/catalog/advertising/adobe-advertising-cloud-connection/segments-in-dsp.png)

## 資料使用與控管 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 處理資料時，目的地符合資料使用原則。 如需詳細資訊，請參閱 [!DNL Adobe Experience Platform] 強制實施資料控管，請參閱 [資料控管概觀](/help/data-governance/home.md).
