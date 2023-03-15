---
title: Twitter自訂對象連線
description: 鎖定Twitter中現有的追隨者和客戶，並啟用Adobe Experience Platform中建置的對象，建立相關的再行銷活動
exl-id: fd244e58-cd94-4de7-81e4-c321eb673b65
source-git-commit: dd18350387aa6bdeb61612f0ccf9d8d2223a8a5d
workflow-type: tm+mt
source-wordcount: '806'
ht-degree: 2%

---

# [!DNL Twitter Custom Audiences] 連接

## 總覽 {#overview}

鎖定Twitter中現有的追隨者和客戶，並啟用Adobe Experience Platform中建置的對象，以建立相關的再行銷活動。

## 先決條件 {#prerequisites}

設定之前 [!DNL Twitter Custom Audiences] 目的地，請務必檢閱您需要符合的下列Twitter必要條件。

1. 您的 [!DNL Twitter Ads] 帳戶必須符合廣告資格。 新增 [!DNL Twitter Ads] 帳戶在建立後的前2週內不符合廣告資格。
2. 您授權在中存取的Twitter使用者帳戶 [!DNL Twitter Audience Manager] 必須具有 *[!DNL Partner Audience Manager]* 權限已啟用。

## 支援的身分 {#supported-identities}

[!DNL Twitter Custom Audiences] 支援啟用下表所述的身分。 深入了解 [身分](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=en#getting-started).

| Target身分 | 說明 | 考量事項 |
|---|---|---|
| device_id | IDFA/AdID/Android ID | Google Advertising ID(GAID)和Apple ID for Advertisers(IDFA)在Adobe Experience Platform中受支援。 請相應地在 [對應步驟](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) 目標啟動工作流程的URL區段。 |
| 電子郵件 | 使用者的電子郵件地址 | 請將純文字電子郵件地址和SHA256雜湊電子郵件地址映射到此欄位。 當來源欄位包含未雜湊屬性時，請檢查 **[!UICONTROL 套用轉換]** 選項，必須 [!DNL Platform] 啟動時自動雜湊資料。 如果您在將客戶電子郵件地址上傳至Adobe Experience Platform之前先雜湊這些電子郵件地址，請注意，這些身分識別必須使用SHA256雜湊處理，不含鹽。 |

{style="table-layout:auto"}

## 匯出類型和頻率 {#export-type-frequency}

有關目標導出類型和頻率的資訊，請參閱下表。

| 項目 | 類型 | 附註 |
---------|----------|---------|
| 匯出類型 | **[!UICONTROL 區段匯出]** | 您正在匯出區段（對象）的所有成員，以及Twitter自訂對象目的地中使用的識別碼。 |
| 匯出頻率 | **[!UICONTROL 串流]** | 串流目的地是「一律開啟」API型連線。 一旦根據區段評估在Experience Platform中更新設定檔，連接器就會將更新傳送至下游的目的地平台。 深入了解 [串流目的地](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## 使用案例 {#use-cases}

以協助您更清楚了解應如何及何時使用 [!DNL Twitter Custom Audiences] 目的地，以下是Adobe Experience Platform客戶可透過此目的地解決的範例使用案例。

### 使用案例#1

鎖定Twitter中現有的追隨者和客戶，並啟用Adobe Experience Platform中建立的對象作為 [!DNL List Custom Audiences] 在Twitter。

## 連接到目標 {#connect}

>[!IMPORTANT]
> 
>若要連線至目的地，您需要 **[!UICONTROL 管理目的地]** [存取控制權限](/help/access-control/home.md#permissions). 閱讀 [存取控制概觀](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得所需的權限。

若要連線至此目的地，請依照 [目的地設定教學課程](../../ui/connect-destination.md). 在設定目標工作流程中，填寫下列兩節所列的欄位。

### 驗證到目標 {#authenticate}

1. 尋找 [!DNL Twitter Custom Audiences] 目標目錄中的目標，然後選取 **[!UICONTROL 設定]**.
2. 選擇 **[!UICONTROL 連接到目標]**.
   ![驗證LinkedIn](/help/destinations/assets/catalog/social/twitter/authenticate-twitter-destination.png)
3. 輸入您的Twitter憑證並選取 **登入**.

### 填寫目的地詳細資訊 {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_twitter_accountid"
>title="帳戶 ID"
>abstract="您的Twitter Ads帳戶ID。 您可在Twitter Ads設定中找到。"

若要設定目的地的詳細資訊，請填寫下方的必填和選填欄位。 UI中欄位旁的星號表示該欄位為必要欄位。

* **[!UICONTROL 名稱]**:日後您將透過此名稱識別此目的地。
* **[!UICONTROL 說明]**:未來可協助您識別此目的地的說明。
* **[!UICONTROL 帳戶ID]**:您的 [!DNL Twitter Ads] 帳戶ID。 您可在 [!DNL Twitter Ads] 設定。

### 啟用警報 {#enable-alerts}

您可以啟用警報，接收有關資料流到目標狀態的通知。 從清單中選擇要訂閱的警報，以接收有關資料流狀態的通知。 如需警報的詳細資訊，請參閱 [使用UI訂閱目的地警報](../../ui/alerts.md).

完成提供目標連接的詳細資訊後，請選擇 **[!UICONTROL 下一個]**.

## 啟用此目的地的區段 {#activate}

>[!IMPORTANT]
> 
>若要啟用資料，您需要 **[!UICONTROL 管理目的地]**, **[!UICONTROL 啟動目的地]**, **[!UICONTROL 檢視設定檔]**，和 **[!UICONTROL 檢視區段]** [存取控制權限](/help/access-control/home.md#permissions). 閱讀 [存取控制概觀](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得所需的權限。

閱讀 [啟動設定檔和區段至串流區段匯出目的地](/help/destinations/ui/activate-segment-streaming-destinations.md) 以取得啟用受眾區段至此目的地的指示。

## 資料使用與控管 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 處理資料時，目的地符合資料使用原則。 有關如何 [!DNL Adobe Experience Platform] 強制實施資料控管，請參閱 [資料控管概觀](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=zh-Hant).

## 其他資源 {#additional-resources}

將受眾區段對應至Twitter時，請務必符合下列區段命名需求：

1. 提供人類看得懂的區段對應名稱。 建議您使用與用於Experience Platform區段相同的名稱。
2. 請勿使用特殊字元(+ &amp; 、 %):;@ / = ? $)。 如果您的Experience Platform區段名稱包含這些字元，請先移除這些字元，再將區段對應至Twitter目的地。

有關 [!DNL List Custom Audiences] 在Twitter, [Twitter檔案](https://business.twitter.com/en/help/campaign-setup/campaign-targeting/custom-audiences/lists.html).
