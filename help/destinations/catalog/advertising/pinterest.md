---
title: pinterest客戶清單連線
description: 從您的客戶清單、造訪過您網站的人，或已在Pinterest上與您的內容互動的人中建立對象。
exl-id: e601f75f-0d40-4cd0-93ca-54d7439f1db7
source-git-commit: 661ef040398a9e2ef8dd9cebdf7bd27d4268636b
workflow-type: tm+mt
source-wordcount: '729'
ht-degree: 2%

---

# [!DNL Pinterest Customer List] 連線

## 概觀 {#overview}

從您的客戶清單、造訪過您網站的人，或已在Pinterest上與您的內容互動的人中建立對象。

>[!IMPORTANT]
>
>此目的地是由Pinterest團隊建置。 如有任何查詢或更新要求，請直接透過https://help.pinterest.com/en/contact聯絡。

## 先決條件 {#prerequisites}

* 使用者必須使用Pinterest帳戶進行驗證，該帳戶具有其要新增受眾的廣告商帳戶的存取權。 您可以找到共用廣告商帳戶的詳細資料 [此處](https://help.pinterest.com/en/business/article/share-and-manage-access-to-your-ad-accounts). 具體來說，使用者需要「對象」存取層級。
* 有關客戶清單身分格式的詳細資料可找到 [此處](https://help.pinterest.com/en/business/article/audience-targeting).

## 支援的身分 {#supported-identities}

此 [!DNL Pinterest Customer List] 目的地支援下表所述的身分啟用。 進一步瞭解 [身分](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=en#getting-started).

在 [對應步驟](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) 在目標啟用工作流程中，將所需的身分對應到目標欄位 *pinterest_audience*. 身分識別會在資料擷取至Pinterest時區分和解析。

| 目標身分 | 說明 | 考量事項 |
|---|---|---|
| GAID | [!DNL Google Advertising ID] | 對應 *GAID* 將來源身分名稱空間新增至目標身分欄位 *pinterest_audience*. 身分識別會在資料擷取至Pinterest時區分和解析。 |
| IDFA | [!DNL Apple ID for Advertisers] | 對應 *IDFA* 將來源身分名稱空間新增至目標身分欄位 *pinterest_audience*. 身分識別會在資料擷取至Pinterest時區分和解析。 |
| 電子郵件 | 電子郵件地址（純文字或使用SHA256演演算法雜湊） | Adobe Experience Platform同時支援純文字和SHA256雜湊電子郵件地址。 <br> 對應 *電子郵件* 或 *Email_LC_SHA256* 將來源身分名稱空間新增至目標身分欄位 *pinterest_audience*. |

{style="table-layout:auto"}

## 匯出型別和頻率 {#export-type-frequency}

請參閱下表以取得目的地匯出型別和頻率的資訊。

| 項目 | 類型 | 附註 |
---------|----------|---------|
| 匯出型別 | **[!UICONTROL 對象匯出]** | 您正在匯出具有Pinterest客戶清單目的地所使用識別碼（名稱、電話號碼或其他）的對象所有成員。 |
| 匯出頻率 | **[!UICONTROL 串流]** | 串流目的地是「一律開啟」的API型連線。 一旦根據對象評估在Experience Platform中更新了設定檔，聯結器就會將更新傳送至下游的目的地平台。 深入瞭解 [串流目的地](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## 使用案例 {#use-cases}

為了協助您更清楚瞭解您應如何及何時使用 [!DNL Pinterest Customer List] 目的地，以下是Adobe Experience Platform客戶可以使用此目的地解決的範例使用案例。

### 使用案例#1

從您的客戶清單、造訪過您網站的人，或已在Pinterest上與您的內容互動的人中建立對象。

## 連線到目的地 {#connect}

>[!IMPORTANT]
> 
>若要連線到目的地，您需要 **[!UICONTROL 管理目的地]** [存取控制許可權](/help/access-control/home.md#permissions). 閱讀 [存取控制總覽](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得必要許可權。

若要連線至此目的地，請遵循以下說明的步驟： [目的地設定教學課程](../../ui/connect-destination.md).

### 連線引數 {#parameters}

當 [設定](../../ui/connect-destination.md) 您必須提供下列資訊給此目的地：

* **[!UICONTROL 名稱]**：您日後可辨識此目的地的名稱。
* **[!UICONTROL 說明]**：可協助您日後識別此目的地的說明。
* **[!UICONTROL 廣告商ID]**：您的Pinterest廣告商ID。

### 啟用警示 {#enable-alerts}

您可以啟用警報以接收有關傳送到您目的地的資料流狀態的通知。 從清單中選取警報以訂閱接收有關資料流狀態的通知。 如需警示的詳細資訊，請參閱以下指南： [使用UI訂閱目的地警報](../../ui/alerts.md).

當您完成提供目的地連線的詳細資訊時，請選取「 」 **[!UICONTROL 下一個]**.

## 啟用此目的地的對象 {#activate}

>[!IMPORTANT]
> 
>* 若要啟用資料，您需要 **[!UICONTROL 管理目的地]**， **[!UICONTROL 啟用目的地]**， **[!UICONTROL 檢視設定檔]**、和 **[!UICONTROL 檢視區段]** [存取控制許可權](/help/access-control/home.md#permissions). 閱讀 [存取控制總覽](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得必要許可權。
>* 要匯出 *身分*，您需要 **[!UICONTROL 檢視身分圖表]** [存取控制許可權](/help/access-control/home.md#permissions). <br> ![選取工作流程中反白顯示的身分名稱空間，以將對象啟用至目的地。](/help/destinations/assets/overview/export-identities-to-destination.png "選取工作流程中反白顯示的身分名稱空間，以將對象啟用至目的地。"){width="100" zoomable="yes"}

讀取 [將設定檔和受眾啟用至串流受眾匯出目標](/help/destinations/ui/activate-segment-streaming-destinations.md) 以取得啟用此目的地對象的指示。

## 資料使用與控管 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 處理您的資料時，目的地符合資料使用原則。 如需如何操作的詳細資訊 [!DNL Adobe Experience Platform] 強制執行資料控管，請參閱 [資料控管概觀](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=zh-Hant).

## 其他資源 {#additional-resources}

請參閱 [pinterest說明中心頁面](https://help.pinterest.com/en/business/article/audience-targeting) 以取得其他資訊。
