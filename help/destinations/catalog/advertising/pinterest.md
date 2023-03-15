---
title: Pinterest客戶清單連線
description: 從您的客戶清單、造訪過您網站的人員或已在Pinterest上與您的內容互動的人員建立對象。
exl-id: e601f75f-0d40-4cd0-93ca-54d7439f1db7
source-git-commit: dd18350387aa6bdeb61612f0ccf9d8d2223a8a5d
workflow-type: tm+mt
source-wordcount: '696'
ht-degree: 3%

---

# [!DNL Pinterest Customer List] 連接

## 總覽 {#overview}

從您的客戶清單、造訪過您網站的人員或已在Pinterest上與您的內容互動的人員建立對象。

>[!IMPORTANT]
>
>這個目的地是Pinterest團隊建造的。 如有任何查詢或更新請求，請直接通過https://help.pinterest.com/en/contact聯繫。

## 先決條件 {#prerequisites}

* 使用者需要使用Pinterest帳戶進行驗證，該帳戶可存取他們要新增受眾的廣告商帳戶。 有關共用廣告商帳戶的詳細資訊，請參閱 [此處](https://help.pinterest.com/en/business/article/share-and-manage-access-to-your-ad-accounts). 具體而言，使用者需要「對象」存取層級。
* 有關客戶清單標識格式的詳細資訊 [此處](https://help.pinterest.com/en/business/article/audience-targeting).

## 支援的身分 {#supported-identities}

此 [!DNL Pinterest Customer List] 目的地支援啟用下表所述的身分。 深入了解 [身分](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=en#getting-started).

在 [對應步驟](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) 將所需身分對應至目標欄位 *pinterest_audience*. 身分識別會在資料擷取至Pinterest時加以區分和解析。

| Target身分 | 說明 | 考量事項 |
|---|---|---|
| GAID | [!DNL Google Advertising ID] | 對應 *GAID* 目標標識欄位的源標識命名空間 *pinterest_audience*. 身分識別會在資料擷取至Pinterest時加以區分和解析。 |
| IDFA | [!DNL Apple ID for Advertisers] | 對應 *IDFA* 目標標識欄位的源標識命名空間 *pinterest_audience*. 身分識別會在資料擷取至Pinterest時加以區分和解析。 |
| 電子郵件 | 電子郵件地址（清除文字或使用SHA256演算法雜湊） | Adobe Experience Platform支援純文字和SHA256雜湊電子郵件地址。 <br> 對應 *電子郵件* 或 *Email_LC_SHA256* 目標標識欄位的源標識命名空間 *pinterest_audience*. |

{style="table-layout:auto"}

## 匯出類型和頻率 {#export-type-frequency}

有關目標導出類型和頻率的資訊，請參閱下表。

| 項目 | 類型 | 附註 |
---------|----------|---------|
| 匯出類型 | **[!UICONTROL 區段匯出]** | 您正在匯出區段（對象）的所有成員，以及Pinterest客戶清單目的地中使用的識別碼（名稱、電話號碼或其他）。 |
| 匯出頻率 | **[!UICONTROL 串流]** | 串流目的地是「一律開啟」API型連線。 一旦根據區段評估在Experience Platform中更新設定檔，連接器就會將更新傳送至下游的目的地平台。 深入了解 [串流目的地](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## 使用案例 {#use-cases}

以協助您更清楚了解應如何及何時使用 [!DNL Pinterest Customer List] 目的地，以下是Adobe Experience Platform客戶可透過此目的地解決的範例使用案例。

### 使用案例#1

從您的客戶清單、造訪過您網站的人員或已在Pinterest上與您的內容互動的人員建立對象。

## 連接到目標 {#connect}

>[!IMPORTANT]
> 
>若要連線至目的地，您需要 **[!UICONTROL 管理目的地]** [存取控制權限](/help/access-control/home.md#permissions). 閱讀 [存取控制概觀](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得所需的權限。

若要連線至此目的地，請依照 [目的地設定教學課程](../../ui/connect-destination.md).

### 連線參數 {#parameters}

同時 [設定](../../ui/connect-destination.md) 此目的地時，您必須提供下列資訊：

* **[!UICONTROL 名稱]**:日後您將透過此名稱識別此目的地。
* **[!UICONTROL 說明]**:未來可協助您識別此目的地的說明。
* **[!UICONTROL 廣告商ID]**:您的Pinterest廣告商ID。

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

請參閱 [Pinterest說明中心頁面](https://help.pinterest.com/en/business/article/audience-targeting) 以取得其他資訊。
